I'll inspect the book's existing knowledge base before proposing any writes.Now let me verify the integration report's claims against the ledger and shipped text rather than taking them on trust.I verified the integration report's findings against the ledger, the shipped chapters and the source corpus rather than taking them on trust. Three of its claims needed correcting, and I found two obligations it missed. Manifest follows.

# Knowledge-Base Manifest — KCNA Chapter 12

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, still true at Chapter 12.** `Book-KCNA/knowledge-base/` **does not exist on disk** — verified directly, not inferred. Chapter 10's and Chapter 11's Stage 14 manifests each composed a full set of write blocks; neither was applied. Twenty-three write blocks are now pending across three manifests.
>
> **Ordering contract — and I have inverted Chapter 11's.** Ch 11's blocks were *self-sufficient full writes* carrying Ch 10's content merged in, with a warning that replaying Ch 10 afterwards would erase Ch 11. Chapter 12 does **not** follow that pattern for the three shared files, and the reason is Rule 5: those files hold roughly sixty definitions inherited *verbatim* from documentation, and re-transcribing them through another stage is precisely how definitional drift gets introduced. Silent corruption of a quoted definition is worse than a fragment.
>
> **So: apply Ch 10 → Ch 11 → Ch 12, in that order.** Ch 11's blocks create `glossary.md`, `objective-coverage.md` and `retrieval-log.md` with Ch 10+11 content; Ch 12 **appends** to them. Appends do not clobber, so the only failure mode if the order is wrong is a headless fragment — recoverable, and no definition is at risk. Ch 12's nine *new* concept shards are fresh filenames and collide with nothing; its five *amendments* to existing shards are appends for the same reason.
>
> **One cost of that choice, stated plainly:** appending a second A–Z block to `glossary.md` leaves the file with two alphabets. That must be interleaved before the file is promoted to the shipped back-of-book glossary. Logged under Infrastructure. I judged a merge step the author can do mechanically to be cheaper than a transcription risk nobody would notice.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11's precedent. The integration report marked **6 terms** as reaching reader text with no definition; skill Part 16 requires *all* technical terms introduced in the book, so the **37 B7-owned Chapter 12 rows** (`term-ownership.md:385–421`) are harvested alongside them.

### Tier 1 — the six the reader cannot look up

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **CEL** | ⚠ **No expansion or definition in the book.** Chapter supplies only co-occurrence: Kyverno policies are *"written in YAML using declarative rules and CEL"* `[source: kyverno-overview-2026-08-23]` | Chapter 12 §8 |
| **OWASP** | ⚠ **No expansion in the book.** Used once, as CycloneDX's steward | Chapter 12 §7 |
| **SPDX** | ⚠ **No expansion in the book.** Function given: *"an open standard designed to facilitate the communication of Bill of Materials (BOM) information across diverse domains"* `[source: sbom-standards-spdx-cyclonedx-2026-08-31]` | Chapter 12 §7 |
| **Kubewarden** | ⚠ **Named once inside a sourced list of third-party enforcement options, never glossed** `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` | Chapter 12 §8 |
| **CVE** | Expanded in-chapter as *Common Vulnerabilities and Exposures* — ⚠ **expansion is unsourced**; see ⚑D | Chapter 12 §7 |
| **SBOM** | Expanded as *Software Bill of Materials* and described from what SPDX and CycloneDX say their standards cover — ⚠ **no canonical definition exists in the corpus** | Chapter 12 §7 |

**I verified all four unexpanded terms independently.** `CEL`, `OWASP`, `SPDX`, `Kubewarden` and `CycloneDX` return **zero matches across `chapter-01` … `chapter-11`** and **zero rows in the B7 acronym register** (register read in full, `term-ownership.md:655–730`). Chapter 12 is genuinely their first appearance in the book.

**One of the six reaches graded material.** `CEL` survives into the **Chapter Summary**, which readers use as a revision surface. The other five stay in body prose. B7's orphan doctrine — *"a term used in question text or an answer key may not be glossary-only"* — is not breached, but the Summary is close enough to the line to be worth the author's eye.

### Tier 2 — the 37 ledger-owned terms, harvested per skill Part 16

All 37 B7 rows for Ch 12 are defined in-chapter; I checked each against the chapter text. Definitions are inherited verbatim per Rule 5 — where the chapter quotes documentation, the glossary quotes the chapter quoting the documentation, tag intact. Full text in the write block.

The 4Cs · lifecycle phases · ServiceAccount as RBAC subject · subject · user/group · service account token · **RBAC** · Role · ClusterRole · RoleBinding · ClusterRoleBinding · rule/verb/resource · `resourceNames` · aggregated ClusterRole · the four default roles · least privilege · additive permissions · binding immutability · escalation prevention · encryption at rest · `EncryptionConfiguration` · Secret hardening · external secret store · `securityContext` · `runAsNonRoot`/`runAsUser`/`privileged` · Linux capabilities · `readOnlyRootFilesystem`/`allowPrivilegeEscalation` · seccomp · AppArmor · Pod Security Standards · Pod Security Admission · PodSecurityPolicy · image scanning · image signing/attestation/provenance · SBOM · in-toto/TUF/Notary · Harbor · supply-chain security · policy engine · OPA/Gatekeeper · Kyverno · Falco.

Plus eleven the chapter defines that the ledger does not assign: **Sigstore, Cosign, Fulcio, Rekor, Policy Controller, keyless signing, transparency log, Rego, `system:masters`, Secrets Store CSI Driver, SELinux**. And **ABAC**, routed glossary-only by the ledger's orphan doctrine — §3 writes the licensing clause the doctrine requires and then correctly never uses ABAC as a distractor.

**`TokenReview` is included as provisional.** It is defined only inside Practice Q4's distractor explanation. A term a reader meets first in an answer key is exactly the case B7's orphan doctrine is about.

---

## Concept shards at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

**Nine created.** Every Ch 12 section clears the 200-word threshold; §9 gets its own shard despite introducing no object, because the argument is cross-chapter and two later chapters inherit it.

