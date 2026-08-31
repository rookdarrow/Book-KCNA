# Fact-Accuracy Audit — Chapter 12

**Mode detected: STANDARD.** The `Cached sources` block carries 26 populated snapshots, and the draft carries roughly 250 inline `[source: ...]` tags. Untagged factual assertions are therefore FAIL, not advisory.

**Note on line references.** The input was `draft-v1.md` (no `draft-v2.md`; no `draft-voice.md`). Line numbers below are approximate — the quoted excerpt is authoritative for locating each finding. Where one claim appears at several sites, it is counted once and all sites are listed.

## Summary

- Total factual claims inspected: **236**
- Tagged claims verified: **196**
- Tagged claims unverifiable (source tag points to a snapshot absent from this chapter's corpus): **1**
- **Untagged factual claims (FAIL): 11**
- **Contradicted claims (FAIL): 3**
- Minor discrepancies (WARN): **25**

Overall the draft's source discipline is unusually good: it obeys every FIDELITY NOTE, WHAT THIS PAGE DOES NOT SAY block, and NOTE FOR DRAFTING in the corpus, and it declines three widely-repeated claims that the corpus explicitly records as unsourced. The failures cluster in four places: (1) the chapter's own curriculum/domain header, (2) named third-party products that never entered the corpus (Kata, Trivy), (3) definitional glosses of terms no snapshot defines (CVE, attestation), and (4) the §3 derivation, which is the chapter's central argument and has no documentary support in this corpus at all.

---

## UNVERIFIABLE — tag points to a snapshot not in this corpus

### Line ~5 (chapter header): "**Domain: Container Orchestration (D2) — 28% of the exam** [source: cncf-kcna-curriculum-2025-11-24]"

**Status:** The snapshot `cncf-kcna-curriculum-2025-11-24` is not among the 26 included. Per the corpus note, it must be named as a gap rather than treated as verified.

**Additional discrepancy worth resolving at the same time:** every snapshot in this corpus labels D2 as **"D2 Security"** in its `objectives_covered` frontmatter (`k8s-docs-rbac-2026-08-23`, `k8s-docs-secret-risks-2026-08-31`, `falco-overview-2026-08-23`, and twenty-three others), and labels D4 as "Cloud Native Ecosystem and Principles." The draft header calls D2 "Container Orchestration." One of the two is wrong, and the audit cannot say which without the curriculum snapshot.

**Fix:** Surface `cncf-kcna-curriculum-2025-11-24` into this chapter's source set, then re-verify both the domain *name* and the *28%* figure. If the corpus frontmatter is correct, the header needs the domain name changed and every snapshot's objective mapping stays as-is.

---

## FAIL — Untagged factual claims

### Line ~8 (domain note): "The CNCF publishes weights for the four domains and for nothing below them. There is no published figure for how much of Domain 2 is security, and anyone who gives you one is guessing."

**Why it's a factual claim:** Three assertions about the vendor's published curriculum — how many domains exist, that weights are published at domain level only, and that no sub-domain figure exists. All are claims about CNCF's published exam documentation.
**Additional inconsistency:** "four domains" sits beside a header that numbers a domain D2 and snapshots that reference D4; four domains is possible but not demonstrated here.
**Fix:** Tag with `cncf-kcna-curriculum-2025-11-24` (same gap as the header). This paragraph is the chapter's honesty disclaimer about its own allocation and it is the one paragraph that most needs a citation.

### Line ~232 (§1, "Why both"): "But the 4Cs have not gone anywhere else. They are in essentially every third-party study guide, every conference talk from the last five years, and a great deal of internal security documentation…"

**Why it's a factual claim:** An unbounded prevalence claim about third-party publications, quantified twice ("essentially every", "every… from the last five years"). No snapshot supports it, and it is precisely the kind of manufactured-frequency statement the chapter's own Exam Alert disclaims ("it will not manufacture a statistic to make the point land harder").
**Fix:** Rewrite as a bounded, defensible statement — e.g. "the 4Cs framing predates the current page and you will still meet it in third-party material" — or mark `[inferred]`. No research gap is needed; the claim should simply not be quantified.

### Line ~215 (§1) and ~858 (§5): "RuntimeClass selects a runtime that provides stronger isolation, and gVisor and Kata Containers are the named implementations." (§1: "…is where RuntimeClass and gVisor and Kata belong on this map.")

**Why it's a factual claim:** Names two specific third-party runtimes and asserts that they are "the named implementations" — phrasing that attributes the naming to an authority.
**Corpus check:** **gVisor** is named, once, in `k8s-docs-linux-kernel-security-constraints-2026-08-31` ("consider using a sandbox, such as gVisor"). **Kata Containers appears in no snapshot in this corpus.** "Container runtime classes" appears in `k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31` ("Select container runtime classes that provide stronger isolation") but `RuntimeClass` as an API object does not.
**Fix:** Drop "the named implementations" (nothing in-corpus names them as a set). Tag gVisor with `k8s-docs-linux-kernel-security-constraints-2026-08-31` and RuntimeClass with the 4Cs snapshot. For Kata, either open a research gap for `katacontainers.io` or let the existing `[cross-bearing: see Ch 2 §7]` carry it without asserting documentary naming.

### Line ~285 (§2): "A human identity arrives at the API server from *outside* — from a certificate authority, an OIDC provider, an authenticating proxy — and Kubernetes' job is to validate the claim, extract a username and a set of groups, and hand those strings to the next gate. It stores nothing."

**Why it's a factual claim:** Enumerates three specific Kubernetes authentication mechanisms and describes the authenticator's contract.
**Corpus check:** No snapshot in this corpus covers authentication mechanisms. `k8s-docs-authorization-2026-08-31` covers authorization modules only. The username/group-as-strings half *is* supported by `k8s-docs-rbac-depth-2026-08-31` and is separately tagged two sentences later; the mechanism list is not.
**Fix:** Open a research gap for `https://kubernetes.io/docs/reference/access-authn-authz/authentication/` (X.509 client certs, OIDC tokens, authenticating proxy). Until it is cached, cut the three named mechanisms to "from outside the cluster" and keep the sourced half.

### Line ~455 (§3, "The two binding objects, and the derivation"): "**a permission over a cluster-scoped resource cannot be granted inside one namespace, because there is no namespace to grant it in.** Not 'should not.' *Cannot.*"

**Why it's a factual claim:** A behavioral assertion about how the API server evaluates a ClusterRole's cluster-scoped rules when bound by a RoleBinding. It is stated as forced by structure, in bold, as the load-bearing premise of §3.
**Corpus check:** `k8s-docs-rbac-2026-08-23` says only that "a RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding." It never states what becomes of cluster-scoped rules in that case. No other snapshot addresses it.
**Sites that depend on it:** the derivation prose (~L455); figure `ch12-fig02` (~L490); Taking Your Bearings #1 answer 3 — "the cluster-scoped rule simply has no effect there" (~L600); Practice Q5 answer B and the option-C explanation — "the `Node` rule would simply have no effect" (~L1712).
**Fix:** This is the chapter's highest-value gap. Open a research gap for a kubernetes.io passage confirming that a ClusterRole bound via RoleBinding grants only within that namespace and that cluster-scoped rules are inert there (the RBAC reference's RoleBinding/ClusterRoleBinding section is the likely home). Four separate reader-facing conclusions rest on this; it should not ship on inference alone.

