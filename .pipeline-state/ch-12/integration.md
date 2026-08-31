Write permission wasn't granted, so here is the artifact directly. (The orchestrator captures stage output from stdout anyway; if you want it on disk it belongs at `../Book-KCNA/.pipeline-state/ch-12/integration.md`.)

```markdown
# Integration Check — KCNA Chapter 12

## Summary

- Terminology consistency: **fail** (scoped — every canonical-form rule holds; the acronym-expansion rule is breached on 6 terms, one of them book-wide)
- Callbacks to earlier chapters: **48 correct / 1 incorrect** (49 checks: 28 distinct cross-bearing targets across 41 bracketed instances, plus 21 narrative attributions; 2 of the correct ones carry quote-attribution drift)
- Retrieval-practice accuracy: **pass** (8 tags, all 8 aligned)
- Glossary coverage: **57 concepts introduced, 51 defined in-chapter, 6 require glossary entries (12 further entries advisable)**
- Contradictions with earlier canon: **none**
- Ethical guardrails (skill Part 14): **pass**

Chapters 1–11 are shipped and were read directly from the book repo, so nothing here is inferred from the absence of knowledge-base shards. The `[no knowledge-base shards tagged]` input was worked around by verifying against `chapter-01`…`chapter-11`.

**Section numbering verifies clean.** All nine section numbers and titles match the B6 skeleton exactly. The heading form is the recommended Ch 5–8 pattern (`## <difficulty> §N — Title`), and §9 carries `☀️` per skeleton recommendation #4. All twelve section-pinned inbound pointers from shipped text (§2, §3 ×2, §4 ×2, §5 ×3, §6, §9 ×2) land on a section that delivers what the pointer promises.

**One structural defect the revision stage did not catch is a content loss, not a nit** — see H2. It is a two-character fix.

---

## Terminology consistency

### Canonical forms — all clean

| Term | Canonical form | Occurrences | Drift? |
|---|---|---|---|
| ServiceAccount | `ServiceAccount` CamelCase | 48 | no |
| NetworkPolicy | `NetworkPolicy` one word | 20 | no |
| kubelet | lowercase, never `Kubelet` | 13 | no |
| etcd | lowercase, even sentence-initially | 27 | no |
| kubectl | lowercase, code style | — | no |
| Pod Security Standards | spelled out, title case | 12 | no |
| Pod Security Admission | spelled out, title case | 16 | no |
| TokenRequest | CamelCase | 7 | no |
| DaemonSet | CamelCase, unspaced | 2 | no |
| RuntimeClass | CamelCase | 1 | no |
| ResourceQuota / LimitRange | CamelCase, unspaced | — | no |
| PersistentVolume | CamelCase | — | no |
| cloud native | **never hyphenated** | 6 prose uses | **no** |
| Linux namespace | qualified, never bare | 2 | no |
| control plane | cluster sense only (no mesh sense present) | — | no |
| binding | RBAC objects always written out in full | — | no |

Two of those deserve calling out as done deliberately well:

- **`cloud native` is unhyphenated in every prose use.** All 34 hyphenated hits in the file are inside snapshot filenames (`k8s-docs-4cs-cloud-native-security-…`), which the canonical-forms table exempts as resource names. Ch 12 adds nothing to the ⚑8 hyphenation debt carried by Ch 1–8.
- **§3 opens by disposing of the `binding` homonym explicitly** — third distinct sense in six chapters, the second met last chapter — and then holds the rule: `RoleBinding` and `ClusterRoleBinding` are always written out, never shortened to "binding". This is exactly what the Canonical forms table asks for, and it is the highest-collision-risk word in the chapter.

Also clean: no retired marker names (`Shoals Ahead`, `Landfall`); no object-name spacing errors (`Cluster Role`, `Service Account`, …); no `Kubelet`/`Etcd`/`Kubectl` miscasing; no branded marker inside a fenced code block (checked all eight fence ranges against every marker glyph — zero hits, so the EPUB empty-box trap does not fire here).

### Acronym expansion — 6 breaches

The B7 register's rule is absolute: *"Every acronym is expanded on its first use in the book, without exception."* Six terms breach it. Expanded correctly and needing no action: CVE, SBOM, TUF, OPA, UID, GID, and OpenID Connect (spelled out, acronym never used).