- `concepts/security-maps-phases-and-4cs.md` — **created** (§1; the two maps, and why both)
- `concepts/serviceaccounts-and-identity.md` — **created** (§2; identity ≠ permission, TokenRequest, identity outliving the workload)
- `concepts/rbac.md` — **created** (§3; the derivation, the default roles' negative space, subjects-are-named)
- `concepts/secret-exposure-and-hardening.md` — **created** (§4; three routes, what encryption at rest closes and does not)
- `concepts/securitycontext.md` — **created** (§5; the workload-to-host axis, two scopes, `privileged` as the off-switch)
- `concepts/pod-security-standards-and-admission.md` — **created** (§6; levels × modes, the namespace as control surface)
- `concepts/supply-chain-security.md` — **created** (§7; the checkpoint sequence, signature-binds-to-digest, the four distinct claims)
- `concepts/policy-engines-and-runtime-detection.md` — **created** (§8; admission time vs runtime)
- `concepts/additive-never-deny.md` — **created** (§9; the shared semantic and its epistemic status)

**Five amended by append**, each discharging or extending an obligation an earlier shard recorded:

- `concepts/hostpath.md` — **appended** · Ch 12 §5 obligation **discharged cleanly**; the shard's instruction *"Ch 12 §5 must not re-derive the risk"* was honoured
- `concepts/volume-types-ephemeral.md` — **appended** · Ch 12 §4 obligation **discharged with a substitution** — see ⚑C
- `concepts/access-modes.md` — **appended** · the *"not a permission system"* forward pointer landed; sourcing caveat recorded
- `concepts/pluggable-interfaces.md` — **appended** · ⚑ **new counting collision at Ch 12 §4**
- `concepts/absent-component-pattern.md` — **appended** · ⛔ **still blocked, and Chapter 13 is next**

Not shard-worthy (adequately carried by the glossary): the Secret-type table, `kubectl auth can-i`, the individual Sigstore components, Rego.

---

## ⚑ Contradictions and conflicts — flagged, not resolved

Rule 6 requires these loud. **Two are new; three correct or extend the integration report.**

### ⚑ A. NEW — JWT and OIDC are assigned to Ch 12 §2 and reach the reader nowhere

B7 assigns `JWT · OIDC` to **Ch 12 §2** (*"name + scope only; glossary owns the definitions"*), and the acronym register carries both with Ch 12 §2 as owner (`term-ownership.md:677, 688`).

Verified against `draft-v2.md`:

- **`JWT` — zero occurrences.** Not in prose, not in a comment, not in a quote.
- **`OIDC` — one occurrence, at line 251, inside an HTML `AUTHOR-REVIEW` comment.** It will not reach the reader.
- `OpenID` appears once, at line 1171, spelled out, in **§7's** keyless-signing flow — not §2.

So the ledger's owner section teaches neither term. The chapter's own §2 AUTHOR-REVIEW explains why and is right to: the corpus has no snapshot covering Kubernetes authentication *mechanisms*, so §2 says only *"from outside the cluster"* rather than naming X.509, OIDC and authenticating proxies. **The deferral is correct; the ledger has not been told.**

The acronym-expansion rule is *not* breached — an acronym that never appears cannot be unexpanded — but two register rows now point at a section that does not deliver, and the glossary is supposed to own definitions the chapter was to have introduced. **Recommendation: retarget both ledger rows and both register rows away from Ch 12 §2**, either to the glossary-only tier or to a future section, and record the authentication-mechanisms fetch as an open research gap. The integration report did not catch this; it audited the acronyms that *appear*, not the ledger rows that were owed.

### ⚑ B. NEW — the Pod Security label grammar rests on a single sentence in a single snapshot

Independently checked, and it goes further than the draft's own AUTHOR-REVIEW claims.

The PSA snapshot **is** truncated exactly as the draft says — `k8s-docs-pod-security-admission-2026-08-31.md` ends at the heading `## Pod Security Admission labels for namespaces` followed by `The label form:` and nothing else. Confirmed by reading the file's tail.

What the draft did not record: **`pod-security.kubernetes.io` appears exactly once in the entire 168-snapshot corpus** — `k8s-docs-pod-security-standards-2026-08-23.md:24`, one sentence carrying the grammar, the three modes and the three levels together. No snapshot anywhere contains a literal `pod-security.kubernetes.io/enforce` string.

That single sentence is load-bearing for: §6's Dead Reckoning, §6's ★ Fixed Point, figure `ch12-fig04`'s third panel, **Taking Your Bearings #2 Q4** (which quotes three literal labels), **Practice Q16** and **Practice Q22**. The chapter's usage is legitimate — the literal keys follow by substitution from the sourced grammar — but six reader-facing sites, three of them graded, depend on one line of one file. **Re-fetching the PSA page in full is now the highest-value single fetch available to this chapter**, and it closes the multi-label question at the same time.

### ⚑ C. The Ch 11 → Ch 12 §4 obligation was discharged with a *different argument* than Ch 11 promised

`chapter-11:444` is section-pinned at Ch 12 §4 and hands the reader *"half an argument"* about file mounts versus environment variables. Ch 11's Stage 14 shard recorded the obligation. **Ch 12 §4 delivers — but the half it delivers is update propagation plus per-container scoping, not the leak argument the pinned phrasing implies.**

The chapter handles this openly and, in my view, correctly: it names the widely-repeated claim that environment variables leak into logs and `kubectl describe`, states that the Kubernetes documentation does not say it, and declines to make it. The research manifest's gap **G-C** anticipated exactly this and asked for the author's eye.

**No contradiction — but the two halves do not join the way Ch 11's sentence led the reader to expect.** Recorded in `volume-types-ephemeral.md` so a Ch 11 retrofit finds it. If the author wants the leak argument, it needs a source that neither research run found.

### ⚑ D. The RBAC acronym finding is real but narrower than the integration report states

The report says *"`Role-Based Access Control` appears in no chapter"* and that Ch 4's two uses have *"no acronym adjacent."* The first half is right; the second is not.

Verified across `chapter-01` … `chapter-11`:

| Line | Text |
|---|---|
| `chapter-04:646` | **First use of the acronym in the book, bare** — *"enable or configure RBAC rules with least-privilege access to Secrets"*, inside a sourced quotation |
| `chapter-04:257` | *"Chapter 12's role-based access control is, underneath the terminology, a namespaced-versus-cluster-scoped problem wearing a costume"* — lowercase expansion, no acronym |
| `chapter-04:839` | *"**Role-based access control** names its subjects and its resources explicitly… will make a specific, confident, wrong prediction in Chapter 12 `[cross-bearing: see Ch 12 — why **RBAC** names subjects instead of selecting them]`"* — **expansion and acronym in the same line** |

So the book *does* bind the two, at ch04:839, by adjacency. The defect is three narrower things: the acronym's **first** use (ch04:646) is bare and 193 lines earlier; the casing is sentence-case, not the register's `Role-Based Access Control`; and **Ch 12 §3, the ledger's owner, never expands it at all** (~80 bare uses). B7 flag ⚑7 anticipated exactly this and asked Ch 12 to retain ownership.

**The fix is the same either way** — one clause at §3 — but it is a *binding-and-ownership* fix, not a first-expansion fix, and stating it correctly matters if a retrofit pass ever greps for the expansion and concludes the job is done.

### ⚑ E. PodSecurityPolicy — chapter and ledger diverge, and nothing reconciles them

§6 says *"superseded"* and deliberately omits a version, per the draft's AUTHOR-REVIEW about the truncated snapshot. The ledger says **removed in 1.25**, twice: the acronym register row (`term-ownership.md:696`) and the orphan routing (`:824–828`, *"Ch 12 §6 owns a single clause naming it as removed"*). Research gap **G-H** records that no snapshot in the corpus contains a removal sentence.

**No contradiction with shipped text** — `PodSecurityPolicy` appears in zero of Chapters 1–11, verified. But the ledger, the register and the chapter now say two different things, and the Exam Alert's trap row was softened to match the chapter. **Resolve all four together when the PSA page is re-fetched**, not one at a time.

### ⚑ F. Chapter 12 §4 adds a fourth reading to the interface-counting thread

§4, line 730: *"a CSI driver… delivered as a DaemonSet…, doing a job through **two interfaces** you already know."* A DaemonSet is a workload controller, not one of the four pluggable interfaces. The integration report's fix — *"two mechanisms"* — is right.

Recorded in `pluggable-interfaces.md` because that shard already holds two live conflicts and **Ch 17 §4 is the section that meets all of them**. This is the third distinct counting error in the thread (Ch 9's *"second instance"*, the B6 skeleton's stale ordinal annotations, now this), which is itself the argument for the standing recommendation: **stop asserting ordinals over sets the reader is still accumulating.**

### ⛔ G. The absent-component instance count is unchanged, and Chapter 13 is next

Chapter 12 does not touch the pattern — **zero occurrences of `absent-component` or `without its component does nothing` in `draft-v2.md`**, verified. So the conflict Ch 11 opened is neither worsened nor resolved, and the block stands: **Ch 13 §7 and Ch 17 §7 are contractually required to retrieve the pattern by name, and the two live counting conventions still differ by exactly two.**

Chapter 13 drafts next. This is the last manifest before the deadline.

One observation that bears on the recommendation. §7 contains a clean unnamed instance — *"Signing without verification is theater. A signature that nothing checks is a file in a registry"* — and §4 contains a second, in the `identity`-provider trap (*"a configuration file that looks configured is not the same as encryption that is on"*). Chapter 12 wrote both **without reaching for the pattern's name or an ordinal, and both land**. That is a working demonstration of Ch 11's preferred option: the rule transfers, the number does not.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Epistemic status, pre-emptive** | "The documentation states the property and does not explain it… What follows is therefore **a reading, not a citation**. It is the interpretation that makes the best sense of what both systems do. **Hold it more loosely than you hold the facts around it.**" | **Strong candidate.** Ch 10 and Ch 11 both nominated provenance passages that separate a sourced claim from a book inference *after the fact*. This one declares the status **before the argument**, and gives the reader an instruction about how to hold it. That is a third distinct move and the catalog has no instance. |
| **Refusing a number** | "There is no published figure for how much of Domain 2 is security, and anyone who gives you one is guessing. The ~7% above is this book's own allocation… It is a planning number for your study time, **not a fact about the exam**." | **Strong candidate.** Skill Part 14's "never fabricate statistics" guardrail made concrete and reader-facing rather than kept as an internal rule. Strongest version of this disclosure in the book so far, and it is short enough to excerpt cleanly. |
| **Extended Analogy** | The locks / strongbox / watch triptych — "The **key** is not the permission… The **strongbox is not the safe**… And the **watch does not prevent anything**." | **Strong candidate.** Distinct from Ch 11's nominated Extended Analogy in construction, not just subject: each of the three panels is built to kill one *named* misconception, and the chapter then discharges all three in §2, §4 and §8. An analogy with a verifiable contract, rather than an evocative one. |
| **Why-wrong explanation** | "The audit is not sloppy — it enumerated every object correctly and read the permission it was looking for accurately. **It is reading a permission that is not the relevant one.**" | **Strong candidate.** Skill Part 11 requires why-wrong explanations everywhere and the catalog has no exemplar of the hardest kind: a distractor that is wrong *while being competently reasoned*. Ch 11's nomination ("right outcome, wrong reason") is the neighbouring case, not this one. |
| **Naming what a control does not cover** | "The lock is on the box; it says nothing about who is handed the box. **That is not a shortcoming; it is the definition of the control.** But an engineer who enables encryption at rest and believes the Secrets problem is now solved has closed one of three doors and stopped counting." | **Strong candidate.** Defends a control and limits it in the same breath, without hedging either. |
| **Identity framing / chapter close** | "Most of what separates a competent Kubernetes engineer from a trusted one is not knowing more controls. It is knowing what each control does *not* cover, and **refusing to be reassured by a green check mark that was measuring the wrong thing.**" | **Moderate.** Skill Part 3 identity transformation, executed well. Marked moderate only because the catalog may already be well supplied with chapter-closing identity beats — an author check against the existing set is the deciding factor, not the prose. |
| **Exam-alert honesty** | "That mark means the row describes something *easy to confuse*, not something anyone has published as *frequently tested*… it will not manufacture a statistic to make the point land harder." | **Moderate — promote at most one of this and the 7% passage.** Same principle, same chapter, and the 7% version is earlier, longer and better situated. Two exemplars of one move would over-weight the catalog. |

---

## Objective coverage log

Appended to `objective-coverage.md`. Concept-level audit walked row by row against `domain-analysis.md:194–212`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D2.2 — Security** | **Chapter 12** | **deep — primary home; Ch 10 held the NetworkPolicy boundary only** | — |
| D4 — Cloud Native Architecture (ecosystem) | Chapter 12 §1, §7, §8 | **substantial but undeclared** — see below | — |

**D2.2 concept coverage: 16 of 19 taught here, 2 assigned elsewhere by design, 1 unassigned anywhere.**

RBAC · Role · ClusterRole · RoleBinding · ClusterRoleBinding · additive permissions · binding immutability · `cluster-admin` · `admin` · `edit` · `view` · Secret storage default · Secret exposure paths · Secret hardening steps · Secret types · ServiceAccount token modernization — **all deep, all in Chapter 12.**

- **NetworkPolicy as a security control** → Chapter 10, per B1 sequencing implication #6. Ch 12 §9 refers and does not re-teach. Contract honoured exactly.
- **Zero trust via service mesh** → Chapter 17 §5, per the lineup. Ch 12 §4 cross-bears forward.
- **Securing the kubelet** → ⚠ **assigned to no chapter.** `kubelet` returns **zero matches in `chapter-lineup.md`**, verified. Ch 12 gives it two glancing touches — §1's runtime/access clause about TLS between nodes and the control plane, and §3's one-line description of the **Node** authorization mode — and nothing on TLS bootstrapping or kubelet authentication/authorization. **This is a genuine D2.2 hole, and Chapter 12 was the natural home.**

**Trap coverage: 10 of 10 D2.2 RBAC/Secret traps (#53–#62) addressed**, verified line by line against `domain-analysis.md:561–570`. The Exam Alert reproduces all ten in order with faithful corrections, and adds **six** the inventory does not carry: `system:masters`, `list`/`watch` on Secrets, the level/mode axis confusion, PodSecurityPolicy, signature-covers-the-tag, and valid-signature-means-current. Traps #50–#52 are NetworkPolicy and remain Chapter 10's.

**Research gaps closed by Chapter 12:**

| Gap | Status |
|---|---|
| **G5** — PSS/PSA and `securityContext`; *"the single most conspicuous D2.2 absence"* | **Closed** by §5 and §6. The research manifest records §5 going from the worst-sourced section in the chapter to the best. |
| **G6** — the 4Cs of Cloud Native Security | **Closed** by §1, from the Kubernetes project's own archived v1.22 page, with the version banner preserved. |
| **G7** — ServiceAccounts as a concept | **Closed** by §2 — the Pod-identity mechanism, the user-account contrast, and the token flow. |
| **G22** — supply chain | **Mostly closed** by §7. **CVE and the SBOM definition remain open** (G-A, G-B); image-scanning *mechanics* remain unsourced, which is why the *scan* subsection is deliberately thin. |
| **G23** — policy engines: OPA/Gatekeeper, Kyverno, Falco | **Closed** by §8. |
| **G-D** — why RBAC names subjects rather than selecting them | **Discharged as the author's reading**, marked in prose and in an AUTHOR-REVIEW, honouring `chapter-04:839`'s promise. |
| **G-E** — §9's design rationale, confirmed unsourceable | **Discharged in the Simple Version / Full Picture uncertainty form**, exactly as the research manifest required. |
| **G-F** — orphaned identity after workload deletion | **Closed** by §2, derived from garbage-collection semantics with the pointer back to Ch 6 §3. |
| **G-G** — cosign's tag-to-digest behaviour | **Closed by substitution** — attributed to the Notary Project, not to Sigstore, as the research manifest directed. |

**Still open and touching Chapter 12:** G-A (CVE — needs a hand-pasted `cve.org` snapshot; the CVE Program's mission sentence *is* recorded in the research manifest from the archived MITRE page and could be used today), G-B (SBOM definition — CISA and NTIA both returned HTTP 403), G-H (PodSecurityPolicy removal), image-scanning mechanics, Kyverno's four verbs (`kyverno.io/docs/policy-types/` — the chapter's glosses are the author's), and the authentication-mechanisms page now needed by ⚑A.

**G30 — sandboxed runtimes.** The lineup assigns it to Chapter 12; §5 refers to Ch 2 §7 rather than teaching it, which is the right call. **Backfill should confirm Ch 2 §7 actually closed it.**

**⚑ D4 under-declaration — corroborated independently.** `outline.md` declares `exam_domain: "Container Orchestration (competency: Security)"` and asserts *"No objective ambiguity: Security is the only competency this chapter touches."* Against that: §1 teaches the 4Cs and the lifecycle phases; §7 teaches Sigstore, in-toto, TUF, the Notary Project, Harbor and the SBOM standards; §8 teaches Policy as Code from the CNCF glossary, plus Kyverno, OPA/Gatekeeper and Falco. That is CNCF-ecosystem material, D4 is 12% of the exam, and few other chapters teach it. **Add D4 to the declared objectives** or the book-close coverage report raises a phantom "D4 under-covered" finding.

---

## Retrieval-practice ledger

| Tested topic | Original chapter | Retested in |
|---|---|---|
| Cluster-scoped means *no* namespace, not *all* namespaces | ch 4 §3 | ch 12 — Bearings #1 Q3 |
| Admission is the third and last gate | ch 8 §2 | ch 12 — Bearings #2 Q5 |
| A tag is a mutable pointer; a digest is content identity | ch 2 §3 | ch 12 — Bearings #3 Q1 |
| RBAC names subjects; everything else selects | ch 4 §5 | ch 12 — Practice Q8 |
| The two axes — reachability vs workload-to-host | ch 10 §6/§7 | ch 12 — Practice Q15 |
| The admission gate as a shared position | ch 8 §2 | ch 12 — Practice Q18 |
| A signature binds to the digest | ch 2 §3 | ch 12 — Practice Q19 |
| Additive semantics, no deny rule | ch 10 §6 | ch 12 — Practice Q21 |

**Compliance: 8 of 38 graded items = 21.1%** (15 Bearings + 23 Practice), inside B3's 20–25% band and above the outline's 20% target. **Spacing floor met with room** — Ch 2 is ten chapters back and carries two items. Question inventory: 8 + 15 (3 × 5) + 23 = **46**.

**All eight tags land on material the named chapter actually owns** — I re-checked each against shipped text rather than against the tag. Practice Q15 and Q21 are genuine interleaving: each requires holding a Ch 10 fact and a Ch 12 fact at once and discriminating, which is what skill Part 10's spacing table asks for. **This is the first chapter since Ch 9 with no failed retrieval anchor** — Ch 11 carried one (Practice Q4's `[retrieval: ch4]` against material Ch 4 never deposited), and that finding is unaffected and still open.

**Soundings note.** Six of eight questions are retrieval, and the block says so and counts correctly — Q1→Ch 4 §3, Q2→Ch 5 §6, Q3→Ch 4 §4, Q4→Ch 8 §2, Q5→Ch 10 §6, Q8→Ch 2 §1, with Q6 and Q7 correctly identified in the preamble as drawing on outside professional intuition instead. Excluded from the budget per B3.

**Obligations Chapter 12 discharged — eighteen, and every pinned one landed.** Ch 2 §2 (reproducible layers → §7) · Ch 2 §3 (tags and digests → §7) · Ch 2 §6 (pull secrets as a boundary → §7) · Ch 2 §7 (sandboxed runtimes → §5, by reference) · Ch 4 §3 (the scoping boundary → §3's derivation) · Ch 4 §4 (the Secret's missing lock → §4) · Ch 4 §5 (the selector prediction → §3) · Ch 5 §6 (SA as RBAC subject → §2, partially — see L3) · Ch 6 §3 (orphaned identity → §2) · Ch 6 §8 (CRDs granted like built-ins → §3) · Ch 7 §4 (taints and affinity as isolation → §5) · Ch 8 §2 (three gates → §6; RBAC model → §3) · Ch 8 §3 (quotas as security controls → §1) · Ch 8 §7 (the etcd backup clause → §4) · Ch 10 §6 (additive semantics → §9) · Ch 10 §7 (the two axes → §5) · Ch 11 §1 (hostPath → §5; secret volumes → §4, see ⚑C) · Ch 11 §4 (access mode is not a permission system → §5).

**Forward obligations Chapter 12 creates:**

| Topic Ch 12 owns | Must be retrieved in | How |
|---|---|---|
| A *rejected* Pod versus a *failed* one; the missing-Secret startup shape; `runAsUser` as an application error in disguise | **Ch 13 §2** | The Voyage Ahead hands over three things by name. ⚠ The missing-Secret behaviour is **unsourced in this chapter's corpus** — the draft flags it and keeps the wording non-specific. **Source it before Ch 13 drafts**, since Ch 13 plans to grade on it. |
| An agent that watches a repository, as an RBAC subject with broad grants | **Ch 15 §4** | §2's fourth ServiceAccount use case plants the shape. |
| Delete-and-recreate a binding, under a system that reconciles against a repository | **Ch 15 §5** | §3's binding-immutability hazard names the consequence and defers. |
| A debug container refused by `restricted` admission | **Ch 16 §3** | §6 names it as a mid-incident surprise. |
| A policy engine **is** an admission webhook | **Ch 17 §4** | *Collects; does not redefine.* ⚑ read `pluggable-interfaces.md` first — now three live conflicts. |
| Encryption in transit as a separate decision from at rest; mTLS | **Ch 17 §5** | §4's 🔭 Closer Look draws the line deliberately for this. |
| The absent-component pattern | **Ch 13 §7, Ch 17 §7** | ⛔ **STILL BLOCKED.** Ch 12 did not touch it. Chapter 13 drafts next. |

**Open gaps carried forward, unchanged by Chapter 12:** north-south/east-west taught in Ch 10 and assessed in zero questions (open since Ch 10) · Ch 9's *"second instance"* CNI ordinal (open since Ch 11) · Ch 11's Practice Q4 retrieval anchor · CSI driver architecture taught and never assessed.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 12 additions

> ⚠ **MERGE REQUIRED BEFORE PROMOTION.** This block is a second A–Z sequence appended
> after the Chapters 10–11 alphabet above. It was appended rather than merged in place
> because merging would have required re-transcribing ~60 verbatim documentation
> definitions, and Rule 5 treats definitional drift as worse than no entry. Interleave
> the two alphabets mechanically before promoting this file to the shipped back-of-book
> glossary. No entry below duplicates an entry above.

---

## A

**ABAC (Attribute-Based Access Control)** — One of the API server's authorization
modes. *"An access control paradigm whereby access rights are granted to users through
policies which combine attributes together."*
`[source: k8s-docs-authorization-2026-08-31]` (Chapter 12 §3)

> Routed **glossary-only** by the B7 orphan doctrine, which permits Ch 12 §3 a single
> clause establishing that RBAC is *an* authorization mode rather than *the* mechanism,
> and forbids ABAC appearing as a distractor unless that clause is written. §3 writes
> the clause and uses ABAC as no distractor anywhere. Rule followed exactly.

**Additive permissions** — The defining semantic of Kubernetes RBAC. *"Permissions are
purely additive (there are no 'deny' rules)."*
`[source: k8s-docs-rbac-2026-08-23]` The effect of a subject's grants is the union of
every rule in every role bound to them; removing access means removing a grant, and no
rule can be written that subtracts. (Chapter 12 §3; argued in §9)

**Admission (Pod Security)** — see **Pod Security Admission**.

**Aggregated ClusterRole** — *"You can aggregate several ClusterRoles into one combined
ClusterRole. A controller, running as part of the cluster control plane, watches for
ClusterRole objects with an `aggregationRule` set. The `aggregationRule` defines a label
selector that the controller uses to match other ClusterRole objects that should be
combined into the `rules` field of this one."*
`[source: k8s-docs-rbac-depth-2026-08-31]` The default `admin`, `edit` and `view` roles
use aggregation, which is how a cluster administrator extends them to cover custom
resources. (Chapter 12 §3)

> A control loop — desired state as a selector, a controller reconciling toward it —
> doing a job the reader has watched it do since Ch 3 §6.

**`admin` (default ClusterRole)** — *"If used in a RoleBinding, allows read/write access
to most resources in a namespace, including the ability to create roles and role
bindings within the namespace. This role does not allow write access to resource quota
or to the namespace itself."* `[source: k8s-docs-rbac-depth-2026-08-31]`
(Chapter 12 §3)

*`admin` can delegate but cannot raise its own ceiling.*

**`allowPrivilegeEscalation`** — A `securityContext` field. *"Controls whether a process
can gain more privileges than its parent process. This bool directly controls whether
the `no_new_privs` flag gets set on the container process."*
`[source: k8s-docs-security-context-2026-08-31]` The Restricted Pod Security level
requires it to be `false`. (Chapter 12 §5)

**AppArmor** — A Linux kernel security module. *"AppArmor is a Linux kernel security
module that supplements the standard Linux user and group based permissions to confine
programs to a limited set of resources… It is configured through profiles tuned to allow
the access needed by a specific program or container, such as Linux capabilities,
network access, and file permissions. Each profile can be run in either enforcing mode,
which blocks access to disallowed resources, or complain mode, which only reports
violations."* `[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]`
(Chapter 12 §5)

> Defines resources by **file path**, where SELinux uses the inode. A node's OS
> typically ships one or the other. And note the enforcing/complain split — §6 does the
> same thing one layer up with `enforce` and `warn`.

**Attestation** — A signed claim *about* an artifact rather than a signature *on* one:
that it was built by a particular pipeline from a particular commit, that it passed a
particular test suite, that it contains a particular set of components.
(Chapter 12 §7)

> ⚠ **PROVISIONAL — the gloss is the book's, not a source's.** Both
> `in-toto-overview-2026-08-31` and `notary-project-signing-digest-2026-08-31` list
> `attestation` in `concepts_covered` and neither body defines it. The chapter's own
> AUTHOR-REVIEW flags this and asks for either a source (in-toto.io/docs, or the SLSA
> attestation spec) or an `[inferred]` marker in prose. **Do not attach a `[source:]`
> tag to this definition.**

---

## B

**Binding immutability** — *"After you create a binding, you cannot change the Role or
ClusterRole that it refers to."* `[source: k8s-docs-rbac-2026-08-23]` Retargeting means
deleting the binding and creating a new one — a different operation, with a window
during which the subject holds nothing. (Chapter 12 §3)

> ⚠ **Homonym.** This is the RBAC sense. Distinct from scheduler binding (Ch 7 §1) and
> PV/PVC binding (Ch 11 §2). Per B7 canonical forms, `RoleBinding` and
> `ClusterRoleBinding` are object names, always in code style, and are never shortened
> to "binding". Ch 12 §3 opens by disposing of the collision explicitly.

---

## C

**CEL** — The expression language Kyverno policies may be written in, alongside
declarative YAML rules. `[source: kyverno-overview-2026-08-23]`

> ⚠ **PROVISIONAL — no expansion or definition exists anywhere in the book.** Three bare
> uses in Chapter 12, **zero occurrences across Chapters 1–11**, and no row in the B7
> acronym register (register checked in full). One of the three uses is in the **Chapter
> Summary**, a revision surface. **Fix: expand on first use at §8 and add a register
> row.**

**ClusterRole** — *"A ClusterRole is a non-namespaced resource."*
`[source: k8s-docs-rbac-2026-08-23]` The documentation gives three uses: define
permissions on **namespaced** resources and grant them **within individual namespaces**;
define permissions on namespaced resources and grant them **across all namespaces**; or
define permissions on **cluster-scoped** resources.
`[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

> Two of the three documented uses concern namespaced resources. The object's name is
> actively misleading about two thirds of its job — **B1 trap #54.**

**ClusterRoleBinding** — Grants a ClusterRole's permissions to a list of subjects
**cluster-wide**. `[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

**`cluster-admin` (default ClusterRole)** — *"Allows super-user access to perform any
action on any resource."* And, decisively: *"When used in a ClusterRoleBinding, it gives
full control over every resource in the cluster and in all namespaces. When used in a
RoleBinding, it gives full control over every resource in the role binding's namespace,
including the namespace itself."* `[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

**Cosign** — Sigstore's client tool for signing and verifying artifacts, including
container images. `[source: sigstore-overview-2026-08-23]` (Chapter 12 §7)

**CVE (Common Vulnerabilities and Exposures)** — An identifier attached to a publicly
disclosed vulnerability. A scanner's job is to enumerate what an image contains and
report which components have known vulnerabilities against them. (Chapter 12 §7)

> ⚠ **PROVISIONAL — the expansion is unsourced.** No snapshot in the corpus expands CVE
> or describes the program; `k8s-docs-linux-kernel-security-constraints-2026-08-31`
> cites `CVE-2022-0185` and `CVE-2019-5736` by number only, and the CNCF glossary index
> has no entry. The B7 register carries the expansion (`term-ownership.md:669`) and the
> book's acronym convention requires it, so the chapter supplies it — correctly flagged
> in an AUTHOR-REVIEW. Research gap **G-A**: `cve.org` and `nvd.nist.gov` are
> client-rendered and return no body to automated retrieval.
>
> **Available today and not yet used:** the research manifest records two sentences
> surviving from the archived MITRE site — *"The mission of the CVE™ Program is to
> identify, define, and catalog publicly disclosed cybersecurity vulnerabilities"* and a
> statement that every CVE Record is added to the CVE List by a CVE Numbering Authority
> (CNA). Either would source this entry. **What may not be said without a further
> fetch:** a definition of "vulnerability", the `CVE-YYYY-NNNNN` ID format, or anything
> about severity scoring / CVSS.

**CycloneDX** — An SBOM standard from OWASP: *"a full-stack Bill of Materials (BOM)
standard that provides advanced supply chain capabilities for cyber risk reduction."*
`[source: sbom-standards-spdx-cyclonedx-2026-08-31]` (Chapter 12 §7)

> No B7 ledger row and no register row. The ledger's §7 grant is *"in-toto · TUF ·
> Notary"*; six further named projects and two standards arrive here unassigned.

---

## E

**`edit` (default ClusterRole)** — *"Allows read/write access to most objects in a
namespace. This role does not allow viewing or modifying roles or role bindings."*
`[source: k8s-docs-rbac-2026-08-23]` The rest of the documentation's own sentence
matters as much: *"However, this role allows accessing Secrets and running Pods as any
ServiceAccount in the namespace, so it can be used to gain the API access levels of any
ServiceAccount in the namespace."* `[source: k8s-docs-rbac-depth-2026-08-31]`
(Chapter 12 §3)

> ⚠ **`edit` *can* read Secrets.** The formal restriction is only about RBAC objects,
> and the practical ceiling is much higher than the restriction suggests. **Do not
> paraphrase this as "`edit` cannot read Secrets"** — the research manifest flagged that
> specific slide as the chapter's likeliest factual error, and the docs contradict it in
> one sentence. **B1 trap #58** is about roles and bindings only.

**Encryption at rest** — *"All of the APIs in Kubernetes that let you write persistent
API resource data support at-rest encryption."* The default is unambiguous: *"By
default, the API server stores plain-text representations of resources into etcd, with
no at-rest encryption."* `[source: k8s-docs-encrypt-data-2026-08-31]` A cluster-operator
decision made in the API server's configuration, not a field on a manifest.
(Chapter 12 §4)

> **Scope, exactly.** It protects the object as written to etcd — closing the etcd and
> etcd-backup route — and does nothing about an authorized API caller or the Pod-creation
> route. *"If you want to encrypt data in filesystems that are mounted into containers,
> you instead need to either: use a storage integration that provides encrypted volumes
> [or] encrypt the data within your own application."*
> `[source: k8s-docs-encrypt-data-2026-08-31]`

**`EncryptionConfiguration`** — The object, in the `apiserver.config.k8s.io/v1` API
group, held in the file named by the API server's `--encryption-provider-config`
argument. It names the API kinds to encrypt and an ordered list of providers. *"If you
are running the kube-apiserver without the `--encryption-provider-config` command line
argument, you do not have encryption at rest enabled."*
`[source: k8s-docs-encrypt-data-2026-08-31]` (Chapter 12 §4)

> ⚠ **A configured-looking file is not encryption.** If the provider list names
> `identity` first, nothing is encrypted — *"the default `identity` provider does not
> provide any confidentiality protection."*
> `[source: k8s-docs-encrypt-data-2026-08-31]`

**`escalate` (verb)** — The RBAC verb that lifts escalation prevention for roles. Absent
it, *"you can only create/update a role if… you already have all the permissions
contained in the role, at the same scope."*
`[source: k8s-docs-rbac-depth-2026-08-31]` The parallel verb for bindings is **`bind`**.
(Chapter 12 §3)

**Escalation prevention** — *"The RBAC API prevents users from escalating privileges by
editing roles or role bindings. Because this is enforced at the API level, it applies
even when the RBAC authorizer is not in use."*
`[source: k8s-docs-rbac-depth-2026-08-31]` (Chapter 12 §3)

**External secret store provider** — *"You can use third-party Secrets store providers
to keep your confidential data outside your cluster and then configure Pods to access
that information."* `[source: k8s-docs-secrets-good-practices-2026-08-24]` The fourth of
the four documented Secret-hardening steps. (Chapter 12 §4)

---

## F

**Falco** — *"A cloud native security tool that provides runtime security across hosts,
containers, Kubernetes, and cloud environments. It is designed to detect and alert on
abnormal behavior and potential security threats in real-time."* CNCF graduated,
originally created by Sysdig. It *"observes Linux kernel events (system calls) and data
from plugins, enriches them with metadata from the container runtime and Kubernetes,
evaluates the event stream against a rules engine, and emits real-time alerts when rules
detect violations."* `[source: falco-overview-2026-08-23]` (Chapter 12 §8)

> ★ **Falco detects; it does not prevent.** There is no step in observe → evaluate →
> alert that blocks anything. This is the single most examinable fact about it.

**The 4Cs of Cloud Native security** — *"Cloud, Clusters, Containers, and Code."* They
nest: each layer builds on the next outermost, so *"You cannot safeguard against poor
security standards in the base layers by addressing security at the Code level."*
`[source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]`
(Chapter 12 §1)

> ⚠ **Version status.** Sourced to the Kubernetes project's **archived v1.22**
> documentation. The current kubernetes.io security overview *replaced* this framing
> with the lifecycle phases. Both are taught, deliberately: **the layers answer *where*
> a control acts; the phases answer *when*.** Neither implies the other.

**Fulcio** — Sigstore's code-signing certificate authority, which issues **short-lived
certificates bound to a verified identity** rather than long-lived keys.
`[source: sigstore-overview-2026-08-23]` (Chapter 12 §7)

---

## G

**Gatekeeper** — OPA's admission controller for Kubernetes, expressing policy in the
**Rego** language. `[source: kyverno-overview-2026-08-23]` (Chapter 12 §8)

---

## H

**Harbor** — A CNCF graduated registry. Mission: *"to be the trusted cloud native
repository for Kubernetes."* It *"is an open source registry that secures artifacts with
policies and role-based access control, ensures images are scanned and free from
vulnerabilities, and signs images as trusted."*
`[source: harbor-overview-2026-08-31]` (Chapter 12 §7)

> Does scan, sign **and** restrict in one place — worth knowing when a question offers
> it as an answer.

---

## I

**Image scanning** — *"As part of an image build step, you should scan your containers
for known vulnerabilities."*
`[source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]`
(Chapter 12 §7)

> ⚠ **Deliberately thin, and the thinness is sourced-in.** No snapshot in the corpus
> describes scanning as a *practice* beyond two one-line recommendations; Harbor's page
> names *"Security and vulnerability analysis"* as a feature without describing the
> mechanism. Research gap **G22**, partially open. Scanner mechanics (SBOM-driven vs
> filesystem-walking, registry-integrated vs CI-stage) need a fetch. **A named scanner
> appeared in draft-v1's figure, was attested by no snapshot, and was removed. Do not
> reintroduce named scanners without a source.**

**Image signing** — *"Sign container images to maintain a system of trust for the content
of your containers."*
`[source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]` A scan tells you
what is *in* an image; a signature tells you *who produced it*, and the two are
independent. (Chapter 12 §7)

**in-toto** — A CNCF graduated framework. *"in-toto is designed to ensure the integrity
of a software product from initiation to end-user installation. It does so by making it
transparent to the user what steps were performed, by whom and in what order."*
`[source: in-toto-overview-2026-08-31]` (Chapter 12 §7)

> ⚠ **Bounded snapshot.** The in-toto page does not itself use the word *provenance*
> (its own snapshot records this), and it warns that supply-chain layout, link metadata,
> and steps/inspections are **not** covered there and must not be described. The
> equation between *what steps, by whom, in what order* and *provenance* is carried by
> the SPDX tag; the chapter's AUTHOR-REVIEW asks the author to confirm that split.

---

## K

**Keyless signing** — Sigstore's flow, which removes the long-lived private key from the
problem: a Cosign client creates an **ephemeral** key pair and requests a certificate
from Fulcio using an OpenID Connect identity token; Fulcio validates the token and issues
a short-lived certificate linking the public key to the verified identity; the artifact
is signed; **the private key is discarded after a single signing**; and the signature and
certificate are recorded in Rekor. `[source: sigstore-overview-2026-08-23]`
(Chapter 12 §7)

*The key exists for seconds. What persists is a certificate binding a public key to an
identity, and a log entry proving when. There is no long-lived secret to steal.*

**Kubewarden** — A third-party policy engine, named alongside Kyverno and OPA Gatekeeper
as an option for enforcing the Pod Security Standards.
`[source: k8s-docs-pod-security-standards-profiles-2026-08-31]`

> ⚠ **PROVISIONAL — named once inside a sourced list and never glossed.** No B7 ledger
> row, no register row, zero occurrences in Chapters 1–11. **Fix: one clause at §8, or
> drop the name and cite the two engines the chapter actually teaches.**

**Kyverno** — Greek for *"govern."* *"A cloud native policy engine"* originally built for
Kubernetes and now usable outside clusters as a unified policy language; it *"allows
platform engineers to automate security, compliance, and best practices validation and
deliver secure self-service to application teams."* Policies can *"validate, mutate,
generate, or clean up Kubernetes resources; verify container images and metadata for
software supply chain security; and be applied as a Kubernetes admission controller
(webhook) or as a CLI-based scanner."* Written in YAML using declarative rules and CEL,
managed as Kubernetes resources, version-controlled with Git.
`[source: kyverno-overview-2026-08-23]` (Chapter 12 §8)

> ⚠ **The four verbs are listed by the source and defined by none of it.** The chapter's
> glosses — validate = refuse; mutate = change in passing; generate = create other
> objects in response; clean up = remove objects meeting a condition — are the author's
> reading of standard policy-engine semantics. Flagged in an AUTHOR-REVIEW. **Either
> source them from `kyverno.io/docs/policy-types/` or mark them `[inferred]` in prose.**

---

## L

**Least privilege (RBAC)** — *"Kubernetes RBAC is a key security control to ensure that
cluster users and workloads have only the access to resources required to execute their
roles."* `[source: k8s-docs-rbac-good-practices-2026-08-31]` The documentation's general
rules: assign permissions at the namespace level where possible; avoid wildcard
permissions, since *"providing wildcard access gives rights not just to all object types
that currently exist in the cluster, but also to all object types which are created in
the future"*; do not use `cluster-admin` except where specifically needed; and avoid
adding users to `system:masters`. (Chapter 12 §3)

**Linux capabilities** — *"With Linux capabilities, you can grant certain privileges to a
process without granting all the privileges of the root user."*
`[source: k8s-docs-security-context-2026-08-31]` (Chapter 12 §5)

> ⚠ **Syntax trap, and it catches everyone once.** *"Linux capability constants have the
> form `CAP_XXX`. But when you list capabilities in your container manifest, you must
> omit the `CAP_` portion of the constant. For example, to add `CAP_SYS_TIME`, include
> `SYS_TIME` in your list of capabilities."*
> `[source: k8s-docs-security-context-2026-08-31]`

---

## N

**Node (authorization mode)** — *"A special-purpose authorization mode that grants
permissions to kubelets based on the pods they are scheduled to run."*
`[source: k8s-docs-authorization-2026-08-31]` (Chapter 12 §3)

**Notary Project** — *"A set of specifications and tools intended to provide a
cross-industry standard for securing software supply chains,"* focused on *"signing and
validating software artifacts, ensure they have not been tampered with and provide
security policies to determine which validated artifacts are allowed to be used in your
systems."* CNCF incubating; **Notation** is its CLI.
`[source: notary-project-signing-digest-2026-08-31]` (Chapter 12 §7)

> ★ The source of the chapter's Fixed Point: *"Notation resolves the tag to the digest
> before signing if a tag is used to identify the container image,"* and *"Always
> reference and use the image digest instead of a tag since digest is immutable."*
> `[source: notary-project-signing-digest-2026-08-31]`
>
> ⚑ **B7 says "Notary"; the project's own page says "Notary Project," with "Notation"
> as the tool.** The canonical form needs a ruling. Chapter 12 uses *Notary Project* and
> *Notation*, which matches the source.

---

## O

**OPA (Open Policy Agent)** — A CNCF graduated policy engine, with the **Gatekeeper**
admission controller for Kubernetes, expressing policy in the **Rego** language.
`[source: kyverno-overview-2026-08-23]` (Chapter 12 §8)

**OWASP** — The steward of the CycloneDX SBOM standard.
`[source: sbom-standards-spdx-cyclonedx-2026-08-31]`

> ⚠ **PROVISIONAL — no expansion in the book.** One bare use in Chapter 12, zero in
> Chapters 1–11, no register row. **Fix: expand on first use at §7 and add a register
> row.**

---

## P

**Pod Security Admission (PSA)** — *"Kubernetes offers a built-in Pod Security admission
controller to enforce the Pod Security Standards."* Stable since Kubernetes v1.25.
`[source: k8s-docs-pod-security-admission-2026-08-31]` It applies a policy **per
namespace** via labels of the form `pod-security.kubernetes.io/<MODE>: <LEVEL>`, where
MODE is **`enforce`** (violations are rejected), **`audit`** (violations are recorded in
the audit log), or **`warn`** (violations trigger a user-facing warning).
`[source: k8s-docs-pod-security-standards-2026-08-23]` (Chapter 12 §6)

> ★ **The level says *what* is checked; the mode says *what happens* when the check
> fails. Independent axes.** An option describing `enforce` as a level, or `restricted`
> as a mode, is wrong at the grammar before you reach the meaning.
>
> ⚑ **Single point of failure.** `pod-security.kubernetes.io` appears **once** in the
> entire 168-snapshot corpus — the one sentence cited above. The PSA snapshot is
> truncated and contains no label text. Six reader-facing sites and three graded items
> rest on that line. **Re-fetch the PSA page in full.**

**Pod Security Standards (PSS)** — Three policies covering the security spectrum,
**cumulative**, ranging from highly permissive to highly restrictive.
`[source: k8s-docs-pod-security-standards-2026-08-23]`

| Profile | Description |
|---|---|
| **Privileged** | *"Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations."* |
| **Baseline** | *"Minimally restrictive policy which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration."* |
| **Restricted** | *"Heavily restricted policy, following current Pod hardening best practices."* |

`[source: k8s-docs-pod-security-standards-2026-08-23]` (Chapter 12 §6)

> **Baseline admits a Pod with no `securityContext` at all**; Restricted does not, because
> it requires `runAsNonRoot: true`, `allowPrivilegeEscalation: false`, capabilities
> dropping `ALL`, and an explicit `RuntimeDefault` or `Localhost` seccomp profile.
> `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` That difference is the
> most productive distractor pair in the chapter.
>
> There is no fourth level: *"Privileges required above the Baseline policy are typically
> very application specific, so we do not offer a standard profile in this niche."*
> `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]`

**PodSecurityPolicy (PSP)** — The predecessor to Pod Security Admission, which supersedes
it. Not the mechanism a current cluster uses, which makes its **absence** the load-bearing
fact: offered as a current mechanism in a question, it is the distractor.
(Chapter 12 §6)

> ⚑ **CONFLICT OPEN — do not assert a version.** The B7 register row and the ledger's
> orphan routing both say **"removed in 1.25."** No snapshot in the corpus contains a
> removal sentence — the PSA snapshot declares `podsecuritypolicy-removed` in its
> frontmatter and its body is truncated before any PSP text (verified). Research gap
> **G-H**. Chapter 12 says only *"superseded"*, correctly, and softened its Exam Alert
> trap row to match. **Reconcile the chapter, the trap row, the ledger and the register
> together** when `kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/`
> or the v1.25 release notes are fetched.

**Policy as Code** — *"Policy as Code is the practice of storing the definition of
policies as one or more files in machine-readable and processable form."* Codified policy
gets consistent automated enforcement instead of manual review, and — because the files
live in version control — a change history you can audit and revert.
`[source: cncf-glossary-policy-as-code-2026-08-31]` (Chapter 12 §8)

**Policy Controller (Sigstore)** — *"Enforces signature verification policies within
Kubernetes"*, as an admission controller.
`[source: sigstore-overview-2026-08-23]` (Chapter 12 §7, §8)

**Policy engine** — A tool that answers **arbitrary** policy questions at the admission
gate, where Pod Security Admission answers a fixed one. Kyverno and OPA Gatekeeper are
the two the chapter teaches. (Chapter 12 §8)

> The Pod Security Standards page draws the framing worth keeping: *"Decoupling policy
> definition from policy instantiation allows for a common understanding and consistent
> language of policies across clusters, independent of the underlying enforcement
> mechanism."* `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` The
> Standards are a *definition*; PSA and the policy engines are *instantiations*.

**`privileged: true`** — *"Any container in a Pod can enable Privileged mode if you set
the `privileged: true` field in the `securityContext` field for the container."* What it
does: *"Privileged containers override or undo many other hardening settings such as the
applied seccomp profile, AppArmor profile, or SELinux constraints. Privileged containers
are given all Linux capabilities, including capabilities that they don't require."*
Specifically, they run as the `Unconfined` seccomp profile, ignore applied AppArmor
profiles, and run as the `unconfined_t` SELinux domain.
`[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]` (Chapter 12 §5)

> ★ **Not one more setting alongside the others — the setting that turns the others
> off.** And a consequence belonging as much to §4: **a container running with
> `privileged: true` can access all Secrets on that node.**
> `[source: k8s-docs-secret-risks-2026-08-31]` Not its namespace's. The node's.

**Provenance** — The verifiable record of how an artifact came to be, not merely what it
is. SPDX names it directly, listing *"Provenance and Integrity: Tracking the origin and
history of components, including checksums and cryptographic hashes"* among what its
standard covers. `[source: sbom-standards-spdx-cyclonedx-2026-08-31]` (Chapter 12 §7)

---

## R

**RBAC (Role-Based Access Control)** — An API-server authorization mode that *"regulates
access based on the roles of individual users within an enterprise."*
`[source: k8s-docs-authorization-2026-08-31]` It uses the `rbac.authorization.k8s.io` API
group *"to drive authorization decisions, allowing you to dynamically configure policies
through the Kubernetes API."* Four object kinds: **Role, ClusterRole, RoleBinding and
ClusterRoleBinding.** `[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

> ⚠ **Acronym-binding defect — narrower than first reported, and still real.** The
> acronym's **first use in the book is bare**, at `chapter-04:646`, inside a sourced
> quotation. The expansion arrives 193 lines later at `chapter-04:839`, in sentence case
> (*"Role-based access control"*), adjacent to a second bare use — so the book does bind
> them, by proximity, in the wrong chapter and the wrong casing. **Ch 12 §3, the B7
> owner, never expands it at all** (~80 bare uses). B7 flag ⚑7 anticipated this.
> **Fix: one clause at §3, in the register's casing.**

**RBAC is *an* authorization mode, not *the* mechanism** — *"All parts of an API request
must be allowed by some authorization mechanism in order to proceed,"* and *"[each
authorizer] is checked in sequence. If any authorizer approves or denies a request, that
decision is immediately returned and no other authorizer is consulted. If all modules
have no opinion on the request, then the request is denied."* The modules include
**Node**, **ABAC**, **RBAC** and **Webhook**.
`[source: k8s-docs-authorization-2026-08-31]` (Chapter 12 §3)

**Rego** — OPA's purpose-built policy language, the counterpart to Kyverno's YAML and CEL.
`[source: kyverno-overview-2026-08-23]` (Chapter 12 §8)

*The practical difference at KCNA depth: a language-and-ecosystem choice, not a
security-model choice. Both sit at the admission gate.*

**Rekor** — Sigstore's *"immutable, append-only transparency log that records signing
events for public audit and verification."*
`[source: sigstore-overview-2026-08-23]` (Chapter 12 §7)

> Append-only means entries are never removed, altered or superseded — which is what
> makes *"was this signed, by whom, and when?"* answerable for artifacts signed with keys
> that no longer exist. Under keyless signing, that is all of them.

**Rekor is not a freshness check.** Practice Q23 option D is built on the assumption that
it is.

**`readOnlyRootFilesystem`** — A `securityContext` field. *"Mounts the container's root
filesystem as read-only."* `[source: k8s-docs-security-context-2026-08-31]`
(Chapter 12 §5)

> ⚠ Not required by the Restricted level
> `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` — Practice Q4 in
> Bearings #3 exists to reject that assumption.

**`resourceNames`** — *"You can also refer to resources by name for certain requests
through the `resourceNames` list. When specified, requests can be restricted to
individual instances of a resource."* With limits: *"You cannot restrict deletecollection
or top-level create requests by resource name. For create, this limitation is because the
name of the new object may not be known at authorization time."*
`[source: k8s-docs-rbac-depth-2026-08-31]` (Chapter 12 §3)

**Role** — *"A Role always sets permissions within a particular namespace; when you
create a Role, you have to specify the namespace it belongs in."*
`[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

**RoleBinding** — *"A RoleBinding grants the permissions defined in a role to a user or
set of users… within a specific namespace."* And the sentence that does the work: *"A
RoleBinding may reference any Role in the same namespace. Alternatively, a RoleBinding
can reference a ClusterRole and bind that ClusterRole to the namespace of the
RoleBinding."* `[source: k8s-docs-rbac-2026-08-23]` (Chapter 12 §3)

> ★ **The binding determines the scope of the grant.** Including for `cluster-admin`,
> which is where it trips people. **B1 trap #55.**

**`runAsGroup`** — Specifies the primary group ID for all processes in the Pod's
containers. *"If this field is omitted, the primary group ID of the containers will be
root(0)."* `[source: k8s-docs-security-context-2026-08-31]` (Chapter 12 §5)

**`runAsNonRoot`** — Requires that containers not run as the root user. The documentation
recommends it generally — *"Unless necessary, run Linux workloads as non-root by setting
specific user and group IDs in your Pod manifest and by specifying `runAsNonRoot:
true`"* `[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]` — and the
Restricted level mandates it.
`[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` (Chapter 12 §5)

**`runAsUser`** — Specifies that all processes in a Pod's containers run with a given user
ID. `[source: k8s-docs-security-context-2026-08-31]` (Chapter 12 §5)

> ⚠ *"Ensure that the user or group that you assign to the workload has the permissions
> required for the application to function correctly. Changing the user or group to one
> that doesn't have the correct permissions could lead to file access issues or failed
> operations."*
> `[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]` Handed forward to
> **Ch 13 §2** as a permissions failure wearing an application error's clothing.

---

## S

**SBOM (Software Bill of Materials)** — A standardized record of what a software artifact
is made of. The two dominant standards are **SPDX** and **CycloneDX**.
(Chapter 12 §7)

> ⚠ **PROVISIONAL — no source in the corpus defines an SBOM in one canonical sentence.**
> The description above is assembled from what SPDX and CycloneDX say their standards
> *cover*, which is defensible but is not a quoted definition. CISA and NTIA both
> returned HTTP 403 to automated retrieval on 2026-08-31; the CNCF glossary has no entry
> (index verified). Research gap **G-B**. **Do not attach a definition-shaped `[source:]`
> tag to this entry.**
>
> An SBOM is itself a signable artifact — Sigstore names SBOMs explicitly among the types
> it handles `[source: sigstore-overview-2026-08-23]`.
>
> *Trimmed from draft-v1 per the curriculum-alignment finding that §7 was over-covered
> relative to its recognition-depth allocation:* the ISO/IEC 5962:2021 and ECMA-424
> standardization details. Both remain sourced in
> `sbom-standards-spdx-cyclonedx-2026-08-31` if the author wants them restored.

**seccomp** — *"Each capability has a set of system calls (syscalls) that a process can
make. seccomp lets you restrict these individual syscalls. It can be used to sandbox the
privileges of a process, restricting the calls it is able to make from userspace into the
kernel."* In the manifest: `seccompProfile` with a `type` of `RuntimeDefault`,
`Unconfined`, or `Localhost`.
`[source: k8s-docs-linux-kernel-security-constraints-2026-08-31;
k8s-docs-security-context-2026-08-31]` (Chapter 12 §5)

> The documentation's own advice on custom profiles is blunt: *"seccomp is a low-level
> security configuration that you should only configure yourself if you require
> fine-grained control over Linux syscalls… Use the default seccomp profile that's
> bundled with your container runtime. If you need a more isolated environment, consider
> using a sandbox, such as gVisor."*
> `[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]`

**Secret exposure paths** — Three, and the third is the one nobody counts as a permission
to read secrets. *"Kubernetes Secrets are, by default, stored unencrypted in the API
server's underlying data store (etcd). Anyone with API access can retrieve or modify a
Secret, and so can anyone with access to etcd. Additionally, anyone who is authorized to
create a Pod in a namespace can use that access to read any Secret in that namespace;
this includes indirect access such as the ability to create a Deployment."*
`[source: k8s-docs-secret-2026-08-23]` (Chapter 12 §4)

> Broader than `get`: *"`list` and `watch` access also effectively allow for users to
> reveal the Secret contents."*
> `[source: k8s-docs-rbac-good-practices-2026-08-31]`
>
> ★ And the design conclusion the documentation draws: *"namespaces should be used to
> separate resources requiring different levels of trust or tenancy… **boundaries within
> a namespace should be considered weak**."*
> `[source: k8s-docs-rbac-good-practices-2026-08-31]` **B1 trap #61.**

**Secret hardening steps** — *"In order to safely use Secrets, take at least the following
steps: enable Encryption at Rest for Secrets; enable or configure RBAC rules with
least-privilege access to Secrets; restrict Secret access to specific containers; consider
using external Secret store providers."*
`[source: k8s-docs-secret-2026-08-23]` (Chapter 12 §4 — closing the four Ch 4 §4 deferred)

**Secret types** — `Opaque` (arbitrary user-defined data, the default) ·
`kubernetes.io/service-account-token` (**legacy** long-lived credential) ·
`kubernetes.io/dockercfg` · `kubernetes.io/dockerconfigjson` (a serialized
`~/.docker/config.json`, which is what an `imagePullSecrets` entry carries) ·
`kubernetes.io/basic-auth` · `kubernetes.io/ssh-auth` · `kubernetes.io/tls` ·
`bootstrap.kubernetes.io/token`. `[source: k8s-docs-secret-2026-08-23]`
(Chapter 12 §4)

**Secrets Store CSI Driver** — *"A DaemonSet that lets the kubelet retrieve Secrets from
external stores, and mount the Secrets as a volume into specific Pods that you authorize
to access the data."* `[source: k8s-docs-secrets-good-practices-2026-08-24]`
(Chapter 12 §4)

**`securityContext`** — *"A security context defines privilege and access control settings
for a Pod or Container."* `[source: k8s-docs-security-context-2026-08-31]`
(Chapter 12 §5)

> ★ **Two scopes, and the container's wins.** *"The security settings that you specify
> for a Pod apply to all Containers in the Pod."* But *"Security settings that you
> specify for a Container apply only to the individual Container, and they override
> settings made at the Pod level when there is overlap. Container settings do not affect
> the Pod's Volumes."* `[source: k8s-docs-security-context-2026-08-31]`
>
> ★ **`securityContext` governs the workload-to-host axis; NetworkPolicy governs the
> workload-to-workload axis.** Separate systems, separate objects, separate layers. They
> fail independently and neither substitutes for the other. Closes the two axes Ch 10 §7
> drew.

**SELinux** — A Linux security module in which objects are assigned security labels.
*"AppArmor uses profiles to define access to resources. SELinux uses policies that apply
to specific labels,"* and *"In AppArmor, you define resources using file paths. SELinux
uses the index node (inode) of a resource to identify the resource."*
`[source: k8s-docs-linux-kernel-security-constraints-2026-08-31]` (Chapter 12 §5)

**ServiceAccount** — *"A type of non-human account that provides a distinct identity in a
Kubernetes cluster."* Application Pods, system components, and entities inside and outside
the cluster can use a ServiceAccount's credentials to identify as it. **Namespaced**;
every namespace gets a `default` on creation.
`[source: k8s-docs-service-accounts-2026-08-23]`

> **Definition home is Ch 5 §6** per B7; logged here because Ch 12 §2 states it and
> because §2 owns the RBAC-subject sense. Backfill should reconcile the two.
>
> ★ *"The default service accounts in each namespace get no permissions by default other
> than the default API discovery permissions that Kubernetes grants to all authenticated
> principals if RBAC is enabled."*
> `[source: k8s-docs-service-accounts-2026-08-23]` **Identity and permission are two
> different things kept in two different objects, and the `default` ServiceAccount is the
> proof.**

**Service account token** — *"In Kubernetes v1.22 and later, Kubernetes gets a
short-lived, automatically rotating token using the TokenRequest API and mounts the token
as a projected volume."* **Not** recommended: long-lived ServiceAccount token Secrets,
which *"don't expire or rotate and pose a security risk."*
`[source: k8s-docs-service-accounts-2026-08-23]` (Chapter 12 §2) **B1 trap #62.**

**Sigstore** — A free, public-good service under the Open Source Security Foundation that
*"empowers software developers and consumers to securely sign and verify software
artifacts such as release files, container images, binaries, software bills of materials
(SBOMs), and more."* Components: **Cosign**, **Fulcio**, **Rekor**, **Policy
Controller**. `[source: sigstore-overview-2026-08-23]` (Chapter 12 §7)

**SPDX** — An SBOM standard from the Linux Foundation: *"an open standard designed to
facilitate the communication of Bill of Materials (BOM) information across diverse
domains, including software, artificial intelligence (AI), datasets, and system
components,"* covering metadata for packages, files and snippets, licensing information,
and provenance and integrity.
`[source: sbom-standards-spdx-cyclonedx-2026-08-31]` (Chapter 12 §7)

> ⚠ **PROVISIONAL on the acronym only** — the function is sourced, the expansion is
> nowhere in the book. No register row. Zero occurrences in Chapters 1–11.

**Subject (RBAC)** — What a grant is made to. *"A RoleBinding or ClusterRoleBinding binds
a role to subjects. Subjects can be group, users or ServiceAccounts."* Each is identified
by a **literal string**. `[source: k8s-docs-rbac-depth-2026-08-31]` (Chapter 12 §3;
B7 assigns the term to §2 — see the note below)

> ★ **Subjects are named, not selected.** There is no `subjectSelector`; you cannot write
> "everything labeled `team=payments`." This is the exception `chapter-04:839` warned
> would produce *"a specific, confident, wrong prediction in Chapter 12"*, and §3 pays it
> off. **The *why* is the author's reading, not documentation** — a grant defined by
> selector would silently expand when someone added a label, and adding a label is one of
> the lowest-privilege operations in the system. Research gap **G-D** confirms no source
> explains the choice.
>
> ⚑ **B7 assigns *subject* to Ch 12 §2; §3 defines it.** §2 uses the word once
> (*"is a subject exactly like any Pod is a subject"*) before it is defined, and shipped
> `chapter-05:779` sends readers to §2 for it. One clause in §2 closes all three.

**`system:masters`** — A group whose membership *"bypasses all RBAC rights checks and will
always have unrestricted superuser access, which cannot be revoked by removing
RoleBindings or ClusterRoleBindings."* If the cluster uses an authorization webhook,
requests from its members are never sent to it.
`[source: k8s-docs-rbac-good-practices-2026-08-31]` (Chapter 12 §3)

> ★ **Not an RBAC grant**, so removing RBAC objects removes nothing — and it is invisible
> to any audit that reads RBAC objects. Graded at Practice Q3.

---

## T

**TokenRequest API** — The current mechanism by which a Pod obtains ServiceAccount
credentials: short-lived, automatically rotating, delivered as a projected volume.
`[source: k8s-docs-service-accounts-2026-08-23]` (Chapter 12 §2)

**TokenReview** — The API that **validates** a token somebody has presented, as against
`TokenRequest`, which **issues** one. (Chapter 12, Practice Q4 answer)

> ⚠ **PROVISIONAL — defined only inside a distractor explanation.** A term a reader first
> meets in an answer key has no place to look it up mid-question, which is the situation
> B7's orphan doctrine exists to prevent. **Fix: one clause in §2, or accept the glossary
> row as the lookup path and record the exception.**

**Transparency log** — An append-only record of signing events, held so that *"was this
artifact signed, by whom, and when?"* has a durable answer. **Rekor** is Sigstore's.
`[source: sigstore-overview-2026-08-23]` (Chapter 12 §7)

**TUF (The Update Framework)** — A CNCF graduated *"framework for securing software update
systems"* that *"maintains the security of software update systems, providing protection
even against attackers that compromise the repository or signing keys."*
`[source: tuf-overview-2026-08-31]` (Chapter 12 §7)

> ★ **Every attack TUF names involves a *correctly signed* artifact** — a file frozen so
> you never see an update; an older insecure version presented as newer; a newer file
> that is not the newest; a compromised signing key producing properly signed malice.
> `[source: tuf-overview-2026-08-31]` Signing answers *did this come from who I think?*
> and answers nothing about freshness, ordering, or key compromise. Graded at
> Practice Q23.

---

## U

**User account / group (Kubernetes)** — Not Kubernetes objects. Service accounts are
*"different from user accounts, which are authenticated human users in the cluster,"* and
*"by default, user accounts don't exist in the Kubernetes API server."*
`[source: k8s-docs-service-accounts-2026-08-23]` Usernames are strings the authenticator
produces, and *"it is up to you as a cluster administrator to configure the authentication
modules so that authentication produces usernames in the format you want."* Groups
likewise; the `system:` prefix is reserved.
`[source: k8s-docs-rbac-depth-2026-08-31]` (Chapter 12 §2)

> In-cluster identities are objects; human identities are not. Human identity is somebody
> else's system.
>
> ⚑ **The corpus has no snapshot covering Kubernetes authentication mechanisms** — X.509
> client certificates, OIDC token authentication, authenticating proxies. §2 says only
> *"from outside the cluster"*, which is what the corpus supports. **B7 assigns `JWT` and
> `OIDC` to Ch 12 §2 and neither reaches the reader** — see the manifest's ⚑A.

---

## V

**`view` (default ClusterRole)** — *"Allows read-only access to see most objects in a
namespace. It does not allow viewing roles or role bindings. This role does not allow
viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount
credentials in the namespace, which would allow API access as any ServiceAccount in the
namespace (a form of privilege escalation)."*
`[source: k8s-docs-rbac-depth-2026-08-31]` (Chapter 12 §3) **B1 trap #57.**

*The stated reason is the useful part: Kubernetes treats "can read Secrets" and "can act
as anybody in this namespace" as nearly the same permission.*

---

## W

**Webhook (authorization mode)** — An authorization module that *"makes a synchronous HTTP
callout, blocking the request until the remote service responds."*
`[source: k8s-docs-authorization-2026-08-31]` (Chapter 12 §3)

> Distinct from an **admission** webhook (Ch 8 §2 / Ch 12 §8), which runs at the third
> gate. Practice Q18 option D exists to reject the conflation.

---

*Stage 14 · Chapter 12 · 2026-08-31. Nine entries provisional pending chapter-side or
research-side fixes recorded in the Chapter 12 KB manifest.*
=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/security-maps-phases-and-4cs.md ===
# Concept — Two maps: lifecycle phases and the 4Cs

**Definition home:** Ch 12 §1 · **Objective:** D2.2, with substantial D4 content
**Closes research gap G6** (the 4Cs were entirely absent from the corpus)
**Figure:** `ch12-fig01-4cs-and-lifecycle-phases`
**Sources:** `k8s-docs-cloud-native-security-2026-08-23`,
`k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31`

---

## Why two maps and not one

> ★ **The phases answer *when* a control acts. The layers answer *where* it acts.**
> Every control has a position on both. A question that appears to be about one is
> frequently about the other.

That sentence is the section's whole payload; the two lists are scaffolding for it.

| Control | Phase | Layer |
|---|---|---|
| RBAC | runtime / access | Cluster |
| ServiceAccount | runtime / access | Cluster |
| `securityContext` | runtime / compute | Container |
| encryption at rest | runtime / storage | Cloud → Cluster |
| image signing | distribute | Container |

Neither coordinate implies the other, and Bearings #1 Q1 is built on exactly that: its
distractors get the phase right and the layer wrong, and the layer half-right and the
phase wrong.

## The phases — develop, distribute, deploy, runtime

`[source: k8s-docs-cloud-native-security-2026-08-23]`

**Runtime splits three ways — access, compute, storage — and that split is the chapter's
table of contents.** Access → §2, §3. Compute → §5, §6. Storage → §4.

Two objects show up in a new role in the compute list, and the recognition is the point:
**ResourceQuota and LimitRange** were fairness controls at Ch 8 §3 and are security
controls here, because a workload that can exhaust a node affects every other workload on
it. Likewise *"partition workloads across different nodes to improve isolation"* is
Ch 7 §4's node selection, doing a second job.

**Nothing in the *develop* phase is a Kubernetes object.** That is the point of having
the phase, and it should not be quietly dropped in a later restatement.

## The layers — Cloud ⊃ Cluster ⊃ Container ⊃ Code

`[source: k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31]`

They nest, and the consequence is stated bluntly by the source: *"You cannot safeguard
against poor security standards in the base layers by addressing security at the Code
level."*

**Cloud** is the trusted computing base — *"If the Cloud layer is vulnerable (or
configured in a vulnerable way) then there is no guarantee that the components built on
top of this base are secure."* It carries the etcd recommendation §4 needs: the disk
*"especially should be encrypted at rest, since etcd holds the state of the entire cluster
(including Secrets)."*

## ⚠ Version status — preserve the disclosure

The 4Cs are sourced to the Kubernetes project's **archived v1.22** documentation. The
current kubernetes.io security overview **replaced** this framing with the lifecycle
phases. The chapter discloses this in a short "Why both" passage and does not pretend the
4Cs are current guidance; it argues they remain useful because they answer a question the
phases do not, and because third-party material still uses them.

**Any later chapter restating the 4Cs must carry the version disclosure.** Dropping it
turns an honest editorial choice into a factual error.

## Constraints on later chapters

- **Ch 17 §4** (extension points) and **Ch 17 §5** (service mesh) both sit on this map.
  Refer to the coordinates; do not redraw the maps.
- The **deploy** phase — *"restrictions on what can be deployed, who can deploy it, and
  where it can go"* — is GitOps described before the reader has the word. **Ch 15** should
  collect that, and §1 already points at it.
- ⚑ **This section is a large part of the chapter's undeclared D4 content.** See
  `objective-coverage.md`.

## See also

[[supply-chain-security]] · [[securitycontext]] · [[secret-exposure-and-hardening]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccounts-and-identity.md ===
# Concept — ServiceAccounts: identity is not permission

**Definition home:** Ch 5 §6 (the object) · **Ch 12 §2 (the RBAC-subject sense)**
**Objective:** D2.2 — **closes research gap G7**
**Figure:** `ch12-fig03-serviceaccount-token-flow`
**Sources:** `k8s-docs-service-accounts-2026-08-23`, `k8s-docs-rbac-depth-2026-08-31`,
`k8s-docs-garbage-collection-2026-08-24`

---

## The Fixed Point, and why it comes before RBAC

> ★ **An identity and a permission are two different things, kept in two different
> objects.** The `default` ServiceAccount is the proof: every Pod in the cluster has an
> identity, and almost none of them can do anything with it.

*"The default service accounts in each namespace get no permissions by default other than
the default API discovery permissions that Kubernetes grants to all authenticated
principals if RBAC is enabled."*

**This is why §2 precedes §3 rather than merging with it.** Creating a ServiceAccount
grants nothing; assigning it to a Pod grants nothing. The Pod authenticates successfully,
reaches the second gate, and is refused — a completely different failure from not being
recognized at all, and one that produces a different message. Bearings #1 Q2 is this
Fixed Point in question form, and its distractor C is the real-world misdiagnosis: seeing
a 403 and going to look at the token.

The figure draws it by leaving the authorization box deliberately **empty**.

## The asymmetry worth keeping

*"Service accounts are different from user accounts, which are authenticated human users
in the cluster,"* and *"by default, user accounts don't exist in the Kubernetes API
server."*

**In-cluster identities are objects; human identities are not.** Kubernetes validates an
external claim, extracts a username and groups as strings, and stores nothing. That is
why ServiceAccounts get a section and users get a paragraph.

⚑ **The corpus has no snapshot on authentication *mechanisms*** — X.509, OIDC tokens,
authenticating proxies — so §2 says only *"from outside the cluster."* Correct given the
sources, and it leaves two B7 rows (`JWT`, `OIDC`, both assigned to Ch 12 §2)
undischarged. See the Ch 12 manifest ⚑A.

## The credential

TokenRequest, short-lived, automatically rotating, delivered by a **projected volume** —
the mechanism the reader already used, unnamed, at Ch 5 §6 and met by name at Ch 11 §1.

🪝 **The distractor to expect:** a Secret of type `kubernetes.io/service-account-token`
looks like the current mechanism and is the legacy one — a credential in etcd that
neither expires nor rotates. **B1 trap #62.** Nothing durable is created by the current
path.

## Identity outlives the workload

Deleting a Deployment removes what it owns. It does **not** remove the ServiceAccount its
Pods ran as, the Secrets it referenced, or the RoleBindings that granted it anything —
none of them carries an owner reference back to the Deployment.

**This closes `chapter-06:486`.** Research gap **G-F** records that no source states it in
these words; the chapter derives it from garbage-collection semantics with the pointer
back to Ch 6, which is what the gap recommended. **Do not upgrade the derivation to a
sourced claim.**

> The consequence is entropy, not an exotic attack: a three-year-old cluster accumulates
> identities nobody remembers creating, still holding grants nobody remembers making, and
> nobody deletes them because nobody is certain what would break.

## Constraints on later chapters

- **Ch 15 §4** inherits the fourth documented use case — an external agent (CI/CD, or a
  reconciler) is a subject exactly like a Pod, with grants that tend to be broad because
  its job is broad. §2 plants the shape deliberately.
- ⚑ **`subject` is used in §2 once before §3 defines it**, and B7 assigns the term to §2.
  One clause after the Fixed Point closes it and lands shipped `chapter-05:779`'s pointer.

## See also

[[rbac]] · [[secret-exposure-and-hardening]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/rbac.md ===
# Concept — RBAC: four objects, one derivation

**Definition home:** Ch 12 §3 · **Objective:** D2.2 — the chapter's densest section
**Figure:** `ch12-fig02-rbac-four-way-matrix`
**Carries B1 traps #53–#59** — seven of the ten D2.2 RBAC/Secret traps.
**Sources:** `k8s-docs-rbac-2026-08-23`, `k8s-docs-rbac-depth-2026-08-31`,
`k8s-docs-authorization-2026-08-31`, `k8s-docs-rbac-good-practices-2026-08-31`

---

## Teach the derivation, not the table

The four-way matrix is the classic memorization target and **B1 trap #55**. The chapter
refuses to present it as a table to memorize, on instruction from Ch 4 and Ch 8, and
derives it from one thing the reader already has.

**Start from the boundary (Ch 4 §3): a cluster-scoped resource belongs to *no* namespace,
not to all of them.** Put that beside two sourced sentences — *"A Role always sets
permissions within a particular namespace"* and *"ClusterRole, by contrast, is a
non-namespaced resource"* — and ask two **independent** questions:

1. **What does the permission cover?** Namespaced resources → a Role can hold the rules.
   Any cluster-scoped resource → a Role has nowhere to put the rule, so a **ClusterRole is
   forced**. Not by convention; by the structure of what a Role is.
2. **Where should the grant apply?** One namespace → **RoleBinding**. Everywhere →
   **ClusterRoleBinding**.

Two independent questions is why there are four objects rather than two, and the
combination that surprises people — a ClusterRole bound by a RoleBinding — falls out
immediately.

> ★ **The binding determines the scope of the grant.**

**The test of whether a reader has the derivation:** cover the bottom of the figure and
rebuild it from the top. The chapter says so explicitly.

⚑ **One step in the derivation is unsourced.** That a cluster-scoped rule *has nowhere to
land* when a ClusterRole is bound by a RoleBinding follows from the two quoted sentences
but is stated outright by no page in the corpus. **Four reader-facing sites rest on it**:
the §3 paragraph, the figure's fourth row, Bearings #1 answer 3, and Practice Q5's
option-B explanation. The chapter flags this in an AUTHOR-REVIEW. **If it cannot be
confirmed, all four need softening together, not individually.**

## RBAC is *an* authorization mode

*"All parts of an API request must be allowed by some authorization mechanism in order to
proceed,"* and the modules — Node, ABAC, RBAC, Webhook — are *"checked in sequence… If all
modules have no opinion on the request, then the request is denied."*

One clause is all ABAC gets in this book, and the B7 orphan doctrine licenses exactly
that clause and forbids ABAC as a distractor without it. **Rule followed; do not extend
it.**

## The default roles, taught as negative space

What each **cannot** do is where the questions are.

| Role | Cannot |
|---|---|
| `cluster-admin` | — but in a **RoleBinding** it is limited to that namespace (**#59**) |
| `admin` | write the namespace's ResourceQuota, or the namespace object itself |
| `edit` | view or modify roles or role bindings (**#58**) |
| `view` | read Secrets; view roles or bindings (**#57**) |

> ⚠ **`edit` CAN read Secrets.** *"This role allows accessing Secrets and running Pods as
> any ServiceAccount in the namespace, so it can be used to gain the API access levels of
> any ServiceAccount in the namespace."* The formal restriction is real; the practical
> ceiling is much higher. The research manifest flagged *"`edit` cannot read Secrets"* as
> the likeliest factual slip in the chapter. **It did not happen — Bearings #1 Q5
> distractor A exists specifically to reject it.** Keep it that way.

`admin`'s ability to create roles is bounded by escalation prevention: you cannot write a
role holding permissions you do not have, absent the `escalate` verb, nor bind one absent
`bind`. So you cannot bootstrap upward.

## Subjects are named, not selected

Ch 4 §5 spent a section establishing that Kubernetes joins things with **selectors**, then
warned that assuming it held here would produce *"a specific, confident, wrong prediction
in Chapter 12."* This is that prediction. There is no `subjectSelector`.

⚠ **The *why* is the author's reading, not documentation.** Research gap **G-D** confirms
no source explains the choice. The argument — dynamic membership is a feature for routing
and a liability for authorization, because "who currently has this?" stops being
answerable by reading the policy — is sound and is flagged in an AUTHOR-REVIEW. **Do not
attach a `[source:]` tag to it.**

## Additive, with no deny

*"Permissions are purely additive (there are no 'deny' rules)."* One parenthetical in the
documentation; **B1 trap #53**; and the load-bearing fact of [[additive-never-deny]].

Two consequences that catch people:

- **You cannot carve an exception out of a grant.** Any option offering a deny rule, a
  deny verb, or a rule that removes a permission is wrong on its face.
- **A binding cannot be retargeted** (**#56**). Delete and recreate — which is a different
  operation under a system that reconciles a cluster against a repository. Handed to
  **Ch 15 §5**.

## `system:masters`

Not an RBAC grant. Bypasses every rights check, cannot be revoked by deleting bindings,
invisible to any audit that reads RBAC objects, and — if the cluster uses an authorization
webhook — requests from its members are never sent to it. Graded at Practice Q3.

## Constraints on later chapters

- **Ch 15 §5** owns the delete-and-recreate consequence under GitOps.
- **Ch 17 §4** must not conflate an authorization **Webhook** mode with an **admission**
  webhook. Practice Q18 option D already grades the conflation.
- ⚑ **Expand RBAC here.** The acronym's first use in the book is bare at
  `chapter-04:646`; §3 is the B7 owner and never expands it. See `glossary.md`.

## See also

[[serviceaccounts-and-identity]] · [[secret-exposure-and-hardening]] ·
[[additive-never-deny]] · [[pod-security-standards-and-admission]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/secret-exposure-and-hardening.md ===
# Concept — Three ways into a Secret, and what closes each

**Definition home:** Ch 4 §4 (the object) · **Ch 12 §4 (exposure and hardening)**
**Objective:** D2.2 · **Carries B1 traps #60, #61**
**Sources:** `k8s-docs-secret-2026-08-23`, `k8s-docs-secret-risks-2026-08-31`,
`k8s-docs-secrets-good-practices-2026-08-24`, `k8s-docs-encrypt-data-2026-08-31`,
`k8s-docs-rbac-good-practices-2026-08-31`

---

## The three routes

| # | Route | Closed by |
|---|---|---|
| 1 | **API access** — including `list` and `watch`, which reveal contents | least-privilege RBAC on Secrets specifically |
| 2 | **etcd access** — including **backups** | encryption at rest |
| 3 | **The ability to create a Pod** | **nothing inside the namespace** |

**Route 3 is the one nobody counts as a permission to read secrets**, and it is the
chapter's most consequential practical fact.

> *"Permission to create workloads (either Pods, or workload resources that manage Pods)
> in a namespace implicitly grants access to many other resources in that namespace, such
> as Secrets, ConfigMaps, and PersistentVolumes that can be mounted in Pods. Additionally,
> since Pods can run as any ServiceAccount, granting permission to create workloads also
> implicitly grants the API access levels of any service account in that namespace."*
> `[source: k8s-docs-rbac-good-practices-2026-08-31]`

**The mechanism is not subtle once seen.** A Pod spec can mount any Secret in its
namespace. If you can create a Pod, you can create one that mounts the Secret and prints
it. You never asked for `get secrets`; you have `create pods`, which everybody who deploys
anything holds.

> ★ **An RBAC audit that greps for `get secrets` and finds nobody holding it is reading
> the wrong permission.** Bearings #2 Q1 is built on this and labelled an intentional
> challenge item. Its distractor D gets the population right and the mechanism exactly
> backwards — blaming `delete` rather than `create` — because people instinctively police
> the destructive verbs.

**The documentation draws the only correct conclusion:** *"namespaces should be used to
separate resources requiring different levels of trust or tenancy… **boundaries within a
namespace should be considered weak**."* If two things must not read each other's Secrets,
they go in different namespaces. **No arrangement of Roles inside one namespace achieves
it**, because the escalation path does not run through Secret permissions at all.

## Route 2 makes Ch 8's backup clause come due

**A backup of etcd is a copy of every Secret in the cluster, in the clear**, protected by
whatever protects your backups. `chapter-08:967` told the reader to keep etcd backups
encrypted and pointed here for the reason. §4 closes it in near-matching words.

## What encryption at rest buys, stated honestly

It protects the object **as written to etcd** — closing route 2 completely — and does
**nothing** about routes 1 and 3, because an authorized caller receives the object
decrypted as normal.

> *"The lock is on the box; it says nothing about who is handed the box. That is not a
> shortcoming; it is the definition of the control."*

⚠ **Scope errors this exists to prevent.** It does not encrypt filesystems mounted into
containers (that needs a storage integration or application-level encryption), and it is
not the reason the kubelet's copy sits in tmpfs — that is a separate protection with a
separate rationale. Bearings #2 Q2 distractors C and D are exactly these.

⚠ **And a configured-looking file is not encryption.** With `--encryption-provider-config`
set but `identity` listed first, nothing is encrypted.

## File over environment variable — the argument, precisely

⚑ **`chapter-11:444` promised "the other half of an argument" and the half that exists is
not the half the phrasing implied.** Research gap **G-C**.

**What is sourced:** a mounted Secret receives updates automatically, *"except when
mounted as a `subPath`"*; an environment variable is read at container start and is then a
fixed string for the life of the process. Plus tmpfs, plus per-container scoping.

**What is NOT sourced and the chapter correctly refuses to claim:** that environment
variables specifically leak into logs, `kubectl describe`, or child processes. The
documentation's warning is **symmetrical** between the two mechanisms. The chapter names
the widely repeated claim, says the docs do not support it, and declines.

**Preserve that refusal.** It is the better recommendation for being accurately argued,
and a later chapter that "restores" the leak argument reintroduces an unsourced claim the
book deliberately rejected.

## The four hardening steps

Encryption at rest · least-privilege RBAC on Secrets (restrict `watch`/`list` to
privileged system components; restrict `get`/`watch`/`list` for humans; etcd access to
administrators only, **including read-only**) · restrict access to specific containers ·
external secret store providers. `[source: k8s-docs-secret-2026-08-23]`

*A Pod is not a trust boundary between its own containers unless you make it one.*

And, aimed at the reader rather than the cluster: base64 in a Git repository is a
plaintext password in a Git repository with a costume on.

## Constraints on later chapters

- **Ch 13 §2** inherits: a Pod referencing a Secret that does not exist never gets a
  running container. ⚠ **This behaviour is unsourced in Ch 12's corpus** — the Secret
  concept page, the risks page and the good-practices page were all checked and none
  describes it. The chapter keeps the wording deliberately non-specific (no reason string,
  no phase name) for that reason. **Source it before Ch 13 drafts**, since Ch 13 plans to
  grade on it.
- **Ch 17 §5** owns encryption *in transit* and mTLS. §4 draws the line deliberately.

## See also

[[rbac]] · [[serviceaccounts-and-identity]] · [[securitycontext]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/securitycontext.md ===
# Concept — `securityContext` and the workload-to-host axis

**Definition home:** Ch 12 §5 · **Objective:** D2.2 — **closes half of research gap G5**
**Collects Ch 11's `hostPath` deferral and Ch 10's second axis.**
**Sources:** `k8s-docs-security-context-2026-08-31`,
`k8s-docs-linux-kernel-security-constraints-2026-08-31`,
`k8s-docs-secret-risks-2026-08-31`, `k8s-docs-rbac-good-practices-2026-08-31`

---

## The axis

> ★ **`securityContext` governs the workload-to-host axis. NetworkPolicy governs the
> workload-to-workload axis.** Separate systems, separate objects, separate layers. They
> fail independently and neither substitutes for the other: a Pod perfectly isolated by
> NetworkPolicy can still be `privileged: true` and read every Secret on its node.

Ch 10 §7 drew two axes and filled in one. **This section is the proof of the other**, and
it is the boundary the chapter's title is actually about — everything else in the chapter
arranges who may ask the API for what.

⚑ **Sourcing note, and it is the strongest single improvement available to this chapter.**
Ch 12's source set contains **no NetworkPolicy snapshot**, yet this Fixed Point, §9's
argument, Practice Q15 and Practice Q21 all rest on three NetworkPolicy claims (additive
with no deny; implemented by a CNI plugin, not the API server; designed against lateral
movement in a flat network). Ch 10 carried those citations and Ch 12 says so in prose.
**Pull Ch 10's NetworkPolicy snapshot into Ch 12's source set** so §9 is verifiable in
place.

## The default position

A container is a process in Linux namespaces and cgroups sharing the host's kernel
(Ch 2 §1). That gives it an isolated *view*, not a different kernel and not, by default, a
different user database. The documentation's phrasing is the tell: *"use the Pod
specification to restrict that workload from running as the root user **on the node**."*
Root in a container is **UID 0 against the host's kernel** unless `hostUsers: false` puts
it in a user namespace — a feature the docs describe as *"still in early stages of
development."*

## Two scopes, and the container wins

*"Security settings that you specify for a Container apply only to the individual
Container, and they override settings made at the Pod level when there is overlap.
Container settings do not affect the Pod's Volumes."*

Pod scope is the default for everything in the Pod; container scope is a per-container
override. **Volume ownership (`fsGroup`) is a Pod-level concern only.** And omitting
`runAsGroup` does not mean "no group" — it means group 0.

## `privileged: true` — the off-switch

Not one more setting alongside the others; **the setting that turns the others off.**
Overrides seccomp to `Unconfined`, ignores AppArmor profiles, runs as the `unconfined_t`
SELinux domain, and grants all capabilities.

**And it reaches §4's material:** a privileged container can access **all Secrets on that
node** — not its namespace's, the node's.

The RBAC good-practices page closes the loop back to §3: *"Users who can run privileged
Pods can use that access to gain node access and potentially to further elevate their
privileges,"* with the named mitigation being Baseline or Restricted enforcement — which
is why §6 comes next.

## The apparatus beside the field

- **Stronger isolation at the runtime layer** — RuntimeClass and sandboxes. Ch 2 §7's
  material, **referred to, not re-taught.**
- **Isolation at the placement layer** — taints and tolerations, node affinity, pod
  anti-affinity, all of Ch 7 §4, doing a second job as isolation controls. *"Avoid running
  powerful pods alongside untrusted or publicly-exposed ones."*
- **Avoid needing root at all** — `runAsNonRoot: true`, because *"managing these
  configurations can be challenging at scale."*

## Constraints on later chapters

- **Ch 13 §2** inherits `runAsUser` as a permissions failure wearing an application
  error's clothing. The docs supply the warning; the diagnosis is Ch 13's.
- **`hostPath` risk was fully stated at Ch 11 §1 and must not be re-derived here.** §5
  honours that: it names the deferral and moves to the apparatus. See [[hostpath]].
- ⚠ **Ch 12 §5 re-quotes a Ch 11 sentence** (*"it does not prevent an application from
  writing to the mounted volume if the Pod's securityContext allows write access"*) whose
  citation lives in **Ch 11's** corpus, not Ch 12's. Re-quoted documentation should carry
  its tag on every appearance — either pull Ch 11's access-modes snapshot in, or attribute
  the quote to Ch 11 explicitly rather than to "the storage documentation."

## See also

[[pod-security-standards-and-admission]] · [[hostpath]] · [[access-modes]] ·
[[secret-exposure-and-hardening]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-security-standards-and-admission.md ===
# Concept — Three levels, three modes

**Definition home:** Ch 12 §6 · **Objective:** D2.2 — **closes the other half of G5**
**Discharges Ch 8 §2's named promise.**
**Figure:** `ch12-fig04-pod-security-standards-levels`
**Sources:** `k8s-docs-pod-security-standards-2026-08-23`,
`k8s-docs-pod-security-standards-profiles-2026-08-31`,
`k8s-docs-pod-security-admission-2026-08-31`, `k8s-docs-rbac-good-practices-2026-08-31`

---

## The derivation that makes this section easy

`chapter-08:471` promised: *"you will not be learning a new kind of thing. You will be
learning one instance of the third gate."* §6 discharges it in its opening paragraph, and
the architectural statement is one sentence — **Pod Security Admission is a built-in
admission controller.** Everything else is *which policy* and *what happens*.

> ★ **Three levels × three modes, applied per namespace by label. The level says *what* is
> checked. The mode says *what happens* when the check fails.** Independent axes.
> Confusing them is the most likely wrong answer in the chapter — Practice Q17 grades
> nothing else.

🪢 **Level = what. Mode = when it hurts.** Check the grammar before the meaning:
`enforce`/`audit`/`warn` are modes, `privileged`/`baseline`/`restricted` are levels, and no
term is both.

## Why the independence is the design, not a curiosity

It is a **migration path**. Set `warn: restricted` and `audit: restricted` while keeping
`enforce: baseline`: nothing breaks, developers see warnings, the audit log accumulates
exactly what would fail, and when the list empties you flip `enforce` knowing it will
hold. That is expressible **only** because level and mode are orthogonal.

## The levels are §5's fields with names on them

**Baseline admits the default minimally-specified Pod** — a spec with no `securityContext`
at all passes. **Restricted does not**, requiring `runAsNonRoot: true`,
`allowPrivilegeEscalation: false`, capabilities dropping `ALL`, and an explicit
`RuntimeDefault` or `Localhost` seccomp profile.

That difference generates the chapter's two best distractor pairs — Bearings #2 Q4 (no
`securityContext` under `enforce: baseline` → admitted, warned, audited) against Practice
Q16 (the same Pod under `enforce: restricted` → rejected), and Practice Q22, where four of
five Restricted requirements are met and **the missing one is seccomp, the only one that
is not obviously about root.**

*"The expense of some compatibility" is not a hedge: an image built to run as root cannot
satisfy Restricted without being changed.*

## The namespace as a control surface

Patching a namespace label is about as innocuous-looking as an operation gets. Here it
lowers the security policy of everything deployed into that namespace: *"In clusters where
Pod Security Admission is used, this may allow a user to configure the namespace for a
more permissive policy than intended by the administrators."* The same paragraph notes the
parallel for NetworkPolicy. **Two systems, same lever** — a strong candidate for an
interleaved item, and arguably evidence for §9.

## ⚑ Two open sourcing questions — resolve together

1. **The multi-label claim.** That one namespace may carry all three modes at once, at
   different levels, follows from the label grammar but is stated in so many words by no
   snapshot. The migration argument and Bearings #2 Q4 both depend on it.
2. **The label grammar itself has one attestation in the entire corpus** —
   `k8s-docs-pod-security-standards-2026-08-23.md:24`. `pod-security.kubernetes.io` appears
   **nowhere else in 168 snapshots** (verified). The PSA snapshot is **truncated**, ending
   at `## Pod Security Admission labels for namespaces` / `The label form:` with the body
   missing — which is exactly where the multi-label example lives.

**Re-fetch the PSA page in full.** It closes both, and it is the highest-value single
fetch available to this chapter.

## ⚑ PodSecurityPolicy — do not assert a version

Chapter says *"superseded."* B7's register row and orphan routing say **"removed in
1.25."** No snapshot supports a version (research gap **G-H**). Draft-v1 asserted the
version untagged in two places; both were softened, and the Exam Alert trap row was
softened to match. **Reconcile chapter, trap row, ledger and register together.**

## Constraints on later chapters

- **Ch 13 §2**: a Pod refused by `enforce` **never starts**. Not a Pod that starts and
  crashes — an object the API server declined, with no phase, no events and no logs. A
  different diagnostic shape entering the triage flow at a different point.
- **Ch 16 §3**: a debug container is a container. Under `restricted`, a debugging tool
  injecting an elevated container can be refused by admission — mid-incident.
- **Ch 17 §4** must keep the *definition vs instantiation* framing: the Standards are a
  definition; PSA and the third-party engines are instantiations.

## See also

[[securitycontext]] · [[policy-engines-and-runtime-detection]] · [[rbac]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/supply-chain-security.md ===
# Concept — The supply chain as a sequence of checkpoints

**Definition home:** Ch 12 §7 · **Objective:** D2.2 + **substantial D4**
**Closes most of research gap G22.** Completes two Ch 2 deferrals.
**Figure:** `ch12-fig05-supply-chain-checkpoints`
**Sources:** `k8s-docs-cloud-native-security-2026-08-23`,
`k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31`,
`sigstore-overview-2026-08-23`, `notary-project-signing-digest-2026-08-31`,
`in-toto-overview-2026-08-31`, `tuf-overview-2026-08-31`,
`sbom-standards-spdx-cyclonedx-2026-08-31`, `harbor-overview-2026-08-31`,
`kyverno-overview-2026-08-23`

---

## Teach the sequence, not the roster

There are five or six well-known projects here and **they are not alternatives to each
other** — they occupy different positions in a sequence. A roster organization is the
wrong one and the chapter says so.

```
BUILD → SCAN → SIGN → RECORD → RESTRICT │ VERIFY → RUN
                                        │
        everything left of the line     │  the first checkpoint
        happened elsewhere, under       │  the cluster performs
        someone else's control          │  itself
```

**That vertical line is the figure's whole point.** Admission is the cluster's gangway.
Practice Q2's distractor D gets the *order* right and the *boundary* wrong — a registry
restricting pulls is a real control and is not the cluster — which is the precise
distinction the line draws.

## The four claims, and none does another's work

> ⚓ **A signature tells you where something came from, a scan tells you what is wrong with
> it, an SBOM tells you what is in it, provenance tells you how it was made, and none of
> the four does any of the others' work.** Every real supply-chain question is asking which
> of those you need.

## ★ A signature binds to a digest, not a tag

> *"Notation resolves the tag to the digest before signing if a tag is used to identify the
> container image."* / *"Always reference and use the image digest instead of a tag since
> digest is immutable."* `[source: notary-project-signing-digest-2026-08-31]`

Ch 2 taught tags-versus-digests as build hygiene. **It was not hygiene — it is the reason a
signature means anything at all.** A tag-covering signature would assert *"whatever
`myapp:v2` happens to point at is trustworthy"*, retroactively extending the attestation to
bytes the signer has never seen. Worse than no signature, because it would look like one.

🪢 **You sign the bytes, not the label on the box.**

⚑ **Attribute this to the Notary Project, not to Sigstore.** Research gap **G-G**: the
cosign docs were fetched and state none of it; the equivalent statement was found in
Notary's docs instead.

## Keyless signing removes the worst problem in signing

Ephemeral key pair → Fulcio issues a short-lived certificate against a verified identity →
sign → **discard the private key after a single signing** → record in Rekor. There is no
long-lived secret to steal.

## TUF answers what signing cannot

Every attack TUF names involves a **correctly signed** artifact: a frozen file, an older
insecure version presented as newer, a not-quite-newest file, a compromised signing key.
**Signing answers authenticity and says nothing about freshness, ordering or key
compromise.** Practice Q23 is built on exactly this and is the chapter's best
discrimination item.

## Verification is where signing becomes a control

*"Signing without verification is theater. A signature that nothing checks is a file in a
registry."* The check happens at admission — Sigstore's Policy Controller, or Kyverno.
**The third gate again, doing a third job**, which hands straight into §8.

> This is an unnamed instance of [[absent-component-pattern]] — an artifact with nothing
> watching it. §7 lands the point **without reaching for the pattern's name or an
> ordinal**, which is a working demonstration of that shard's preferred resolution.

## Gaps carried in this section

- **Image scanning is deliberately thin.** No source describes the practice beyond two
  one-line recommendations. A named scanner appeared in draft-v1's figure, was attested by
  nothing, and was removed. **Do not reintroduce named scanners without a source.**
- **CVE's expansion is unsourced**; **no source defines an SBOM in one sentence**;
  **`attestation` is glossed by the author, not by a source**; **in-toto's page never uses
  the word *provenance*** (the SPDX tag carries that term). All four are flagged in
  AUTHOR-REVIEW comments. **Do not attach `[source:]` tags to any of them.**
- Trimmed per the curriculum-alignment finding that §7 was over-covered: the ISO/IEC
  5962:2021 and ECMA-424 standardization details. Both remain sourced if wanted back.

## Closing Chapter 2

`chapter-02:393` called reproducible layers *"the hinge on which supply-chain verification
swings"*; `chapter-02:459` flagged registry access as *"a genuine security boundary rather
than a convenience feature."* Both are completed here, not repeated.

⚠ **§7 transposes the second quote onto `imagePullSecrets`.** Ch 2 applies it to
**registry access**. The phrase is verbatim and italicized — the book's quotation signal —
so it reads as a quote about something Ch 2 did not say it about. Attribute to registry
access or drop the italics. And the field is `imagePullSecrets`, plural; §7's authorial
sentence uses the singular.

## See also

[[policy-engines-and-runtime-detection]] · [[security-maps-phases-and-4cs]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/policy-engines-and-runtime-detection.md ===
# Concept — Two positions: admission time and runtime

**Definition home:** Ch 12 §8 · **Objective:** D2.2 + **D4** — **closes research gap G23**
**Sources:** `kyverno-overview-2026-08-23`, `falco-overview-2026-08-23`,
`cncf-glossary-policy-as-code-2026-08-31`,
`k8s-docs-pod-security-standards-profiles-2026-08-31`

---

## The organizing question is *when does the rule run?*

| | admission time | runtime |
|---|---|---|
| **Examines** | the object, as submitted | process behaviour, as it happens |
| **When** | before the object exists | after it is running |
| **Can** | refuse, or change | observe, and report |
| **Fixed question** | Pod Security Admission | — |
| **Arbitrary question** | Kyverno, OPA/Gatekeeper | **Falco** |

Three ways of covering the same territory. **Not which engine — when.**

## Why a policy engine exists at all

PSA answers one question extremely well and **is not extensible**. "Every Pod must carry a
`cost-center` label," "no image from outside our registry," "every new Namespace gets a
default-deny NetworkPolicy" — PSS has nothing to say about any of it. Bearings #3 Q3 is
exactly this, and its distractor A invents a custom-level mechanism PSA does not have.

**Policy as Code** is the underlying idea: *"the practice of storing the definition of
policies as one or more files in machine-readable and processable form."* Version-controlled,
so the change history is auditable and revertible.

## ★ Falco detects; it does not prevent

*"Observes Linux kernel events (system calls) and data from plugins, enriches them with
metadata from the container runtime and Kubernetes, evaluates the event stream against a
rules engine, and emits real-time alerts."* **No step in that sequence blocks anything.**

> **A control that reports is not a lesser version of a control that refuses — it answers
> a question refusal cannot.** Admission can only reason about the object as submitted; it
> knows nothing about what the process does at hour six. Runtime detection knows nothing
> about the object and everything about the behaviour. **Keep that framing.** An exam
> question distinguishing them is asking whether you know they are different *questions*,
> not different *qualities of answer*.

Falco's default detections read as a list of §5's material seen from the other side —
privilege escalation via privileged containers, namespace manipulation, writes to `/etc`
or `/usr/bin`, shell execution inside containers. **A `privileged: true` Pod that got past
admission is invisible to every control in §6, and Falco sees the behaviour after the
fact.**

Practice Q4 in Bearings #3 is the sharpest item here, and its distractor B is worth
preserving in any rewrite: a validating policy is evaluated against **API requests at the
admission gate**, and a process writing a file generates no API request, so there is no
admission event to fire on.

## ⚑ The Chapter 8 attribution is wrong and the fix is easy

§8 says *"Validate and mutate map exactly onto a distinction Chapter 8 drew: validating and
mutating admission webhooks… Chapter 8 gave you the two webhook types as an abstraction."*

**Chapter 8 did not.** Verified directly: `mutating` appears in shipped Ch 8 **only** in
the frontmatter `concepts_covered` list (`chapter-08:126`) — **zero prose occurrences**.
`validating` appears once in prose (`chapter-08:475`), in a Closer Look about webhook
availability. B7's Ch 8 gate note corroborates from the other side: it puts
*"mutating/validating admission webhook"* on the glossary queue, meaning the pair was
deferred, not taught.

**What Ch 8 *did* establish is better for this passage** — `chapter-08:608`: *"Two of them
are asking about you and answering yes or no; the third is asking about the request itself
and has a third answer available: yes, in modified form."* Rewriting around that keeps the
recognition beat, attributes it correctly, and introduces the two webhook names here —
which the ledger permits, since Ch 8 shipped without them and the glossary queue already
records the gap.

⚠ **The four Kyverno verbs are listed by the source and defined by none of it.** The
chapter's glosses are the author's. Source them or mark them `[inferred]`.

⚠ **eBPF is deliberately not named.** B7 rules it glossary-only and not eligible for graded
text, and Falco's page describes the mechanism as kernel events and syscalls without
needing the word. **Do not add it.**

## Constraints on later chapters

- **Ch 17 §4** collects the extension points. **A policy engine is an admission webhook** —
  the cleanest available payoff for having learned the distinction, and Ch 17 owns the
  synthesis.
- **Ch 18** must not treat Falco as an observability tool. It is runtime *security*
  detection; the overlap in mechanism is not an overlap in purpose.

## See also

[[pod-security-standards-and-admission]] · [[supply-chain-security]] ·
[[pluggable-interfaces]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/additive-never-deny.md ===
# Concept — Additive, never deny: the shared semantic

**Definition home:** Ch 12 §9 (the ☀️ Zenith) · **Objective:** D2.1 + D2.2, cross-cutting
**Set up across two chapters:** `chapter-10:1312` and `chapter-11:1638` both point here.
**Figure:** `ch12-zenith-additive-never-deny`
**Status:** ⚠ **the property is sourced; the explanation is the author's reading.**

---

## The observation

**RBAC** — API layer, Role and binding objects, second gate, built for multi-tenant API
access. *"Permissions are purely additive (there are no 'deny' rules)."*

**NetworkPolicy** — network layer, selector-based policies, implemented by a CNI plugin
rather than the API server, built against lateral movement in a flat network. Additive:
policies allow, and the effect of several is the union of what they allow.

Different layers, different objects, different implementers, different problems, different
decades. **The same shape.**

## ⚠ Epistemic status — the section states it before arguing, and that ordering is the
craft

> *"The documentation states the property and does not explain it… What follows is
> therefore **a reading, not a citation**. It is the interpretation that makes the best
> sense of what both systems do. **Hold it more loosely than you hold the facts around
> it.**"*

Research gap **G-E** is marked **CONFIRMED UNSOURCEABLE** after two search passes across
the RBAC reference, RBAC good practices, the authorization reference and the NetworkPolicy
pages. **Every source states the property; none explains it.** The book is committed to an
explanation by `chapter-11:1638`, and it is delivered in skill Part 11's Simple Version /
Full Picture uncertainty form.

**Do not promote this argument to a sourced claim in any later chapter.**

## The argument, in one sentence

> **A deny rule makes the effect of a grant non-local.**

Everything follows. With deny, a rule in front of you does not tell you what it does —
somewhere else there may be a rule that cancels it. And **evaluation order becomes
semantics**: deny-overrides, first-match, most-specific-wins, explicit-beats-inherited are
all defensible and none is obvious, so the resolution procedure becomes part of what a
policy *means*.

Add the two conditions that describe a real cluster:

1. **Rules are written by many authors** — platform engineering, application teams, every
   operator's bundled bindings, Helm charts nobody reads. Policy is not authored; it
   accretes.
2. **The governed objects change constantly** — which is why wildcard access grants rights
   *"not just to all object types that currently exist in the cluster, but also to all
   object types which are created in the future."*

Under those conditions a deny rule is close to unusable. **Additive-only is what makes a
single rule readable in isolation**, and the union of grants is order-independent,
composable, and answerable without global knowledge.

## The cost, which the section names rather than hides

You cannot carve an exception out of a grant. Somebody holding `edit` who should have
everything except one verb needs a hand-built role, maintained forever as the cluster
acquires resource types nobody anticipated. **The clean composability and the expensive
exceptions are the same property.**

*"That is more work, and it is honestly more work."* Keep that sentence's register — it is
what stops the section reading as advocacy.

## What transfers

Faced with a Kubernetes access-control system they have never seen, the reader can predict
its shape — additive, no deny, removal by removing the grant — **and say why.** That is
derived, not memorized, and it survives a curriculum change.

## Constraints on later chapters

- ⚑ **No NetworkPolicy snapshot is in Ch 12's source set.** Three claims here are carried
  on Ch 10's authority via prose attribution. **Pull Ch 10's snapshot into Ch 12's set.**
- Practice Q21 distractor D invents a version history in which both systems were
  retrofitted with deny rules. Neither ever had one, and the argument here is that the
  additive design is load-bearing rather than a default somebody happened to pick. **A
  later chapter that treats no-deny as an API limitation contradicts a graded item.**

## See also

[[rbac]] · [[securitycontext]] · [[absent-component-pattern]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/hostpath.md ===

---

## Chapter 12 update — 2026-08-31 · obligation DISCHARGED, cleanly

This shard's instruction was: *"Ch 12 §5 must not re-derive the risk… Ch 12 owns the
apparatus — what polices the boundary — not the hazard."*

**Honoured.** Ch 12 §5 opens by naming Ch 11's two deferrals — the `hostPath` warning and
the `ReadOnlyMany`-is-not-a-permission-system pointer — states that this is the axis and
the apparatus, and **does not restate the hazard**. `hostPath` appears in §5 only where it
belongs: as a forbidden volume type in the Baseline and Restricted Pod Security levels
(figure `ch12-fig04`).

**What the apparatus turned out to be:** [[securitycontext]] at two scopes ·
`privileged: true` as the setting that disables the others · seccomp, AppArmor, SELinux ·
[[pod-security-standards-and-admission]] as the enforcement surface · and, notably, two
mechanisms the reader already had — Ch 7 §4's taints/affinity as *isolation* controls, and
Ch 8 §3's ResourceQuota/LimitRange as *security* controls.

**The recommended alternative recorded above (a `local` PersistentVolume) is untouched by
Chapter 12** and remains the answer to "what should I use instead."

*No conflict. No canon change. Recorded so a Ch 11 or Ch 12 retrofit can see the
obligation closed.*
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/volume-types-ephemeral.md ===

---

## Chapter 12 update — 2026-08-31 · ⚑ obligation discharged **with a substitution**

This shard recorded: *"Forward obligation — Ch 12 §4 owes the other half of the
file-versus-environment-variable argument. Ch 11 says so explicitly and hands over half of
it."*

**Ch 12 §4 delivers a half — but not the half `chapter-11:444`'s phrasing implies.**
Research gap **G-C** anticipated this and asked for the author's eye.

| | |
|---|---|
| **The half Ch 11 handed over** | `secret` volumes are tmpfs-backed, memory-resident, removed with the Pod |
| **The half Ch 11's wording implied was coming** | environment variables *leak* — into logs, `kubectl describe`, child processes |
| **The half Ch 12 §4 actually supplies** | **update propagation** (a mounted Secret stays current, *"except when mounted as a `subPath`"*; an env var is fixed at container start) plus **per-container scoping** |

**Chapter 12 refuses the leak argument explicitly, and correctly.** It names the claim,
states that the Kubernetes documentation does not make it, and quotes the documentation's
actual warning — which is **symmetrical** between the two mechanisms: *"Applications still
need to protect the value of confidential information after reading it from an environment
variable or volume."* `[source: k8s-docs-secrets-good-practices-2026-08-24]`

⚠ **Do not "restore" the leak argument in a later chapter.** It is plausible, widely
repeated in prep material, and unsourced; the book examined it and declined it on purpose.

**Recommendation:** if a Ch 11 retrofit pass happens, soften `chapter-11:444`'s phrasing so
the promised half matches the delivered one. The `subPath` exception, already owned by
[[subpath]], is the natural bridge between the two chapters.

*No canon conflict — the two halves join, just not along the seam Ch 11 drew.*
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/access-modes.md ===

---

## Chapter 12 update — 2026-08-31 · forward pointer landed

This shard's second "easy to forget" fact carried: *"It is not a permission system… ⚠
Forward pointer to **Ch 12 §5**."*

**Landed.** Ch 12 §5 re-quotes the sentence verbatim — *"it does not prevent an application
from writing to the mounted volume if the Pod's securityContext allows write access"* — and
uses it as the section's entry point: the reader met `securityContext` inside a sourced
quotation doing exactly this job, and §5 now defines it. Good handoff craft, and the
`ReadOnlyMany` fact is not re-derived.

⚠ **One sourcing defect to fix in Ch 12, not here.** The re-quoted sentence's citation
lives in **Ch 11's** source set; **Ch 12's set contains no persistent-volumes snapshot**,
so §5 attributes it loosely to *"the storage documentation."* Re-quoted documentation
should carry its tag on every appearance. **Fix: pull Ch 11's access-modes snapshot into
Ch 12's source set, or attribute the quote to Ch 11 explicitly.**

*The capability-not-policy framing and the RWO-counts-nodes Fixed Point are untouched by
Chapter 12.*
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interfaces.md ===

---

## Chapter 12 update — 2026-08-31 · ⚑ CONFLICT 3 — a third counting error, new shape

Ch 12 §4, describing the Secrets Store CSI Driver:

> *"Note the shape of that: a CSI driver `[Ch 11 §5]` delivered as a DaemonSet `[Ch 6 §7]`,
> doing a job through **two interfaces you already know**."*

**A DaemonSet is a workload controller, not one of the four pluggable interfaces.** A reader
tracking the interface thread — who was told at Ch 10 they held three, and at Ch 11 §5 that
CSI was the fourth and last — arrives here and tries to make the arithmetic work.

**This is a different error from Conflicts 1 and 2.** Those are disagreements about *which
ordinal* or *which name*. This one **admits a non-member to the set.** It is the more
damaging kind, because the set is supposed to be closed at four, and Ch 17 §4's entire job
is to collect a closed set.

**Fix: "two mechanisms you already know."** One word, and the recognition beat survives
intact — CSI driver and DaemonSet *are* both things the reader already knows.

### Standing recommendation, now with a third data point

Ch 9's *"second instance"*, the B6 skeleton's stale ordinal annotations, and now this. The
recommendation this shard has carried since Ch 11 holds and strengthens: **stop asserting
ordinals over a set the reader is still accumulating.** The membership list transfers; the
number breaks, and it has now broken three different ways in four chapters.

**⛑ B6's own note records that interface counting has already produced one collision in
this book** (Ch 9 §8's "second instance" against Ch 10's and Ch 11's "three of four"), and
that **Ch 17 §4 inherits a reader who has been reconciled**. Ch 17 §4 now has three
conflicts to reconcile, not two. Read all three before drafting it.

*Chapter 12 introduces no new interface and makes no claim about the set's membership
beyond this one sentence. Conflicts 1 and 2 are unchanged.*
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

---

## Chapter 12 update — 2026-08-31 · ⛔ STILL BLOCKED — and Chapter 13 is next

**Chapter 12 does not touch the pattern.** Verified directly against `draft-v2.md`: **zero
occurrences of `absent-component`, and zero of `without its component does nothing`.** No
instance added, no ordinal asserted, no enumeration restated.

**So the conflict recorded above is unchanged in every particular.** Convention A
(Chapter 10's, and graded at Practice Q18) and Convention B (Chapter 11's, restarting at
the Ingress) still differ by exactly two, the instance ledger's rows 7 and 8 are still
reserved for **Ch 13 §7** and **Ch 17 §7**, and both reservations are still wrong under one
of the two conventions.

> ⛔ **Chapter 13 drafts next. This is the last Stage 14 manifest before the deadline the
> block was set against.** Whichever ordinal Ch 13 §7 picks, it contradicts a graded answer
> key in the other chapter, and nothing downstream will flag it — both counts are
> internally coherent and both cite real instances.

### One new piece of evidence, and it favours the preferred fix

Chapter 12 contains **two clean unnamed instances**:

- **§7** — *"Signing without verification is theater. A signature that nothing checks is a
  file in a registry."* An artifact with nothing watching it.
- **§4** — the `EncryptionConfiguration` whose provider list names `identity` first: *"a
  configuration file that looks configured is not the same as encryption that is on."* A
  correct object, doing nothing.

**Both land, and neither uses the pattern's name or an ordinal.** That is the un-numbered
treatment working in shipped-quality text, by a chapter that was not trying to demonstrate
it. It is the strongest available argument for recommendation 2 above: **keep the rule and
the enumeration, drop the ordinal.**

If the author takes that route, these two become candidate ledger entries — extending the
table without extending the count.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 12 — D2.2 Security

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D2.2 — Security** | **Chapter 12** | **deep — primary home** | — |
| D4 — Cloud Native Architecture (ecosystem) | Chapter 12 §1, §7, §8 | **substantial but UNDECLARED** — see ⚑ | — |

**D2.2 note.** Chapter 10 held the boundary (NetworkPolicy only) and the row above is
updated accordingly: Chapter 12 is the full home. B1 sequencing implication #6 is honoured
exactly — NetworkPolicy is taught once in Ch 10 and **referred to** in Ch 12 §9, never
re-taught.

## Concept-level — D2.2, all 19 B1 concepts

Walked row by row against `domain-analysis.md:194–212`. **16 taught in Chapter 12, 2
assigned elsewhere by design, 1 unassigned anywhere.**

| B1 concept | Covered in | Depth |
|---|---|---|
| RBAC | Ch 12 §3 | deep |
| Role | Ch 12 §3 | deep |
| ClusterRole | Ch 12 §3 | deep |
| RoleBinding | Ch 12 §3 | deep |
| ClusterRoleBinding | Ch 12 §3 | deep |
| Permissions are purely additive | Ch 12 §3, §9 | deep — §9 argues it |
| Binding immutability | Ch 12 §3 | deep |
| `cluster-admin` | Ch 12 §3 | deep |
| `admin` | Ch 12 §3 | deep |
| `edit` | Ch 12 §3 | deep |
| `view` | Ch 12 §3 | deep |
| Secret storage default | Ch 12 §4 | deep |
| Secret exposure paths | Ch 12 §4 | deep — the chapter's hardest checkpoint item |
| Secret hardening steps | Ch 12 §4 | deep — all four, closing Ch 4 §4's deferral |
| Secret types | Ch 12 §4 | adequate — full table, two connected onward |
| ServiceAccount token modernization | Ch 12 §2 | deep |
| NetworkPolicy as a security control | **Ch 10** | by design (B1 #6); Ch 12 §9 refers |
| Zero trust via service mesh | **Ch 17 §5** | by design; Ch 12 §4 cross-bears forward |
| **Securing the kubelet** | **— nowhere** | ⚠ **GAP** |

⚠ **Securing the kubelet is assigned to no chapter.** `kubelet` returns **zero matches in
`chapter-lineup.md`** (verified). Chapter 12 touches it twice in passing — §1's
runtime/access clause on TLS between nodes and the control plane, and §3's one-line
description of the **Node** authorization mode — and covers neither TLS bootstrapping nor
kubelet authentication/authorization. **Chapter 12 was the natural home.** Either assign it
to a Ch 12 revision or record it as a deliberate scope exclusion.

## Trap coverage — D2.2

**10 of 10 (#53–#62) addressed**, verified line by line against `domain-analysis.md:561–570`.
The Exam Alert reproduces all ten in order with faithful corrections.

| Trap | Where corrected |
|---|---|
| #53 "RBAC has deny rules" | §3 Fixed Point + §9 + Bearings #3 Q5 + Practice Q21 |
| #54 "ClusterRole is only for cluster-scoped resources" | §3 (the three documented uses) + Practice Q6 |
| #55 The four-way matrix | §3 derivation + fig02 + Bearings #1 Q3 + Practice Q5 |
| #56 "You can retarget a binding" | §3 hazard + Bearings #1 Q4 |
| #57 "`view` can read Secrets" | §3 + Bearings #1 Q5 + §4's reprise |
| #58 "`edit` can manage RBAC" | §3 + Bearings #1 Q5 |
| #59 "`cluster-admin` always means the whole cluster" | §3 Fixed Point + Practice Q6 |
| #60 "Secrets are encrypted" | §4 Fixed Point + Practice Q10 |
| #61 The Pod-creation escalation path | §4 Fixed Point + hazard + Bearings #2 Q1 |
| #62 "Token Secrets are current best practice" | §2 Snag + Practice Q4 |

**Plus six traps the B1 inventory does not carry**, all sourced: `system:masters` cannot be
revoked by deleting bindings · `list`/`watch` reveal Secret contents · PSS levels vs PSA
modes as one axis (marked `[inferred]`, honestly) · PodSecurityPolicy as current ·
a signature covering the tag · a valid signature meaning the artifact is current ·
Falco preventing what it detects.

Traps #50–#52 are NetworkPolicy and remain Chapter 10's.

## Research gaps closed

| Gap | Status |
|---|---|
| **G5** — PSS/PSA and `securityContext`; B1's *"single most conspicuous D2.2 absence"* | **CLOSED** by §5 and §6. The research run turned §5 from the worst-sourced section in the chapter into the best. |
| **G6** — the 4Cs of Cloud Native Security | **CLOSED** by §1, from the Kubernetes project's archived v1.22 page, version banner preserved. |
| **G7** — ServiceAccounts as a concept | **CLOSED** by §2. |
| **G22** — supply chain (SBOM, signing, sigstore, in-toto, TUF, Harbor, scanning) | **MOSTLY CLOSED** by §7. CVE, the SBOM definition, and scanning mechanics remain open. |
| **G23** — policy engines (OPA/Gatekeeper, Kyverno, Falco) | **CLOSED** by §8. |
| **G-D** — why RBAC names subjects | **Discharged as the author's reading**, honouring `chapter-04:839`. |
| **G-E** — §9's design rationale | **CONFIRMED unsourceable; discharged in the uncertainty form**, honouring `chapter-11:1638`. |
| **G-F** — orphaned identity after workload deletion | **CLOSED** by §2, derived from garbage collection, honouring `chapter-06:486`. |
| **G-G** — cosign's tag-to-digest behaviour | **CLOSED by substitution** — attributed to the Notary Project. |

## Research gaps still open that touch Chapter 12

- **G-A · CVE.** The expansion is carried in-chapter and unsourced. `cve.org` and
  `nvd.nist.gov` are client-rendered and return no body. **A hand-pasted browser snapshot
  is a five-minute job.** The CVE Program's mission sentence and the CNA sentence, already
  recorded in the research manifest from the archived MITRE site, would source the entry
  today.
- **G-B · SBOM definition.** CISA and NTIA both returned HTTP 403; the CNCF glossary has no
  entry.
- **G-H · PodSecurityPolicy removal.** No snapshot states it. Fetch `migrate-from-psp/` or
  the v1.25 release notes, then reconcile chapter, trap row, ledger and register together.
- **The Pod Security Admission page is truncated in the corpus.** `pod-security.kubernetes.io`
  appears **once in 168 snapshots**. Six reader-facing sites and three graded items rest on
  that line. **Highest-value single fetch available to this chapter.**
- **Image-scanning mechanics** — no source describes the practice.
- **Kyverno's four verbs** — listed by the source, defined by the author.
- **Kubernetes authentication mechanisms** — newly needed, because two B7 rows (`JWT`,
  `OIDC`) are assigned to Ch 12 §2 and reach the reader nowhere.
- **No NetworkPolicy snapshot in Ch 12's source set**, though §5, §9 and two Practice
  questions depend on Ch 10's claims. Pull Ch 10's snapshot in.
- **G30 · sandboxed runtimes.** The lineup assigns it to Ch 12; §5 refers to Ch 2 §7 rather
  than teaching it, which is right. **Backfill should confirm Ch 2 §7 closed it.**

## ⚑ D4 under-declaration — corroborated independently

`outline.md` declares `exam_domain: "Container Orchestration (competency: Security)"` and
asserts *"No objective ambiguity: Security is the only competency this chapter touches."*

Against that: §1 teaches the 4Cs and the lifecycle phases; §7 teaches Sigstore, in-toto,
TUF, the Notary Project, Harbor and the SBOM standards; §8 teaches Policy as Code from the
CNCF glossary, plus Kyverno, OPA/Gatekeeper and Falco. **That is CNCF-ecosystem material,
D4 is 12% of the exam, and few other chapters teach it.**

**Recommendation: add D4 to the chapter's declared objectives**, or the book-close coverage
report raises a phantom "D4 under-covered" finding against a chapter that in fact carries a
good deal of it.

---

*Stage 14 · Chapter 12 · 2026-08-31.*
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 12 — backward retrieval

| Tested topic | Original chapter | Retested in |
|---|---|---|
| Cluster-scoped means *no* namespace, not *all* namespaces | ch 4 §3 | ch 12 — Bearings #1 Q3 |
| Admission is the third and last gate | ch 8 §2 | ch 12 — Bearings #2 Q5 |
| A tag is a mutable pointer; a digest is content identity | ch 2 §3 | ch 12 — Bearings #3 Q1 |
| RBAC names subjects; everything else selects | ch 4 §5 | ch 12 — Practice Q8 |
| The two axes — reachability vs workload-to-host | ch 10 §6/§7 | ch 12 — Practice Q15 |
| The admission gate as a shared position | ch 8 §2 | ch 12 — Practice Q18 |
| A signature binds to the digest | ch 2 §3 | ch 12 — Practice Q19 |
| Additive semantics, no deny rule | ch 10 §6 | ch 12 — Practice Q21 |

## Chapter 12 compliance

| Check | Target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of graded items | 20–25% (B3) | **8 of 38 = 21.1%** (15 Bearings + 23 Practice) | ✅ |
| Spacing floor (≥4 chapters back) | ≥1 item | ch 2 is **ten** back, ×2 items | ✅ |
| Tagged items land on covered material | 8 of 8 | **8 of 8** | ✅ |
| Question inventory | 8 Soundings, ≥10 Bearings across ≥2 checkpoints | 8 + 15 (3 × 5) + 23 = **46** | ✅ |

**First chapter since Ch 9 with no failed retrieval anchor.** Each tag was re-checked
against shipped text rather than against the tag. Ch 11's failed anchor (Practice Q4's
`[retrieval: ch4]` against material Ch 4 never deposited) is unaffected and still open.

**Genuine interleaving, not disguised same-chapter items.** Practice Q15 and Q21 each
require holding a Ch 10 fact and a Ch 12 fact simultaneously and discriminating between
them — what skill Part 10's spacing table asks for and what a tag alone does not guarantee.

**Soundings note.** Six of eight questions are retrieval and the block's own arithmetic is
correct: Q1→Ch 4 §3, Q2→Ch 5 §6, Q3→Ch 4 §4, Q4→Ch 8 §2, Q5→Ch 10 §6, Q8→Ch 2 §1, with Q6
and Q7 correctly identified in the preamble as drawing on professional intuition from
outside Kubernetes instead. Excluded from the budget per B3.

## Obligations Chapter 12 discharged — eighteen

Ch 2 §2 (reproducible layers → §7) · Ch 2 §3 (tags and digests → §7) · Ch 2 §6 (pull
secrets as a boundary → §7) · Ch 2 §7 (sandboxed runtimes → §5, by reference) ·
Ch 4 §3 (the scoping boundary → §3's derivation) · Ch 4 §4 (the Secret's missing lock →
§4) · Ch 4 §5 (the selector prediction → §3) · Ch 5 §6 (SA as RBAC subject → §2, partially)
· Ch 6 §3 (orphaned identity → §2) · Ch 6 §8 (custom resources granted like built-ins →
§3) · Ch 7 §4 (taints and affinity as isolation → §5) · Ch 8 §2 (three gates → §6; the RBAC
object model → §3) · Ch 8 §3 (quotas as security controls → §1) · Ch 8 §7 (the etcd backup
clause → §4) · Ch 10 §6 (additive semantics → §9) · Ch 10 §7 (the two axes → §5) ·
Ch 11 §1 (`hostPath` → §5; `secret` volumes → §4, **with a substitution**) · Ch 11 §4
(access mode is not a permission system → §5).

**All twelve section-pinned inbound pointers from shipped text land on a section that
delivers what the pointer promises.**

⚑ **One ledger obligation NOT discharged.** B7 assigns `JWT · OIDC` to **Ch 12 §2**. `JWT`
has **zero occurrences** in the chapter; `OIDC`'s only occurrence is **inside an HTML
comment** (line 251) and will not reach the reader; `OpenID` is spelled out once, at **§7**,
in the keyless-signing flow. The chapter's §2 AUTHOR-REVIEW explains why — the corpus has no
authentication-mechanisms snapshot — and the deferral is correct. **The ledger and the
acronym register have not been told.** Retarget both ledger rows and both register rows.

## Forward obligations Chapter 12 creates

| Topic Ch 12 owns | Must be retrieved in | How |
|---|---|---|
| A *rejected* Pod versus a *failed* one | **Ch 13 §2** | An object admission declined leaves nothing to inspect — no phase, no events, no logs. |
| A Pod referencing a Secret that does not exist | **Ch 13 §2** | ⚠ **Unsourced in Ch 12's corpus** — the chapter keeps the wording deliberately non-specific. **Source it before Ch 13 drafts**; Ch 13 plans to grade on it. |
| `runAsUser` on a root-expecting image | **Ch 13 §2** | A permissions failure wearing an application error's clothing. |
| An agent that watches a repository, as an RBAC subject | **Ch 15 §4** | §2's fourth documented ServiceAccount use case plants the shape. |
| Delete-and-recreate a binding, under GitOps | **Ch 15 §5** | §3's binding-immutability hazard names the consequence and defers. |
| A debug container refused by `restricted` | **Ch 16 §3** | §6 names it as a mid-incident surprise. |
| A policy engine **is** an admission webhook | **Ch 17 §4** | ⚑ Read `pluggable-interfaces.md` first — **three** live conflicts now. |
| Encryption in transit, and mTLS | **Ch 17 §5** | §4's 🔭 Closer Look draws the line for this. |
| The absent-component pattern | **Ch 13 §7, Ch 17 §7** | ⛔ **STILL BLOCKED.** Ch 12 did not touch it. |

## Open gaps

**1. ⛔ The absent-component instance count remains contested, and Chapter 13 drafts next.**
Chapter 12 neither added an instance nor asserted an ordinal — verified, zero occurrences of
either canonical string. The two conventions still differ by exactly two, and the block on
Ch 13 §7 and Ch 17 §7 stands. **This is the last manifest before that deadline.** New
evidence favouring the un-numbered fix: Ch 12 §7 and §4 each land a clean unnamed instance
without a name or an ordinal.

**2. ⚑ NEW — `JWT` and `OIDC` are ledger-assigned to Ch 12 §2 and reach the reader
nowhere.** See above.

**3. ⚑ Chapter 12 §4 admits a non-member to the pluggable-interface set** — *"two interfaces
you already know"*, of a CSI driver and a DaemonSet. Third counting error in the thread, and
the first that adds a member rather than misnumbering one. Recorded in
`pluggable-interfaces.md`. **Ch 17 §4 now has three conflicts to reconcile.**

**4. north-south / east-west is taught but never assessed.** Carried from Ch 10, untouched
by Ch 11 and Ch 12. **Still open.**

**5. ⚑ Chapter 9 undercounts the pluggable interfaces** — *"the second instance"* for CNI
against Ch 2, Ch 10 and Ch 11's third. **Still open.**

**6. CSI driver architecture is taught (Ch 11 §5) and assessed nowhere.** Untouched by
Chapter 12.

**7. Chapter 11 Practice Q4's retrieval anchor.** Untouched by Chapter 12; the fix
recommended there (rewrite around Ch 4's own cluster-scoped trio) still holds the rate.

---

*Stage 14 · Chapter 12 · 2026-08-31.*
=== END APPEND ===
```

---

## Recommended fixes carried forward from this stage

**Blocking — resolve before Chapter 13 §7 drafts.**

1. **The absent-component instance count** (⛔G). Unchanged since Chapter 11. Chapter 13 is next and is contractually required to retrieve the pattern by name and by count. My recommendation is unchanged and now has a third supporting data point: keep the rule and the enumeration, drop the ordinal.

**Fix before ship — chapter-text edits, all small, all verified independently.**

2. **§8's Chapter 8 attribution** (H1). Ch 8 has **zero prose occurrences of "mutating"** — the word lives only in its frontmatter. Rewrite around `chapter-08:608`'s *"yes, in modified form"*, which is the better anchor anyway and keeps the recognition beat.3. **The Exam Alert's broken table row** (H2). Line 1535 has three cells in a two-column table; pandoc discards the overflow, so the reader sees the trap printed twice and never sees the correction — and the paragraph directly below discusses that row by name. Two-character fix:

```
| Pod Security levels and admission modes are the same axis | Levels say what is checked; modes say what happens. Independent. `[inferred]` |
```

4. **Introduce PSS and PSA, or drop the abbreviations.** Neither is ever bound. First bare `PSA` is line 1084, inside a Bearings answer; first bare `PSS` is line 1250, in §8. They then run through the Exam Alert, four Practice answers and the Chapter Summary — 19 and 8 uses, much of it graded. One parenthetical each at the §6 Fixed Point closes it.

5. **Expand RBAC at §3, in the register's casing** (⚑D). Not a first-expansion fix — the expansion exists at `chapter-04:257` and `:839` — but a binding-and-ownership fix. The acronym's first use in the book (`chapter-04:646`) is bare, and §3, the B7 owner, never expands it in ~80 uses.

6. **Expand CEL, OWASP and SPDX, and add three register rows.** CEL first — it survives into the Chapter Summary, which readers use as a revision surface.

7. **§4's "two interfaces you already know" → "two mechanisms"** (⚑F). One word, and it keeps a non-member out of a set Ch 17 §4 has to close.

8. **§7's "doing a third job" → "doing another job."** "Third gate" is fine — a closed set the reader can see. "A third job" counts instances of an open set, which the ratified convention forbids.

9. **Two quote attributions.** §7 applies *"a genuine security boundary rather than a convenience feature"* to `imagePullSecrets`; `chapter-02:459` applies it to **registry access**. The phrase is verbatim and italicized, so it reads as a quote about something Ch 2 did not say. And §3's *"Chapter 8 quoted that list at you"* should be *"quoted part of that list"* — Ch 8 quotes three of the four authorization modes, omitting Node.

10. **Name *subject* in §2** (L3), where B7 assigns it and where `chapter-05:779` sends readers. One clause after the identity-≠-permission Fixed Point removes a use-before-definition and lands an inbound pointer.

11. **`imagePullSecret` → `imagePullSecrets`** in §7's authorial sentence. Leave the singular inside quoted documentation.

**Research — ranked by what they unblock.**

12. **Re-fetch the Pod Security Admission page in full.** The cached snapshot is truncated at `The label form:`, and `pod-security.kubernetes.io` appears **once in 168 snapshots**. Six reader-facing sites and three graded items rest on that one line. This also settles the multi-label claim and the PodSecurityPolicy version in one go.

13. **Pull Chapter 10's NetworkPolicy snapshot into Chapter 12's source set.** §5's Fixed Point, §9's entire argument, Practice Q15 and Practice Q21 all rest on three NetworkPolicy claims that Ch 12's set does not contain. This is the single strongest improvement available to the chapter's verifiability.

14. **CVE** (G-A) — a hand-pasted browser snapshot of `cve.org/About/Overview`, five minutes. Or use the two sentences the research manifest already recovered from the archived MITRE site, which would source the glossary entry today.

15. **Confirm the RBAC derivation's unsourced step.** That a cluster-scoped rule has nowhere to land when a ClusterRole is bound by a RoleBinding follows from two quoted sentences but is stated outright nowhere. Four reader-facing sites depend on it, including a graded answer. If it cannot be confirmed, **soften all four together.**

16. **Kyverno's four verbs** and the **attestation gloss** — source them or mark them `[inferred]`. The chapter flags both; the asymmetry with the SBOM case (which *is* flagged in prose) is what makes them worth closing.

17. **Fetch a Kubernetes authentication-mechanisms page** — newly required by ⚑A, and the precondition for deciding whether `JWT`/`OIDC` stay at Ch 12 §2 or move.

**Ledger and register maintenance.**

18. **Retarget the `JWT` and `OIDC` rows** away from Ch 12 §2 (⚑A) — both the ownership rows and the acronym-register rows.
19. **Add register rows** for CEL, OWASP, SPDX, and ledger rows for the seven §7/§8 projects the ledger does not assign (Sigstore, Cosign, Fulcio, Rekor, Policy Controller, CycloneDX, Kubewarden).
20. **Rule on the Notary canonical form** — the ledger says "Notary"; the project says "Notary Project," with "Notation" as the tool. The chapter follows the source.
21. **Add D4 to Chapter 12's declared objectives**, or the book-close coverage report raises a phantom finding.

**Infrastructure.**

22. **Apply the pending Stage 14 writes.** Twenty-three blocks across three manifests, none applied; `knowledge-base/` still does not exist. **Order: Ch 10 → Ch 11 → Ch 12.**
23. **Interleave the two glossary alphabets** before promoting the file to the shipped back-of-book glossary. This is the deliberate cost of appending rather than re-transcribing.
24. **`retrieval-architecture.md` on disk is still a blocked-write error message**, not the B3 artifact — flagged by Chapter 10, unchanged through Chapter 12. Regenerate.
25. **Two Stage 10 figure flags remain open** and are not re-raised as new: `ch12-zenith-additive-never-deny` is a non-conforming anchor ID (blocking for the book-level figure index), and `fig03` precedes `fig02` in reading order.
26. **Assign "securing the kubelet"** — a D2.2 concept in no chapter's lineup — or record it as a deliberate exclusion.

---

## What I'd act on first

**Item 12, the PSA re-fetch**, ahead of everything else including the two the integration report headlined.

H1 and H2 are real and I confirmed both, but each is a known defect with an obvious fix and a named line number; they will get done whenever someone opens the file. The PSA gap is different in kind. Six reader-facing sites and three graded items are resting on a single sentence in a single snapshot, the page that should corroborate it is truncated in a way nothing downstream detects, and the truncation is *silent* — the chapter reads as fully sourced because the citations are real and point at a real file. One re-fetch closes the multi-label question, settles the PodSecurityPolicy version that four artifacts currently disagree about, and removes the single point of failure. It is the cheapest fix on the list with the largest blast radius if skipped.

Then item 1, because Chapter 13 drafts next and this manifest is the last checkpoint before the deadline that block was set against.

Two things worth saying plainly about the chapter itself, since a manifest full of ⚑ marks can misrepresent it. **Chapter 12 is the first chapter since Chapter 9 with no failed retrieval anchor**, all eight tags verified against shipped text rather than against the tag. And where it lacked a source, it consistently declined to claim — the environment-variable leak argument, the PodSecurityPolicy version, the scanner names, the CVE format. Sixteen AUTHOR-REVIEW comments in the draft are the record of that discipline, not a defect count. Most of what I have flagged is ledger and register drift catching up to a chapter that got the hard calls right.