### Line ~490 (§3, figure ch12-fig02): "Role + ClusterRoleBinding → ✗ does not exist. A Role's rules are namespace-local; there is nothing cluster-wide to grant."

**Why it's a factual claim:** An assertion about API validation — that this object combination is rejected/impossible.
**Corpus check:** Not stated in `k8s-docs-rbac-2026-08-23` or `k8s-docs-rbac-depth-2026-08-31`. The snapshots describe what each binding *may* reference; neither states the negative.
**Fix:** Same research gap as the entry above — a docs passage constraining `ClusterRoleBinding.roleRef` to ClusterRole. If unavailable, soften the figure cell to reflect that a ClusterRoleBinding references a ClusterRole (positive statement, sourced) rather than asserting a validation failure.

### Line ~757 (§4, closing note) and ~1840 (The Voyage Ahead): "a Pod that references a Secret which does not exist does not start. It is a specific, recognizable failure shape, distinct from a Pod that starts and then dies…"

**Why it's a factual claim:** A behavioral claim about Pod startup semantics, offered as a diagnostic signature and forwarded into Chapter 13 as one of three things the reader should "bring with you."
**Corpus check:** Neither `k8s-docs-secret-2026-08-23` nor `k8s-docs-secret-risks-2026-08-31` nor `k8s-docs-secrets-good-practices-2026-08-24` says anything about a missing-Secret reference blocking Pod start.
**Fix:** Open a research gap for the Secrets page's "Using a Secret" / consumption section or the Pod lifecycle docs. This one is cheap to source and is handed forward to the next chapter, so it should be closed before Ch 13 drafts against it.

### Line ~975 (§6, "PodSecurityPolicy") and ~1530 (Exam Alert traps table): "PodSecurityPolicy was the predecessor, it was removed in Kubernetes 1.25… It appears throughout prep material written before 2025." / Traps row: "PodSecurityPolicy is a current control | Removed in 1.25; superseded by Pod Security Admission."

**Why it's a factual claim:** A specific version number for a feature removal, plus a prevalence claim about third-party prep material. The traps table row is the only untagged row in that table besides two the chapter deliberately marks as derivations.
**Corpus check:** `k8s-docs-pod-security-admission-2026-08-31` declares `podsecuritypolicy-removed` in its `concepts_covered` frontmatter — but **the snapshot body is truncated** (it ends at "## Pod Security Admission labels for namespaces / The label form:") and contains no PodSecurityPolicy text at all. So the concept is claimed as covered and is not actually present.
**Fix:** Re-cache `k8s-docs-pod-security-admission-2026-08-31` in full (see WARN — corpus health), then tag both sites. Separately, drop or hedge "appears throughout prep material written before 2025" — it is an unsourced prevalence claim of the same kind as the 4Cs one above.

### Line ~1110 (§7, "Scan"): "A **CVE** — Common Vulnerabilities and Exposures — is an identifier for a publicly disclosed vulnerability, and a scanner's job is to enumerate the packages in an image and report which of them have CVEs against them."