| Acronym | Register row | Status in Ch 12 | Severity |
|---|---|---|---|
| **RBAC** | `RBAC \| Role-Based Access Control \| Ch 12 §3` | never expanded; ~80 uses. **Never expanded anywhere in the book** — see M1 | medium |
| **PSA** | `PSA \| Pod Security Admission \| Ch 12 §6` | never introduced as an abbreviation; 19 uses beginning in a graded answer | **high** |
| **PSS** | `PSS \| Pod Security Standards \| Ch 12 §6` | never introduced as an abbreviation; 8 uses beginning in §8 | **high** |
| **CEL** | *absent from register* | 3 uses, unexpanded, including the Chapter Summary | medium |
| **OWASP** | *absent from register* | 1 use, unexpanded (§7) | medium |
| **SPDX** | *absent from register* | 3 uses, unexpanded (§7) | medium |

### Minor naming drift

`imagePullSecret` (singular) appears 4 times against 1 use of the plural. The field is `imagePullSecrets`, and that is the form shipped Ch 2 §6 uses. The singular is the Kubernetes documentation's own informal prose usage, so it is defensible inside quoted material at §2 — but §7's `An imagePullSecret holds registry credentials` is the book's own voice naming a field that does not exist under that spelling.

---

## Callback correctness

### Cross-bearings — 28/28 targets verified

Every `Ch N §M` pointer was checked mechanically against the B6 skeleton, then against the shipped headings for Ch 2–11. **All 28 distinct targets resolve; none disagrees with the skeleton.** Forward pointers into undrafted chapters (Ch 13 §2, Ch 15 §4, Ch 15 §5, Ch 16 §3, Ch 17 §4, Ch 17 §5) all name a section the skeleton actually grants, with the topic the skeleton assigns it — no invented section numbers.

Reciprocity also holds. Shipped text emits 12 section-pinned pointers into this chapter and all 12 land correctly:

| Inbound pointer | From | Delivered by |
|---|---|---|
| `Ch 12 §2 — ServiceAccounts as RBAC subjects` | ch05:779 | §2 — partially; see L3 |
| `Ch 12 §3 — Role, ClusterRole, and the binding model` | ch08:426 | §3 ✓ |
| `Ch 12 §3 — namespaced and cluster-scoped permissions` | ch08:577 | §3 ✓ (the derivation, exactly as promised) |
| `Ch 12 §4 — Secrets are not encrypted` | ch11:444 | §4 ✓ (title matches verbatim) |
| `Ch 12 §4 — Secrets, and encryption at rest` | ch08:967 | §4 ✓ |
| `Ch 12 §5 — what a Pod may do to its node` | ch10:1035, ch11:440, ch11:896 | §5 ✓ (title matches verbatim) |
| `Ch 12 §6 — Pod Security Standards and Pod Security Admission` | ch08:471 | §6 ✓ |
| `Ch 12 §9 — additive, never deny` | ch10:1312 | §9 ✓ (title matches verbatim) |
| `Ch 12 §9 — RBAC and NetworkPolicy as one shared semantic` | ch10:1201 | §9 ✓ |

### Narrative attributions — 20/21 correct

Twenty-one prose callbacks were traced to the actual sentence in shipped text. Twenty are correct, several verbatim:

- **Ch 4 §5** — *"a specific, confident, wrong prediction in Chapter 12"* — verbatim at ch04:839. §3 pays it off exactly as set up.
- **Ch 4 §4** — *"the lock is Chapter 12's; this chapter is only telling you the box did not ship with one fitted"* — verbatim at ch04:648.
- **Ch 8 §2** — *"you will not be learning a new kind of thing. You will be learning one instance of the third gate"* — verbatim at ch08:471. §6 discharges it in its opening paragraph.
- **Ch 2 §2** — *"the hinge on which supply-chain verification swings"* — verbatim at ch02:393.
- **Ch 11** — the "no way to say no" tell (ch11:1638), the workload-to-host apparatus (ch11:440), the `securityContext` quote (ch11:896), and the half-argument on file-over-env-var (ch11:444) — all four of Ch 11's closing promises located and closed.
- **Ch 10** — *"Hold on to the phrasing about subtraction"* (ch10:1312) and the two-axes framing (ch10:1035) — both correct; §9 retrieves the semantic by name as Ch 10 said it would.
- **Ch 8 §7** — *"Chapter 12 covers why 'keep it encrypted' is not paranoia. It is the reason that clause is in the sentence"* (ch08:967). §4 closes it with near-matching wording (*"That is why the clause is in the sentence"*). Clean callback craft.
- **Ch 6 §3** (ch06:486), **Ch 6 §8** (ch06:981), **Ch 7 §4** (ch07:726), **Ch 5 §6** (ch05:779), **Ch 4 §3** (ch04:565, ch04:1239), **Ch 8 §3**, **Ch 2 §1**, **Ch 2 §6** — all verified.

**One is incorrect. See H1.**

### Two quote-attribution drifts (both minor, both in the "correct" column)

1. **§7 opening** attributes *"a genuine security boundary rather than a convenience feature"* to `imagePullSecrets`. Ch 2:459 applies that phrase to **registry access**: *"Registry access is also a genuine security boundary rather than a convenience feature."* The phrase is verbatim; the subject has been transposed. Since it is set in italics — the book's quotation signal — it reads as a quote about a thing Ch 2 did not say it about.
2. **§3** says *"Chapter 8 quoted that list at you and pointed here"* of a four-item list (Node, ABAC, RBAC, Webhook). Ch 8:426 quotes three: *"such as ABAC mode, RBAC Mode, and Webhook mode."* Node is absent from Ch 8's quote. "Quoted part of that list" would be accurate.

---

## Retrieval-practice accuracy

Eight tagged items. **All eight aligned** — each tag names a chapter that actually owns the retrieved material, and in every case the retrieved half is genuinely earlier-chapter knowledge rather than this chapter's content wearing a tag.

| # | Tag | Retrieved topic | Owner in shipped text | Aligned? |
|---|---|---|---|---|
| TYB#1 Q3 | `ch4` | cluster-scoped resource is in *no* namespace | Ch 4 §3 (ch04:1239 states the "none, not all" distinction explicitly) | yes |
| TYB#2 Q5 | `ch8` | admission is the third and last gate | Ch 8 §2 (ch08:410, 455) | yes |
| TYB#3 Q1 | `ch2` | tag is a mutable pointer; digest is identity | Ch 2 §3 | yes |
| Practice 8 | `ch4` | RBAC names subjects; everything else selects | Ch 4 §5 (ch04:839, the planted prediction) | yes |
| Practice 15 | `ch10` | the two axes — reachability vs workload-to-host | Ch 10 §6/§7 (ch10:1035) | yes |
| Practice 18 | `ch8` | the admission gate as a shared position | Ch 8 §2 | yes |
| Practice 19 | `ch2` | signature binds to the digest | Ch 2 §3 | yes |
| Practice 21 | `ch10` | additive semantics, no deny rule | Ch 10 §6 (ch10:1120, 1308) | yes |

Two things worth recording as done right. **Practice 15 and 21 are true interleaving** rather than disguised same-chapter items: each requires holding a Ch 10 fact and a Ch 12 fact simultaneously and discriminating between them, which is what the spacing-effect table in skill Part 10 asks for. And the **Soundings arithmetic checks out** — the block claims "six of these test material from earlier chapters," and exactly six (Q1, Q2, Q3, Q4, Q5, Q8) point at Ch 4 §3, Ch 5 §6, Ch 4 §4, Ch 8 §2, Ch 10 §6 and Ch 2 §1 respectively, with Q6 and Q7 correctly identified in the preamble as the two drawing on outside professional intuition instead.

Counts against the skill: Soundings 8 (content chapter ✓), Taking Your Bearings 15 across three checkpoints of 5 (≥10 across ≥2 ✓), Practice Questions 23 with 46 numbered blocks — 23 stems, 23 answers, no orphans.

---

## Glossary coverage

57 concepts/commands introduced. 51 are defined in place and need no entry. The table below lists only the interesting cases; the routine ones (Role, ClusterRole, RoleBinding, verbs, `resourceNames`, aggregated ClusterRoles, the four default roles, `escalate`/`bind`, binding immutability, `EncryptionConfiguration`, the Secret-type table, `securityContext` at both scopes, capabilities, seccomp, AppArmor, SELinux, `privileged`, the three PSS levels, the three PSA modes, keyless signing, attestation, provenance, transparency log, policy engine, in-toto, TUF, Harbor, Kyverno, Falco, Policy as Code) are all defined in-chapter and are omitted.