**Why it's a factual claim:** Defines an external standard (MITRE/CVE Program) and describes third-party scanner behaviour.
**Corpus check:** `k8s-docs-linux-kernel-security-constraints-2026-08-31` cites CVE-2022-0185 and CVE-2019-5736 by number; no snapshot expands the acronym or defines the program. The existing AUTHOR-REVIEW comment at ~L1120 already flags that scanner *mechanics* are unsourced (G22) but does not cover the CVE definition itself.
**Fix:** Open a research gap for `cve.org` (or the CNCF glossary, though its index — checked 2026-08-31 per `cncf-glossary-policy-as-code-2026-08-31` — has no CVE entry). Alternatively drop the definition and use "a known, publicly disclosed vulnerability" without naming the program as a defined standard.

### Line ~1098 (§7, figure ch12-fig05): "Trivy, Harbor / scanners"

**Why it's a factual claim:** Names a specific third-party product as an instance of a scanner. It appears **only** in the figure — never in the prose, never with a tag.
**Corpus check:** Trivy appears in no snapshot in this corpus. Harbor is well sourced (`harbor-overview-2026-08-31`); every other product named in that figure (Cosign, Notation, Fulcio, Rekor, Kyverno, Gatekeeper, Policy Controller, imagePullSecrets) is sourced.
**Fix:** Either open a research gap for `trivy.dev` or remove "Trivy" from the figure — Harbor alone already carries the SCAN column via its sourced "Security and vulnerability analysis" feature. Removal is the cheaper fix and costs the reader nothing.

### Line ~1175 (§7, "Attestation, provenance, and SBOMs"): "**Attestation** generalizes signing. A signature says 'I vouch for these bytes.' An attestation says 'I vouch for this *claim* about these bytes'…"