### Required — reaches reader text without a definition

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| **CEL** | no — used bare 3×, including the Chapter Summary | **yes** (+ register row) |
| **OWASP** | no — acronym unexpanded | **yes** (+ register row) |
| **SPDX** | no — acronym unexpanded | **yes** (+ register row) |
| **Kubewarden** | no — named once inside a sourced list, never glossed | **yes** |
| **CVE** | expanded, but the expansion is unsourced (draft's own AUTHOR-REVIEW) | **yes** |
| **SBOM** | glossed, but no canonical definition exists in the corpus (draft's own AUTHOR-REVIEW) | **yes** |

### Advisable — defined in place, but absent from the B7 ledger

The ledger's §7 row grants this chapter *"in-toto · TUF · Notary"* and nothing else from the signing ecosystem. Six named projects and one language arrive here with no ledger row at all, plus five terms that are graded or near-graded:

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Sigstore | yes | advisable — no ledger row |
| Cosign | yes | advisable — no ledger row |
| Fulcio | yes | advisable — no ledger row |
| Rekor | yes | advisable — no ledger row |
| Policy Controller | yes | advisable — no ledger row |
| Notary Project / Notation | yes | advisable — **ledger says "Notary"; canonical form needs a ruling** |
| CycloneDX | yes (via quote) | advisable — no ledger row |
| Rego | yes ("a purpose-built policy language") | advisable |
| `system:masters` | yes | advisable — it is graded (Practice Q3) |
| Secrets Store CSI Driver | yes | advisable |
| TokenReview | yes — but only inside a Practice Q4 distractor explanation | advisable |
| ABAC | one clause, exactly as the ledger licenses | already routed glossary-only ✓ |

The ABAC handling is worth a note as correct: the ledger's orphan entry says ABAC *"must not appear as a distractor unless that clause is written."* §3 writes the clause — *"RBAC is what essentially every cluster uses… but it is one mode among several rather than the mechanism"* — and then never uses ABAC as a distractor. That is the rule followed precisely.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Only three numbers appear: 28% (published D2 weight, source-tagged), 12% (D4, inside an AUTHOR-REVIEW), and the ~7% chapter allocation. The 7% carries a dedicated opening paragraph disclosing it as *"this book's own allocation… a planning number for your study time, not a fact about the exam,"* and noting that *"anyone who gives you one is guessing."* This is the strongest version of that disclosure in the book so far.
- [x] **Fear-based content uses real examples.** The §4 hazards are documented mechanisms (`create pods` → Secret read; the etcd backup) rather than invented breach anecdotes. No third-party harm is used for stakes.
- [x] **Simplification acknowledged.** Three Dead Reckoning blocks. §1 sets out "the honest situation" on why two maps are taught; §4 gives "the honest accounting of what encryption at rest gives you" and names what it leaves open; §9 states its own epistemic status before making its argument — *"What follows is therefore a reading, not a citation… Hold it more loosely than you hold the facts around it"* — and then names the cost of the design it is defending. That is skill Part 11's Order/Truth pattern executed properly, not a hedge.
- [x] **Authority claims cite legitimate sources.** Source tags throughout; the four places where the prose is the author's reasoning rather than documentation are each marked in an AUTHOR-REVIEW comment so no later stage attaches a false tag.
- [x] **"Frequently tested" claims are verifiable.** The Exam Alert closes with an explicit refusal: the one `[inferred]` row *"describes something easy to confuse, not something anyone has published as frequently tested… it will not manufacture a statistic to make the point land harder."* The two "highest-yield" claims (Attention Budget, Exam Alert item 1) are author judgment reasoned from the published objectives, which is the standard that paragraph sets for itself.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (skill v5.7).** The wry beats — *"unpleasant to debug at 3 a.m."*, *"a plaintext password in a Git repository with a costume on"*, *"Signing without verification is theater"* — are all oriented at the practitioner. Nothing is aimed at people harmed by a breach.

**Pass.**

---

## Recommended fixes

Everything in the diagnostics was addressed by the revision stage; these are new. Two are worth doing before the chapter ships, four are cheap, and the rest are author decisions.

### H1 — §8 credits Chapter 8 with a distinction Chapter 8 never draws

§8 says: *"Validate and mutate map exactly onto a distinction Chapter 8 drew: validating and mutating admission webhooks… **Chapter 8 gave you the two webhook types as an abstraction.** A policy engine is one. It is… the cleanest possible payoff for having learned the distinction."*

Chapter 8 did not give the reader the two webhook types. Verified: `mutating` appears in shipped Ch 8 **only** in the frontmatter `concepts_covered` list (ch08:126) — zero prose occurrences. `validating` appears once in prose, at ch08:475, in a Closer Look about webhook availability. The B7 ledger corroborates from the other side: its Ch 8 gate note puts *"mutating/validating admission webhook"* on the glossary queue, meaning the pair was deferred, not taught.

What Chapter 8 *did* establish is better for this passage anyway — ch08:608: *"Two of them are asking about you and answering yes or no; the third is asking about the request itself and has a third answer available: yes, in modified form."* That is the distinction, stated as a capability. Suggested rewrite preserving the payoff:

> Validate and mutate are the two answers Chapter 8 told you the third gate has. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]* Two gates answer yes or no; the third can also answer *yes, in modified form*. Those two answers have names — a **validating** admission webhook and a **mutating** one — and **a policy engine is one.**

This keeps the recognition beat, attributes it correctly, and introduces the two webhook types here (which the ledger permits: it names Ch 8 §2 as owner, but Ch 8 shipped without them and the glossary queue already records the gap).

### H2 — Broken table row in the Exam Alert, dropping a correction

Line 1535 has three cells in a two-column table, with the trap text duplicated and a missing space before the second pipe:

```
| PSS levels and PSA modes are the same axis| PSS levels and PSA modes are the same axis | Levels say what is checked; modes say what happens. Independent. `[inferred]` |
```

Under GFM and pandoc, cells beyond the header count are discarded. The reader sees the trap in column one and *the same sentence again* in the "correct understanding" column; the actual correction is silently dropped. This is the one row the closing paragraph then discusses by name, so that discussion refers to text the reader cannot see. Fix:

```
| Pod Security levels and admission modes are the same axis | Levels say what is checked; modes say what happens. Independent. `[inferred]` |
```

### H3 — Introduce PSS and PSA, or stop using them

Neither abbreviation is ever bound. §6 spells both out and never abbreviates; the first bare **PSA** is at line 1084 in a Taking Your Bearings answer, and the first bare **PSS** is at line 1250 in §8. They then run through the Exam Alert, four Practice answers, and the Chapter Summary — 19 and 8 uses respectively, much of it in graded text.

Cheapest fix: one parenthetical each at the Fixed Point in §6, introducing **Pod Security Standards (PSS)** and **Pod Security Admission (PSA)** at their first bold use in that section. Alternatively, expand them everywhere and drop the abbreviations — §6 reads well without them, and the register rows exist either way.

### M1 — Expand RBAC once, in §3

Verified book-wide: `Role-Based Access Control` appears in no chapter. Ch 4 writes the lowercase expansion twice (ch04:257, ch04:839) with no acronym adjacent; Ch 4:646, Ch 5, Ch 6, Ch 8 and Ch 10 all use bare `RBAC`. The acronym is never bound to its expansion anywhere in the book, and Ch 12 §3 is the ledger's owner. One clause at the top of "RBAC is *an* authorization mode" fixes it: **RBAC — role-based access control —** *"regulates access based on the roles of individual users within an enterprise."*

### M2 — Expand CEL, OWASP, SPDX; add register rows for all three

Three lines of prose and three register rows. CEL is the priority of the three because it survives into the Chapter Summary, which readers use as a revision surface.

### M3 — "Two interfaces you already know" collides with the four-interface thread

§4, line 730: *"a CSI driver… delivered as a DaemonSet…, doing a job through two interfaces you already know."* A DaemonSet is a workload controller, not one of the four pluggable interfaces. The skeleton's ⛑ note records that interface counting has already produced one collision in this book (Ch 9 §8's "second instance" against Ch 10 and Ch 11's "three of four") and that Ch 17 §4 inherits a reader who has been reconciled — so a reader tracking that thread will stop here and try to make four minus three equal two. Fix: **"two mechanisms you already know."**

### L1 — "doing a third job" is a running ordinal

§7, line 1242: *"Which is the third gate again, doing a third job."* "Third gate" is fine — a closed set of three the reader can see. "A third job" counts instances of something the reader has not been given a closed set for, which is precisely what the ratified convention forbids. Fix: **"doing another job."**

### L2 — Two quote attributions (detail under Callbacks)

§7: attribute *"a genuine security boundary rather than a convenience feature"* to registry access, as Ch 2:459 does, or drop the italics and paraphrase. §3: *"Chapter 8 quoted part of that list at you."*

### L3 — Name "subject" in §2, where the ledger and a shipped pointer both expect it

The B7 ledger assigns both *ServiceAccount as an RBAC subject* and *Subject (RBAC subject)* to **§2**. In the draft the word is used once in §2 (line 285, *"is a subject exactly like any Pod is a subject"*) before §3 defines it at line 386. Shipped Ch 5:779 sends readers here with the promise *"see Ch 12 §2 — ServiceAccounts as RBAC subjects."*

One clause in §2 — after the "identity and a permission are two different things" Fixed Point, naming *subject* as RBAC's word for whatever a grant is made to, with a pointer to §3 — honors the ledger, lands the inbound pointer, and removes the use-before-definition. Worth noting that Ch 5's pointer over-promises §2 in any case (it also advertises grants and the privilege-escalation path, which are §3 and §4); the chapter delivers all of it, just across three sections. That is shipped text's defect, not this chapter's, and the one clause makes §2 a correct landing point regardless.

### L4 — `imagePullSecret` → `imagePullSecrets` in §7's authorial sentence

Leave the singular where it sits inside quoted documentation.

### Author decisions (not defects)

- **D4 under-declaration — corroborated.** `outline.md` declares `exam_domain: "Container Orchestration (competency: Security)"` and asserts *"No objective ambiguity: Security is the only competency this chapter touches."* Against that: §1 teaches the 4Cs and the lifecycle phases; §7 teaches Sigstore, in-toto, TUF, the Notary Project, Harbor and the SBOM standards; §8 teaches Policy as Code (from the CNCF glossary), Kyverno, OPA/Gatekeeper and Falco. That is CNCF-ecosystem material, and D4 is 12% of the exam with few other chapters teaching it. The draft's opening AUTHOR-REVIEW recommends adding D4 to the declared objectives; the evidence supports it, and the book-close coverage report will otherwise raise a phantom "D4 under-covered" finding.
- **PodSecurityPolicy framing.** §6 says "superseded" rather than "removed in 1.25," per the draft's AUTHOR-REVIEW about the truncated snapshot. This creates **no contradiction** — `PodSecurityPolicy` appears nowhere in Ch 1–11 — but it diverges from the ledger's orphan entry and register row, both of which say "removed in 1.25." Resolve when the snapshot is re-fetched, then reconcile the ledger and the Exam Alert trap row together.
- **16 AUTHOR-REVIEW comments** are carried in `draft-v2.md`. All are substantive and correctly scoped; none should be silently dropped at materialization.
- **Two Stage 10 figure flags remain open** and are not re-raised here: `ch12-zenith-additive-never-deny` is a non-conforming anchor ID (blocking for the book-level index), and `fig03` precedes `fig02` in reading order. Both are recorded in `image-specs.md` awaiting an author call.

### Nothing else

The diagnostics from the revision cycle are all addressed. Contradictions with earlier canon: none found — the `default` ServiceAccount's permissions, the v1.22 TokenRequest recommendation, the four Secret-hardening steps, the tmpfs property, the `dockerconfigjson` pull-secret type, the additive NetworkPolicy semantic and the three-gate ordering all match shipped Ch 4, Ch 5, Ch 8, Ch 10 and Ch 11 exactly.
```

Two things to flag verbally, since they're the ones that would cost the reader something:

**H2 is a silent content loss**, not a formatting nit. The Exam Alert's level-vs-mode row has three cells in a two-column table, so pandoc drops the correction and prints the trap twice — and the paragraph immediately below discusses that row by name.

**H1 is a false promise made to the reader.** §8 tells them they already learned the mutating/validating webhook distinction in Chapter 8. Chapter 8 has zero prose occurrences of "mutating" — the word appears only in its frontmatter `concepts_covered` list, and the B7 ledger's own Ch 8 gate note confirms the pair was punted to the glossary. The recognition beat is salvageable and the suggested rewrite keeps it, because Ch 8 *did* teach the underlying idea ("*yes, in modified form*") — just not the names.