**Why it's a factual claim:** Defines a term of art in supply-chain security and distinguishes it from signing.
**Corpus check:** `in-toto-overview-2026-08-31` and `notary-project-signing-digest-2026-08-31` both list `attestation` in `concepts_covered`, but **neither body defines it**. The in-toto snapshot explicitly warns: "Supply-chain layout, link metadata and steps/inspections are **not** covered on this page and must not be described."
**Fix:** Note the asymmetry — the draft added an AUTHOR-REVIEW comment for the SBOM definition (correctly, per that snapshot's caveat) but not for attestation, which is in the same position. Either add an equivalent AUTHOR-REVIEW comment and mark the definition `[inferred]`, or open a research gap for `in-toto.io/docs` or the SLSA attestation spec.

---

## FAIL — Contradicted claims

### Line ~53 (epigraph): "*'The RBAC API prevents users from escalating privileges by editing roles or role bindings…'* — Kubernetes documentation, *RBAC good practices*"

**Attribution given:** "Kubernetes documentation, *RBAC good practices*" (i.e. `kubernetes.io/docs/concepts/security/rbac-good-practices/`).
**Snapshot says:** The sentence appears in `k8s-docs-rbac-depth-2026-08-31` — `source_url: "https://kubernetes.io/docs/reference/access-authn-authz/rbac/"` — under "Privilege escalation prevention and bootstrapping": *"The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use."*
**And the good-practices snapshot does not contain it.** `k8s-docs-rbac-good-practices-2026-08-31` is transcribed in full and its nearest sentence is different: *"Generally, the RBAC system prevents users from creating clusterroles with more rights than the user possesses. The exception to this is the `escalate` verb."*
**Recommended fix:** Change the attribution line to "Kubernetes documentation, *Using RBAC Authorization*". This is the chapter's opening epigraph and it currently sends the reader to the wrong page.

### Line ~540 (§3, "Escalation prevention, and least privilege"): "*'The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use'* [source: k8s-docs-rbac-good-practices-2026-08-31]."

**Tag:** `[source: k8s-docs-rbac-good-practices-2026-08-31]`
**Snapshot says:** That snapshot does not contain the quoted sentence (full transcription; see above). The sentence is in `k8s-docs-rbac-depth-2026-08-31`.
**Draft says:** the sentence, presented as a verbatim quotation of the tagged snapshot.
**Recommended fix:** Retag to `[source: k8s-docs-rbac-depth-2026-08-31]`. Note that the two sentences immediately following it are already correctly tagged to `rbac-depth`, so this is an isolated slip, not a systematic one.

### Line ~940 (§6, paragraph following figure ch12-fig04): "The rows in that figure are the documented Baseline and Restricted controls: Baseline forbids `privileged`, host namespaces… restricts `hostPort`, added capabilities to a known list, AppArmor and SELinux to approved values, `/proc` mount type to `Default`, and sysctls to a safe list. [source: k8s-docs-pod-security-standards-profiles-2026-08-31]"

**Tag:** `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]`
**Snapshot says:** The Baseline control list contains **thirteen** controls, two of which appear neither in the figure nor in this sentence: *"**HostProcess** — disallow Windows host access. Fields: `spec.securityContext.windowsOptions.hostProcess`…"* and *"**Host Probes / Lifecycle Hooks** (v1.34+) — disallow direct host connections."*
**Draft says:** "The rows in that figure **are** the documented Baseline and Restricted controls" — an identity claim, followed by an enumeration that omits two documented controls.
**Recommended fix:** One word. Change to "The rows in that figure are the Baseline and Restricted controls this chapter grades on" (or "the load-bearing rows of"), which is true and preserves the pedagogy. Optionally add HostProcess to the figure; Host Probes is v1.34+ and reasonably out of scope for a KCNA chapter, but the completeness claim as written is wrong either way.

---

## WARN — Minor discrepancies

### Over-attribution (tag exists; the tagged snapshot does not carry the statement)

These are all *true* and *entailed* by adjacent sourced material, but the reader sees a citation for a sentence the cited page does not contain.

**W1 — ~L960 (§6) and ~L1063 (Bearings #2, answer 4):** "A namespace may carry all three modes at once, at three different levels." / "Level and mode are independent axes, and a namespace may carry all three modes at different levels [source: k8s-docs-pod-security-standards-2026-08-23]." The snapshot gives the label form and the three modes; it does not state that a namespace may carry all three simultaneously. The claim is entailed by the label grammar, and the whole migration argument plus one practice answer rest on it. *Fix:* re-cache `k8s-docs-pod-security-admission-2026-08-31` (truncated exactly where the label form and the multi-label example live — see W21) and retag.

**W2 — ~L1215 (§7, "Restrict"):** "An `imagePullSecret` is a Secret of type `kubernetes.io/dockerconfigjson` [source: k8s-docs-secret-2026-08-23]." The snapshot's type table says only "serialized `~/.docker/config.json` file"; it never identifies that type with imagePullSecrets. `k8s-docs-service-accounts-2026-08-23` supplies the other half ("authenticating to a private image registry using an imagePullSecret"). *Fix:* cite both snapshots on that sentence.

**W3 — ~L1712 (Practice Q5 answer):** "`Node` is cluster-scoped, so a Role… has nowhere to put the rule, and the ClusterRole is forced [source: k8s-docs-rbac-2026-08-23]." The tag attributes the derivation to the RBAC snapshot, which does not make it. Same root cause as FAIL #5 above; resolving that gap resolves this tag.

### Cross-chapter deferrals (fact carried by `[cross-bearing:]`, no snapshot in *this* chapter's corpus)

The book's convention lets a cross-bearing substitute for a source when an earlier chapter carried the citation. That convention is respected here; these are logged so the revision stage knows which claims cannot be verified against the material in front of it.

**W4 — NetworkPolicy, multiple sites (~L88 Soundings A5; ~L875 §5 Fixed Point; ~L1420 §9; ~L1662 Practice Q15; ~L1690 Practice Q21).** No NetworkPolicy snapshot exists in this corpus, yet the chapter asserts that NetworkPolicy is additive, is implemented by a CNI plugin rather than the API server, and "was designed for the problem of lateral movement inside a flat network." §9's Zenith — the chapter's climactic argument — is half-built on these, and Practice Q21's correct answer C and its explanation of distractor A both depend on them. The draft is honest about it ("Chapter 10's sources said the equivalent about NetworkPolicy"), but the strongest single improvement available to this chapter is to pull the Ch 10 NetworkPolicy snapshot into this chapter's source set so the Zenith is verifiable in place. *Recommended source:* `https://kubernetes.io/docs/concepts/services-networking/network-policies/`.

**W5 — ~L768 (§5):** "Chapter 11 quoted the storage documentation verbatim: *'it does not prevent an application from writing to the mounted volume if the Pod's securityContext allows write access.'*" A verbatim documentation quotation with no snapshot in this corpus. Re-quoted documentation should carry its source tag even on the second appearance. *Recommended source:* the persistent-volumes access-modes snapshot from Ch 11.

**W6 — ~L82 (Soundings A4), ~L890 (§6), ~L1075 (Bearings #2 answer 5):** the three-gate ordering (authentication → authorization → admission). `k8s-docs-authorization-2026-08-31` establishes the authorization step and its default-deny behaviour but never enumerates the three gates in sequence. Ch 8 material; flagged only because §6's entire derivation opens on it.

**W7 — ~L108 (Soundings A8), ~L775 (§5):** "a container is a process in a set of Linux namespaces and cgroups, sharing the host's kernel." Ch 2 material; no snapshot here.

**W8 — ~L490 (figure ch12-fig02):** the namespaced/cluster-scoped example sets ("Pod, Service, Secret, Deployment, ConfigMap" vs "Node, PersistentVolume, StorageClass, Namespace"). Ch 4 material; correct, unsourced here.

### Claims stated more strongly than the corpus supports

**W9 — ~L1000 (§6):** "Restricted requires `runAsNonRoot: true`, and a great many published images assume root." The first clause is sourced; "a great many published images assume root" is an unquantified prevalence claim about third-party images. *Fix:* hedge or mark `[inferred]`.

**W10 — ~L950 (§6, Closer Look):** "`NET_BIND_SERVICE` is the exception because binding a port below 1024 is the single most common legitimate reason a container wants a scrap of root's authority." The rule is sourced; the superlative rationale is not. *Fix:* "a common legitimate reason", or `[inferred]`.

**W11 — ~L520 (§3, Worth Securing):** "Cloud IAM systems that do support attribute-based group membership generally pair it with heavy audit tooling for exactly this reason." A claim about external products with no corpus support. The chapter elsewhere marks its unsourced readings explicitly (§3's "here is the reading", §9's "a reading, not a citation") — this aside has neither. *Fix:* mark `[inferred]` for consistency with the chapter's own convention.

**W12 — ~L125 (Why This Chapter Matters):** "The industry arrived at the 4Cs and at the lifecycle phases because practitioners kept solving one layer beautifully and shipping the other three wide open." An unsourced causal history. *Fix:* soften to a statement about what the two framings *do* rather than why they arose.

**W13 — ~L780 (§5):** "A process running as root inside a container is, absent further configuration, running as **UID 0 against the host's kernel**." Stated as bald fact; the corpus supports it only obliquely, via `k8s-docs-linux-kernel-security-constraints-2026-08-31`'s "restrict that workload from running as the root user **on the node**" and the `hostUsers: false` passage ("run containers as root users in the user namespace, but as non-root users in the host namespace on the node"). The next paragraph does quote and tag the first of these. *Fix:* attach the tag to the claim sentence itself; the support exists.

**W14 — ~L300 (§2):** "Kubernetes has no User object. There is no `kubectl create user`." Entailed by the sourced "by default, user accounts don't exist in the Kubernetes API server", but the specific CLI-absence claim is stronger than the snapshot's sentence. Low risk; noted for completeness.

**W15 — ~L360 (§2, "Identity outlives the workload"):** "When you delete a Deployment, cascading deletion removes what the Deployment owns: its ReplicaSet, and through that, its Pods… a ServiceAccount you created alongside a Deployment is not *owned* by it. Neither are the Secrets it referenced. Neither are the RoleBindings." `k8s-docs-garbage-collection-2026-08-24` covers cascading deletion and owner references generally and mentions "the pods left behind when you delete a ReplicaSet", but never the Deployment→ReplicaSet→Pod chain nor the non-ownership of ServiceAccounts/Secrets/RoleBindings. The tagged sentence between them is correctly sourced; the framing sentences are inference.

### Sourcing available but not used

**W16 — ~L505 (§3):** "**RBAC rules name custom resources exactly as they name built-in ones.** A CRD-backed resource lives in the same API, gets addressed the same way, and is granted the same way." Untagged, but `k8s-docs-rbac-depth-2026-08-31` supports it directly: *"This lets you, as a cluster administrator, include rules for custom resources, such as those served by CustomResourceDefinitions or aggregated API servers, to extend the default roles"* and *"You can assume that CronTab objects are named `"crontabs"` in URLs as seen by the API server."* *Fix:* add the tag — free verification.

**W17 — ~L1180 (§7):** "That sentence — *what steps, by whom, in what order* — is in substance what **provenance** means." The in-toto snapshot authorises this reading ("is in substance the definition of **provenance**") but also records that "The word 'provenance' itself does not appear on this landing page; see § Gaps." The draft states it without the hedge — and inconsistently, since the adjacent SBOM definition *does* get an AUTHOR-REVIEW comment for the same reason. Note also that `sbom-standards-spdx-cyclonedx-2026-08-31` uses the word directly: *"Provenance and Integrity: Tracking the origin and history of components, including checksums and cryptographic hashes."* *Fix:* add the SPDX tag to the provenance gloss, or add an AUTHOR-REVIEW comment matching the SBOM one.

**W18 — ~L1265 (§8):** the four Kyverno verb glosses — "Validate — refuse an object… Mutate — change an object as it passes… Generate — create *other* objects in response… Clean up — remove objects meeting a condition." `kyverno-overview-2026-08-23` lists the four verbs but defines none of them; the semantics and the examples (inject a sidecar; a new Namespace bringing a default NetworkPolicy and ResourceQuota with it) are the author's. Reasonable and standard, but presented as product behaviour. *Fix:* open a small research gap for `kyverno.io/docs/policy-types/` or mark the glosses `[inferred]`.

### Version-currency framing

**W19 — §1, "The layers: where" (~L238–L258):** The 4Cs passages are quoted in the present tense — "The documentation states the consequence bluntly", "The documentation is direct", "**Code** is described as…" — while the snapshot they come from is `k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31`, whose own header reads: *"⚠ VERSION STATUS — read before citing. This is the Kubernetes project's own 4Cs page as it stood in the v1.22 documentation."* The draft does tell the reader the framing is "older" and that the current page replaced it, so the substance is honest; the attribution voice is not. *Fix:* on first use, attribute once as "the 4Cs page, as it stood in the v1.22 documentation", then present tense is harmless.

### Internal numeric inconsistencies

**W20 — ~L16 (Attention Budget header):** "**Total time: ~155 minutes**". The table's own rows sum to **187** (10+6+10+12+22+8+14+16+12+8+14+8+8+6+4+25+4). Excluding the Exam Alert (4), Practice Questions (25) and Chapter Summary (4) gives 154, which is likely the intended figure. *Fix:* either state "~155 minutes of reading, plus ~30 for the exam alert, questions and summary", or correct the total to ~187.

**W21 — ~L62 (Soundings preamble):** "Five of these test material from earlier chapters. Three test professional intuitions you may have built outside Kubernetes entirely." Seven of the eight answers carry `[cross-bearing:]` pointers to earlier chapters (A1 Ch4, A2 Ch5, A3 Ch4, A4 Ch8, A5 Ch10, A7 Ch2, A8 Ch2); only A6 is purely outside-intuition. The 5/3 split does not reconcile with the questions as written. *Fix:* recount, or move Q7's Ch 2 cross-bearing if it is meant to read as an outside-intuition item.

**W22 — ~L105 (Soundings reading strategy):** "§3 because it carries seven of this chapter's ten sourced traps." Against the Exam Alert traps table, which has **14 rows, 11 of them source-tagged**, of which **7 are §3 traps but only 6 are sourced** (the "four combinations must be memorized" row is untagged). Neither number lands. This may refer to a B1 trap inventory outside this corpus (the rbac-depth snapshot references "B1 TRAP #58"), in which case the audit cannot check it. *Fix:* reconcile against whichever inventory is meant, and if it is the Exam Alert table, correct to "six of this chapter's eleven sourced traps."

**W23 — ~L1540 (Exam Alert, closing paragraph):** "Two of these — the level/mode confusion and any claim about supply-chain project frequency — are marked `[inferred]`." The table marks **one** row `[inferred]` (PSS levels/modes), and contains **no row** about supply-chain project frequency. The sentence describes a table that does not exist. *Fix:* either drop the second clause, or add the supply-chain-frequency trap row it refers to. This matters beyond tidiness: it is the chapter's own `[inferred]` ledger, and it currently misreports itself.

### Presentation

**W24 — ~L935 (figure ch12-fig04):** "cumulative: privileged ⊃ baseline ⊃ restricted" sits directly above the gloss "(restricted includes every baseline requirement, plus the rows below the line)". The ⊃ chain is only correct if read as *sets of permitted Pods*; the gloss reads it as *sets of requirements*, in which case the direction inverts. `k8s-docs-pod-security-standards-2026-08-23` says the policies "are cumulative and range from highly-permissive to highly-restrictive", and the profiles snapshot says "The Restricted policy is cumulative: it includes every Baseline requirement." *Fix:* label the axis — e.g. "permitted Pods: privileged ⊃ baseline ⊃ restricted" — or drop the symbol and keep the prose gloss.

**W25 — ~L1620 (Practice Question 12):** the question stem is corrupted: "**12.** Which**12.** Which statement about mounting a Secret is correct?" Not a fact-accuracy issue, but it looks like a generation-seam artifact rather than a typo, so it is flagged here in case anything else in that region was affected. The answer options and explanation for Q12 are intact and correctly sourced.

### Corpus health (blocks two findings above)

**W26 — two snapshots in this corpus are truncated mid-section.**
- `k8s-docs-pod-security-admission-2026-08-31.md` ends at "## Pod Security Admission labels for namespaces / The label form:" with nothing following. It therefore carries none of the label mechanics its `concepts_covered` promises (`namespace-label-control-surface`, `psa-enforce`, `psa-audit`, `psa-warn`, `podsecuritypolicy-removed`). This is the direct cause of FAIL #8 (PSP removed in 1.25) and W1 (all-three-modes).
- `k8s-docs-encrypt-data-2026-08-31.md` ends at "It names the API kinds to encrypt and an ordered list of providers:" with the provider list missing. The draft claims nothing past that point, so no finding follows — but the snapshot should be completed before any chapter grades on provider ordering.

*Fix:* re-fetch both before the revision stage runs, then close FAIL #8 and W1 by tagging rather than by rewriting.

---

## PASS — Verified claims

Sampled across all nine sections. Beyond routine verification, the draft's handling of the corpus's own warning blocks is worth recording as coverage evidence: **every fidelity note, caveat and "what this page does NOT say" instruction in the 26 snapshots was obeyed.**

**Fidelity-note compliance (each of these was a trap the corpus set, and the draft cleared it):**

- **§3, `edit` and Secrets** (~L512). `k8s-docs-rbac-depth-2026-08-31` carries "⚠ FACT-CHECK FOR §3 AND B1 TRAP #58… The book must not state that `edit` cannot read Secrets." The draft states the opposite of the common error, in the docs' own words: *"However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace."* The Exam Alert trap row ("`edit` can manage RBAC in its namespace → It cannot; `admin` can") matches the snapshot's blessed formulation exactly.
- **§4, environment-variable leakage** (~L740). `k8s-docs-secret-risks-2026-08-31` records that the "env vars leak into logs/`kubectl describe`/child processes" claim "was searched for and not found" anywhere on kubernetes.io. The draft explicitly declines it — *"You will read that in a great deal of prep material and it is plausible, but the Kubernetes documentation does not say it"* — and builds the file-over-env-var argument from the two sourced halves (tmpfs; rotation) exactly as the snapshot permits, with an AUTHOR-REVIEW comment recording the decision.
- **§7, SBOM definition** (~L1190). `sbom-standards-spdx-cyclonedx-2026-08-31`'s caveat forbids quoting a definition of SBOM as though a source supplied one, and permits describing a BOM as a standardised record of components, licensing and provenance/integrity. The draft stays inside that envelope, quotes nothing definitional, and flags the constraint in an AUTHOR-REVIEW comment naming the CISA/NTIA 403s.
- **§7, Harbor and OCI** (~L1205). `harbor-overview-2026-08-31` warns that OCI conformance may not be claimed from that page. The draft cites Harbor only for RBAC, scanning, signing, multi-tenancy and replication — no OCI claim appears anywhere in the chapter.
- **§7, digest attribution** (~L1160). `notary-project-signing-digest-2026-08-31` instructs: "It is a *Notary Project* statement, not a Kubernetes one — attribute it to the Notary Project." The draft writes "Here is the Notary Project's own statement of what happens at signing time" before both quotes. Correct.
- **§3, ABAC** (~L400). `k8s-docs-authorization-2026-08-31` frames itself as "the source for §3's one-clause ABAC disposal." The draft gives ABAC exactly one clause and says so: "That one clause is all ABAC gets in this book."
- **§3 and §8, condensed paragraphs.** `k8s-docs-authorization-2026-08-31` and `cncf-glossary-policy-as-code-2026-08-31` both mark specific paragraphs as condensed and forbid quoting them as documentation sentences. The draft restates the verb list, the request attributes, `kubectl auth can-i`/`--as`, and the Policy-as-Code "problem/how it helps" material in its own words, and quotes verbatim only the four authorization-module descriptions and the single exact PaC sentence. Correct in both places.
- **§3, why subjects are named** (~L515). `k8s-docs-rbac-depth-2026-08-31` records that the docs never explain the design choice. The draft says so — "the documentation does not answer it, so here is the reading that makes sense of it" — and adds an AUTHOR-REVIEW comment instructing later stages not to attach a source tag.
- **§8, eBPF** (~L1320). Deliberately unnamed, with an AUTHOR-REVIEW comment recording the B7 glossary-only rule. Consistent with `falco-overview-2026-08-23`, which describes the mechanism as kernel events and syscalls without the term.
- **§9, the no-deny rationale** (~L1440). The draft states the epistemic status before the argument: "**The documentation states the property and does not explain it**… What follows is therefore **a reading, not a citation**." Accurate — no snapshot in the corpus offers a rationale.

**Spot-verified quotations and tables (representative, ~40 of ~196):**

| Site | Claim | Snapshot | Result |
|---|---|---|---|
| §1 ~L160 | four lifecycle phases; develop/distribute/deploy/runtime content | `k8s-docs-cloud-native-security-2026-08-23` | exact |
| §1 ~L175 | runtime's three areas: access, compute, storage | same | exact |
| §1 ~L180 | "partition workloads across different nodes to improve isolation" | same | exact |
| §1 ~L240 | "The 4C's of Cloud Native security are Cloud, Clusters, Containers, and Code" | `…4cs…v1-22-archived…` | exact |
| §1 ~L242 | "You cannot safeguard against poor security standards in the base layers…" | same | exact |
| §1 ~L248 | "since etcd holds the state of the entire cluster (including Secrets)" | same | exact |
| §1 ~L255 | Container-layer four rows; Code-layer five rows | same | exact |
| §2 ~L270 | ServiceAccount definition, namespaced, `default` per namespace | `k8s-docs-service-accounts-2026-08-23` | exact |
| §2 ~L295 | "by default, user accounts don't exist in the Kubernetes API server" | same | exact |
| §2 ~L305 | `system:serviceaccount:` / `system:serviceaccounts:` prefixes | `k8s-docs-rbac-depth-2026-08-31` | exact |
| §2 ~L318 | default SA gets only API discovery permissions | `k8s-docs-service-accounts-2026-08-23` | exact |
| §2 ~L340 | TokenRequest, projected volume, v1.22+; token Secrets not recommended | same | exact |
| §3 ~L385 | default-deny; authorizer chain short-circuit | `k8s-docs-authorization-2026-08-31` | exact |
| §3 ~L392 | Node / ABAC / RBAC / Webhook module descriptions | same | exact |
| §3 ~L420 | Dead Reckoning object model (7 clauses) | `k8s-docs-rbac-2026-08-23` | all exact |
| §3 ~L435 | three documented uses of a ClusterRole | same | exact |
| §3 ~L470 | "A RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding" | same | exact |
| §3 ~L495 | `cluster-admin` in ClusterRoleBinding vs RoleBinding | same | exact |
| §3 ~L500 | eight API verbs | `k8s-docs-authorization-2026-08-31` | exact |
| §3 ~L502 | `resourceNames`; deletecollection/create limitation | `k8s-docs-rbac-depth-2026-08-31` | exact |
| §3 ~L508 | aggregated ClusterRoles, `aggregationRule`, default roles use aggregation | same | exact |
| §3 ~L516 | "Subjects can be group, users or ServiceAccounts" | same | exact (incl. the docs' own phrasing) |
| §3 ~L525–535 | `cluster-admin` / `admin` / `edit` / `view` descriptions | `rbac-2026-08-23` + `rbac-depth` | exact |
| §3 ~L537 | "Permissions are purely additive (there are no 'deny' rules)" | `k8s-docs-rbac-2026-08-23` | exact |
| §3 ~L545 | `escalate` / `bind` verb conditions; `user-1` example | `k8s-docs-rbac-depth-2026-08-31` | exact |
| §3 ~L552 | four least-privilege rules; `system:masters` webhook bypass | `k8s-docs-rbac-good-practices-2026-08-31` | exact |
| §4 ~L650 | "Base64 encoding is not an encryption method…" | `k8s-docs-secrets-good-practices-2026-08-24` | exact |
| §4 ~L655 | tmpfs, node-scoped delivery, local copies removed | `k8s-docs-secret-risks-2026-08-31` | exact |
| §4 ~L665 | the headline caution (three routes) | `k8s-docs-secret-2026-08-23` | exact |
| §4 ~L672 | "`list` and `watch` access also effectively allow…" | `k8s-docs-rbac-good-practices-2026-08-31` | exact |
| §4 ~L685 | workload-creation privilege escalation | same | exact |
| §4 ~L700 | "boundaries within a namespace should be considered weak" | same | exact |
| §4 ~L710 | encryption-at-rest opening; plain-text default; `--encryption-provider-config`; `identity`-first trap; `EncryptionConfiguration` group | `k8s-docs-encrypt-data-2026-08-31` | all exact |
| §4 ~L730 | four hardening steps; Components/Humans guidance; CSI driver; manifest-sharing warning | `secret-2026-08-23` + `secrets-good-practices-2026-08-24` | exact |
| §4 ~L745 | `subPath` mounts do not receive automated updates | `k8s-docs-secret-risks-2026-08-31` | exact |
| §4 ~L752 | Secret types table (8 rows) | `k8s-docs-secret-2026-08-23` | exact |
| §5 ~L790 | securityContext definition + 8-item list incl. `allowPrivilegeEscalation`/`no_new_privs` | `k8s-docs-security-context-2026-08-31` | exact |
| §5 ~L805 | Pod scope vs container scope; container overrides; volumes unaffected | same | exact |
| §5 ~L812 | `runAsGroup` omitted → root(0) | same | exact |
| §5 ~L822 | capabilities; `CAP_` prefix omitted in manifests | same | exact |
| §5 ~L832 | seccomp/AppArmor/SELinux; enforcing vs complain; profile-vs-label and path-vs-inode differences | `k8s-docs-linux-kernel-security-constraints-2026-08-31` | exact |
| §5 ~L848 | privileged overrides seccomp/AppArmor/SELinux; all capabilities; `Unconfined`/`unconfined_t` | same | exact |
| §5 ~L855 | "A container running with `privileged: true` can access all Secrets on that node" | `k8s-docs-secret-risks-2026-08-31` | exact |
| §5 ~L865 | taints/tolerations/NodeAffinity/PodAntiAffinity isolation guidance | `k8s-docs-rbac-good-practices-2026-08-31` | exact |
| §5 ~L870 | `runAsNonRoot: true`; `hostUsers: false` early-stage caveat | `linux-kernel-security-constraints` | exact |
| §6 ~L895 | "built-in Pod Security admission controller"; "Stable since Kubernetes v1.25" | `k8s-docs-pod-security-admission-2026-08-31` | exact |
| §6 ~L905 | three profile descriptions + the three profile paragraphs | `k8s-docs-pod-security-standards-2026-08-23` | exact |
| §6 ~L930 | figure ch12-fig04 control rows (13 checked against Baseline/Restricted tables) | `…pod-security-standards-profiles…` | all rows correct |
| §6 ~L955 | Restricted capabilities: drop must include `ALL`, add limited to `NET_BIND_SERVICE` | same | exact |
| §6 ~L958 | FAQ: no profile between privileged and baseline | same | exact |
| §6 ~L965 | `pod-security.kubernetes.io/<MODE>: <LEVEL>`; enforce/audit/warn semantics | `pod-security-standards-2026-08-23` | exact |
| §6 ~L985 | namespace-patch → PSA policy weakening; NetworkPolicy label parallel | `rbac-good-practices` | exact |
| §7 ~L1130 | Sigstore mission; Cosign/Fulcio/Rekor/Policy Controller; keyless flow | `sigstore-overview-2026-08-23` | exact |
| §7 ~L1155 | Notary Project mission, Notation CLI, CNCF incubating | `notary-project-signing-digest-2026-08-31` | exact |
| §7 ~L1162 | "Notation resolves the tag to the digest before signing…" / "Always reference and use the image digest…" | same | exact |
| §7 ~L1185 | in-toto integrity sentence; CNCF graduated | `in-toto-overview-2026-08-31` | exact |
| §7 ~L1195 | SPDX overview + provenance/integrity bullet + ISO/IEC 5962:2021 relation; CycloneDX + ECMA-424 | `sbom-standards-spdx-cyclonedx-2026-08-31` | exact |
| §7 ~L1200 | TUF mission + four named attacks + CNCF graduated | `tuf-overview-2026-08-31` | exact, all four |
| §7 ~L1208 | Harbor mission, registry description, feature list, CNCF Graduated | `harbor-overview-2026-08-31` | exact |
| §8 ~L1245 | Policy-as-Code definition (the one verbatim sentence) | `cncf-glossary-policy-as-code-2026-08-31` | exact |
| §8 ~L1255 | Kyverno description, four verbs, webhook-or-CLI, YAML+CEL, Git | `kyverno-overview-2026-08-23` | exact |
| §8 ~L1280 | OPA/Gatekeeper/Rego; Kubewarden+Kyverno+Gatekeeper as PSS instantiations; decoupling quote | `kyverno-overview` + `pss-profiles` | exact |
| §8 ~L1295 | Falco description, CNCF graduated, Sysdig origin, how-it-works, seven default detections | `falco-overview-2026-08-23` | exact, all seven |
| Bearings #3 ~L1395 | "`readOnlyRootFilesystem` is a `securityContext` field the Restricted level does not in fact mandate" | `…pod-security-standards-profiles…` | correct — Restricted's six controls do not include it |
| Practice ~L1720 | Q9: `admin` cannot write ResourceQuota or the namespace itself | `k8s-docs-rbac-depth-2026-08-31` | exact |
| Practice ~L1745 | Q16: Baseline "Allows the default (minimally specified) Pod configuration" vs Restricted's four requirements | `pss-2026-08-23` + `pss-profiles` | exact |

**Internal consistency checks that passed:** the Practice Questions header claims 21 questions and four earlier-chapter retrievals — 21 questions are present, and exactly four carry `[retrieval: ...]` tags (Q8 ch4, Q15 ch10, Q18 ch8, Q19 ch2). The Attention Budget's session-break placement ("after Checkpoint #2") matches the `— session break —` row and §6/§7 boundary. Safe Harbor's "Nine sections, five independent systems" matches §1–§9 and the five-system Dead Reckoning in Why This Chapter Matters.