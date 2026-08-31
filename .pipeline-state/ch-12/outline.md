I have both binding contracts, all 24 published cross-bearings into Ch 12 (twelve of them section-pinned, every one matching B6), Ch 11's four closing promises, the cached sources, and B1's ten sourced RBAC/Secret traps. Three research gaps are genuinely blocking, and one is an editorial decision rather than a fetch — **kubernetes.io's own snapshot records that the 4Cs framing was *replaced* by the lifecycle phases, and §1 is titled for both.**

---

```
---
chapter: 12
chapter_type: "content"
title: "Locks, Keys, and Watchstanders"
subtitle: "RBAC has no deny rule, and Secrets aren't encrypted"
exam_domain: "Container Orchestration (competency: Security)"
domain_weight_pct: 7
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "RBAC has no
#-- deny rule, and Secrets aren't encrypted" — nine words, inside the
#-- ≤10-word constraint. Carried forward unmodified. It names the
#-- chapter's two loudest Fixed Points, and the first half is also the
#-- §9 Zenith heading, so subtitle and synthesis agree by construction.
#--
#-- One caution for drafting: the subtitle states a Fixed Point on the
#-- chapter's second line. That is fine — it is the SUBTITLE's job, and
#-- shipped Ch 11 did the same thing. It is NOT a licence for the
#-- Soundings to state it. See the FIXED-POINT SPOILER CHECK below.

#-- EXAM_DOMAIN NOTE. D2.2 Security, recorded in Ch 9/-10/-11's house
#-- form. No objective ambiguity: Security is the only competency this
#-- chapter touches. NetworkPolicy — the one concept that would be
#-- dual-listed — was taught once in Ch 10 and is referred to here, never
#-- re-taught (B2 constraint, arc outline line 218).
#--
#-- The 7% figure is the chapter's AUTHORED allocation, not CNCF data.
#-- CNCF publishes four domain weights (44/28/16/12) and no
#-- sub-competency weights — B1 gap G33, B2 disclosure #1. The in-chapter
#-- metadata line must carry the published 28% for D2 with its source tag
#-- and the authored-allocation disclaimer, matching the house form
#-- shipped by ch-02/-05/-07/-08/-09/-10/-11. Do not present 7% as
#-- published. 7 is the largest single-chapter allocation in Part III.

#-- PREREQ NOTE. `heavy`, and heavy in Ch 11's shape rather than Ch 10's:
#-- narrow, specific pieces of many chapters rather than the whole of one.
#-- The load-bearing eight:
#--   Ch 2 §3 (digests as identity)      -> §7
#--   Ch 2 §7 (RuntimeClass, sandboxed)  -> §1, §5
#--   Ch 4 §3 (namespaced/cluster-scoped)-> §3   ** the big one **
#--   Ch 4 §4 (Secrets, base64)          -> §4
#--   Ch 4 §5 (everything is a selector) -> §3   ** the contrast **
#--   Ch 5 §6 (ServiceAccount as identity)-> §2
#--   Ch 8 §2 (the three gates)          -> §6
#--   Ch 10 §6 (additive, never deny)    -> §9
#-- A reader who skipped any one loses a section, not the chapter — with
#-- ONE exception. Ch 4 §3 is not optional. §3 is built as a derivation
#-- from that boundary and shipped Ch 8 line 577 has already promised the
#-- reader it will be, in those words. A reader who has lost the
#-- namespaced/cluster-scoped distinction cannot receive §3 as designed.
#--
#-- Consequence for drafting: the Soundings 0–2 branch names sections,
#-- not chapters (Ch 11 precedent), and singles out Ch 4 §3 as the one to
#-- re-read before starting rather than alongside.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "substantial" — 7
#-- points, seven distinct arcs. Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING, AND MORE SO HERE THAN ANYWHERE
#-- ELSE IN THE BOOK. Twenty-four published cross-bearings point at this
#-- chapter. TWELVE name a section by number:
#--   chapter-05:779  -> Ch 12 §2   ServiceAccounts as RBAC subjects
#--   chapter-08:426  -> Ch 12 §3   Role, ClusterRole, and the binding model
#--   chapter-08:577  -> Ch 12 §3   namespaced and cluster-scoped permissions
#--   chapter-08:967  -> Ch 12 §4   Secrets, and encryption at rest
#--   chapter-11:444  -> Ch 12 §4   Secrets are not encrypted
#--   chapter-10:1035 -> Ch 12 §5   what a Pod may do to its node
#--   chapter-11:440  -> Ch 12 §5   what a Pod may do to its node
#--   chapter-11:896  -> Ch 12 §5   what a Pod may do to its node
#--   chapter-08:471  -> Ch 12 §6   Pod Security Standards and Pod Security Admission
#--   chapter-10:1201 -> Ch 12 §9   RBAC and NetworkPolicy as one shared semantic
#--   chapter-10:1312 -> Ch 12 §9   additive, never deny
#--   (chapter-10:28 is a pipeline comment, not reader-facing)
#-- All twelve match the B6 skeleton exactly. §2, §3, §4, §5, §6 and §9
#-- are FIXED. §1, §7 and §8 carry no pinned pointer and are free.
#-- Verified 2026-08-31 against chapters 01–11.
sections:
  - name: "Four Layers and Four Phases"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-fig01-4cs-and-lifecycle-phases"
    checkpoint_after: false
  - name: "Who You Are"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-fig03-serviceaccount-token-flow"
    checkpoint_after: false
  - name: "What You May Do"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-fig02-rbac-four-way-matrix"
    checkpoint_after: true
  - name: "Secrets Are Not Encrypted"
    objectives: ["D2.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "What a Pod May Do to Its Node"
    objectives: ["D2.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Three Levels, Three Modes"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-fig04-pod-security-standards-levels"
    checkpoint_after: true
  - name: "Trusting What You Ship"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-fig05-supply-chain-checkpoints"
    checkpoint_after: false
  - name: "Rules That Watch"
    objectives: ["D2.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Additive, Never Deny"
    objectives: ["D2.2"]
    requires_figure: true
    figure_anchor: "ch12-zenith-additive-never-deny"
    checkpoint_after: false

#-- Nine sections against 7 weight points — the joint-largest count in the
#-- book, tied with Ch 17, and B6 states outright that it should not be
#-- compressed. It is correct: this chapter carries SEVEN independent
#-- arcs (framing, identity, authorization, secrets, workload isolation,
#-- admission policy, supply chain, runtime policy — eight if you count
#-- the synthesis) that share a domain and almost nothing else. Ch 11 was
#-- one ladder walked seven times; this is not that shape and must not be
#-- forced into it.
#--
#-- Three sections carry no figure (§4, §5, §8) — a decision, not an
#-- oversight. See § Open questions #7.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
#-- Five of eight are retrieval from shipped chapters, which per B3 makes
#-- them spaced-retrieval events at zero cost against the chapter's
#-- retrieval budget. Three are general professional priors drawn from
#-- permission systems and software signing the reader has met OUTSIDE
#-- Kubernetes, so a reader with a security background but weak
#-- Kubernetes recall still scores meaningfully.
soundings_planned:
  question_count: 8
  topics:
    - "retrieval from Ch 4 §3 and Ch 8 §5 — whether a permission over a cluster-scoped resource can be granted 'inside one namespace', and why the answer is forced rather than chosen"
    - "retrieval from Ch 5 §6 — what identity a Pod runs as when its manifest names no ServiceAccount, and where that identity comes from"
    - "retrieval from Ch 4 §4 — what base64 does to a Secret's value and what it does not do, stated as the reader was told it in Chapter 4"
    - "retrieval from Ch 8 §2 — the three gates an API request passes in order, and which of the three runs last"
    - "retrieval from Ch 10 §6 — whether one NetworkPolicy can deny traffic another NetworkPolicy allows"
    - "general professional prior — in a permission system the reader has actually used (Unix file modes, cloud IAM, a Windows ACL), whether a rule can subtract access that another rule grants"
    - "general professional prior plus Ch 2 §3 retrieval — what a signature on a software release proves and what it does not prove, and whether a signature that covers a tag would mean the same thing as one that covers a digest"
    - "general professional prior — a process running as root inside a container: whether that is the same root as the node's, and what the reader already knows from Ch 2 §1 that bears on the answer"

#-- ✅ FIXED-POINT SPOILER CHECK — all eight cleared, but Q5 needs a
#-- deliberate ruling and gets one.
#-- This chapter's Fixed Points are: the phases are a WHEN and the layers
#-- are a WHERE; the `default` ServiceAccount is an identity with almost
#-- no permissions; the BINDING type determines the scope of the grant;
#-- RBAC permissions are additive and there is no deny rule; a binding
#-- cannot be retargeted after creation; `view` cannot read Secrets;
#-- Secrets sit unencrypted in etcd by default; anyone who can create a
#-- Pod in a namespace can read every Secret in it; securityContext is
#-- the workload-to-host axis and NetworkPolicy is the
#-- workload-to-workload axis; three PSS levels x three PSA modes applied
#-- per namespace by label; a signature binds to a digest.
#--   Q1 asks about the BOUNDARY (Ch 4 §3's material, graded there), not
#--     about the four objects. It sets up the derivation without
#--     performing it, which is the whole point of §3.
#--   Q2 names the `default` ServiceAccount but asks only where a Pod's
#--     identity COMES FROM — Ch 5 §6 taught exactly that and deferred
#--     everything about permissions in as many words at line 779.
#--   Q3 is verbatim Ch 4 §4 material. §4's Fixed Points are the three
#--     exposure paths and what encryption at rest actually adds; neither
#--     is touched by asking what base64 is.
#--   Q4 is verbatim Ch 8 §2 material and does not mention Pod Security
#--     anything. §6's Fixed Point is levels x modes, untouched.
#--   Q5 ⚠ RULING. This asks about NetworkPolicy's additive semantics,
#--     which is Ch 10 §6's Fixed Point, not this chapter's. The adjacent
#--     RBAC fact IS a Fixed Point here — and shipped Ch 11 line 1638
#--     already gave it to the reader outright, on purpose, as the hook
#--     into this chapter: "the permission system you are about to learn
#--     has no way to say no. None." The book has therefore already spent
#--     the surprise deliberately. What §9 owes is not the fact but the
#--     WHY, and Q5 does not touch that. **Constraint on drafting: Q5's
#--     stem and its answer key stay entirely inside NetworkPolicy. The
#--     answer key must not say "and RBAC is the same."** Q6 does the
#--     setting-up instead, from outside Kubernetes.
#--   Q6, Q7, Q8 are posed OUTSIDE Kubernetes for the same reason Ch 11's
#--     Q5/Q7/Q8 were — they build the priors that make §3, §7 and §5
#--     land without pre-empting any Kubernetes-specific claim. Q6 in
#--     particular establishes that most permission systems the reader
#--     knows DO have deny, which is what makes §3's answer surprising
#--     rather than arbitrary.

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 21 = 39. The arc outline overrides the Bearings
#-- figure upward — "Ch 8, Ch 12, and Ch 17 each carry enough unrelated
#-- conceptual arcs to warrant three checkpoints and 12–15 Bearings" —
#-- and B4 states plainly that its Bearings numbers are minimums to
#-- exceed. Set at 15 across three checkpoints of 5, matching the shape
#-- shipped by Chapters 3–11 without exception. Chapter total 39 -> 44.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 21
  total_this_chapter: 44

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D2.2"]
  concepts:
    - "cloud-native-security-lifecycle"
    - "develop-phase"
    - "distribute-phase"
    - "deploy-phase"
    - "runtime-phase"
    - "runtime-protection-access"
    - "runtime-protection-compute"
    - "runtime-protection-storage"
    - "four-cs"
    - "serviceaccount-as-subject"
    - "rbac-subject"
    - "default-serviceaccount-permissions"
    - "user-and-group-external-identity"
    - "service-account-token"
    - "tokenrequest"
    - "projected-token-volume"
    - "long-lived-token-secret-legacy"
    - "service-account-name-field"
    - "orphaned-identity"
    - "rbac"
    - "authorization-mode"
    - "role"
    - "clusterrole"
    - "rolebinding"
    - "clusterrolebinding"
    - "four-way-binding-matrix"
    - "binding-determines-scope"
    - "rule-verb-resource"
    - "subjects-are-named-not-selected"
    - "aggregated-clusterrole"
    - "default-role-cluster-admin"
    - "default-role-admin"
    - "default-role-edit"
    - "default-role-view"
    - "additive-permissions"
    - "no-deny-rule"
    - "binding-immutability"
    - "least-privilege"
    - "base64-is-encoding"
    - "secret-storage-default-unencrypted"
    - "secret-exposure-paths"
    - "pod-creation-privilege-escalation"
    - "encryption-at-rest"
    - "encryptionconfiguration"
    - "secret-hardening"
    - "file-mount-over-env-var"
    - "external-secret-store"
    - "secret-type"
    - "securitycontext"
    - "pod-scope-vs-container-scope"
    - "run-as-non-root"
    - "run-as-user"
    - "privileged-container"
    - "linux-capabilities"
    - "read-only-root-filesystem"
    - "allow-privilege-escalation"
    - "seccomp"
    - "apparmor"
    - "workload-to-host-boundary"
    - "pod-security-standards"
    - "pss-privileged"
    - "pss-baseline"
    - "pss-restricted"
    - "pod-security-admission"
    - "psa-enforce"
    - "psa-audit"
    - "psa-warn"
    - "namespace-label-control-surface"
    - "podsecuritypolicy-removed"
    - "supply-chain-security"
    - "image-scanning"
    - "cve"
    - "image-signing"
    - "attestation"
    - "provenance"
    - "signature-binds-to-digest"
    - "sbom"
    - "sigstore"
    - "cosign"
    - "fulcio"
    - "rekor"
    - "keyless-signing"
    - "transparency-log"
    - "in-toto"
    - "tuf"
    - "notary"
    - "harbor"
    - "private-registry-restriction"
    - "policy-engine"
    - "opa"
    - "gatekeeper"
    - "rego"
    - "kyverno"
    - "validate-mutate-generate"
    - "falco"
    - "runtime-detection"
    - "admission-time-vs-runtime"
    - "one-shared-semantic"
  commands:
    - "kubectl-auth-can-i"
    - "kubectl-create-role"
    - "kubectl-create-rolebinding"
    - "kubectl-describe-clusterrole"
    - "kubectl-get-serviceaccount"
    - "kubectl-label-namespace"

figures_planned:
  - "ch12-fig01-4cs-and-lifecycle-phases"
  - "ch12-fig02-rbac-four-way-matrix"
  - "ch12-fig03-serviceaccount-token-flow"
  - "ch12-fig04-pod-security-standards-levels"
  - "ch12-fig05-supply-chain-checkpoints"
  - "ch12-zenith-additive-never-deny"
---

# Chapter 12 Outline — Locks, Keys, and Watchstanders

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 12: Locks, Keys, and Watchstanders` | required | top |
| `## *"RBAC has no deny rule, and Secrets aren't encrypted"*` | required | line 2 |
| Metadata line (domain / weight / complexity / novelty) | required | after subtitle — **conform to shipped ch-02/-05/-07/-08/-09/-10/-11 house form**, carrying the published **28%** D2 weight with its CNCF source tag inline, plus the authored-allocation disclaimer for the 7% chapter figure |
| `## Attention Budget` | required | before epigraph — **see the Attention Budget note below; Ch 11 shipped a broken one and it had to be repaired in review** |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §3, §6, §8 |
| `★ Fixed Point` ×7 | **required, min 1** | §1, §2, §3, §4, §5, §6, §7 |
| `**Dead Reckoning:**` ×2 min | **required** | §3 (the four objects and the four default roles, stated flat) and §6 (three levels, three modes, the label form) |
| `⚠ Navigational Hazards` ×3 | expected, min 1 | §3 (no deny rule; binding immutability), §4 (the Pod-creation escalation path), §5 (`privileged: true`) |
| `☀️ Zenith` | expected | §9 |
| `## Exam Alert! 🚨` | **required** | after §9 |
| `## Practice Questions` | **required** | 21 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19; hands to Ch 13 |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** `## 🔵 §3 — What You May Do`, matching Chapters 5–11 and B6 Collision #3's recommendation. Difficulty glyph before the section number.

**Zenith heading glyph — `☀️`.** `## ☀️ §9 — Additive, Never Deny`, per B6 Collision #4 and the precedent Chapters 10 and 11 set, *plus* an inline `☀️ **Zenith:**` block inside §9. The heading glyph signposts the section; the inline block is what the structural contract matches on. Both, not either.

**Zenith:** exactly one, per Part 18.10. `ch12-zenith-additive-never-deny` in §9.

**⚠ Attention Budget — inherited defect, do not repeat.** Shipped Ch 11's Attention Budget table summed to 95 minutes against a stated 85, and omitted the Soundings, the opening blocks, the Exam Alert, all 17 Practice Questions, the Chapter Summary and The Voyage Ahead. It was repaired in review (`chapter-11` line 239). This chapter is larger: nine sections, three checkpoints, 21 Practice Questions. **Build the table to cover every block in the chapter, and make the stated header total equal the column sum.** Given the size, the "Recommended" field should say *split across two sessions*, with the natural seam after Checkpoint #2 — §1–§6 are the API-and-workload half, §7–§9 the supply-chain-and-synthesis half.

**⚠ Three word collisions, and the first is the worst the book has had.**

1. **`binding`.** This is the *third* sense of the word in six chapters, and the reader met the second one **one chapter ago**: scheduler binding (Ch 7 §1, "filter → score → bind"), PV/PVC binding (Ch 11 §2, "exclusive and one-to-one"), and now RoleBinding/ClusterRoleBinding. B7's Canonical forms table rules that the RBAC objects are *object names, always in code style, never shortened to "binding"* — but §3's entire subject is bindings and the prose will not survive nine sections of `RoleBinding`-or-nothing. **§3 must open by disposing of this explicitly**, in one sentence, naming both prior senses and saying that within this section a bare "binding" means the RBAC object and nothing else. Ch 11 §2 did exactly this for the `Volume`/`PersistentVolume` near-miss and it worked.
2. **`namespace`.** Linux namespace (Ch 2 §1) versus the Kubernetes Namespace (Ch 4 §3), and this chapter is the first to need *both in the same paragraph* — §5 discusses container isolation primitives while §3 and §6 discuss namespaced permissions and namespace labels. B7 rule holds: sense A is always written **"Linux namespace"**, lowercase, never bare.
3. **`request`.** Resource request (Ch 5 §8), API request (Ch 8 §2), and now `TokenRequest` as an object name. §2 and §3 both discuss API requests heavily. Write **"API request"** wherever a resource request could be read instead; `TokenRequest` stays code-styled.

**⚠ `securityContext` has already appeared in shipped text, four chapters before §5 defines it.** Shipped Ch 11 line 896 quotes the storage documentation verbatim: *"it does not prevent an application from writing to the mounted volume if the Pod's securityContext allows write access."* The reader has met the word inside a sourced quotation with a pointer to `Ch 12 §5` attached. §5 should acknowledge this in a clause — *you have seen this word once, in a quotation, doing exactly the job this section is about* — rather than introducing it as if it were new. It is a free retrieval hook and it costs one sentence.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 12 — Locks, Keys, and Watchstanders". Carried forward without modification:

- **Covers**: **D2.2** — the cloud native security lifecycle phases (develop / distribute / deploy / runtime) and the 4Cs framing; RBAC (Role, ClusterRole, RoleBinding, ClusterRoleBinding, additive permissions, binding immutability, default roles); ServiceAccounts and TokenRequest; Secret types and hardening; encryption at rest; Pod Security Standards and Pod Security Admission; `securityContext`; supply-chain security (scanning, signing, SBOM, in-toto, TUF, Harbor); policy engines (OPA, Kyverno, Falco); sandboxed runtimes.
- **Prerequisites**: Ch 4 (namespaces, namespaced vs cluster-scoped, Secrets), Ch 5 (ServiceAccount as Pod identity, planted), Ch 8 (the admission gate), Ch 10 (NetworkPolicy). **See the PREREQ NOTE in frontmatter** — the real set is eight sections across six chapters, and only one of them is non-negotiable.
- **Retrieval targets**: **20%** **[B3]**, from Ch 7–11, with the **≥4-back spacing floor** satisfied several times over: **Ch 4 §3 (namespaced vs cluster-scoped, eight back)**, **Ch 4 §5 (selectors, eight back)**, **Ch 2 §3 (digests, ten back)**, **Ch 8 §2 (the admission gate, four back)**. Named anchors: NetworkPolicy (Ch 10) cross-beared as the network half of the security story rather than duplicated; ServiceAccount (Ch 5) collected from its planting.
- **Question budget**: 8 Soundings · **12–15 Bearings** (three checkpoints) · 21 Practice · **41–44 total**. Set at 15 Bearings below, per B4's "minimums to exceed" and the shape Chapters 3–11 shipped. Chapter total **44**.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: substantial.
- **Blocking gaps**: G5 (PSS/PSA, `securityContext`), G6 (4Cs), G7 (ServiceAccounts), G22 (supply chain), G23 (policy engines). **G7 status: CLOSED** — `k8s-docs-service-accounts-2026-08-23.md` covers the object, the `default` account and its near-zero permissions, the use cases, and the TokenRequest recommendation with the v1.22 boundary. **G23 status: CLOSED** — `kyverno-overview-2026-08-23.md` names OPA, Gatekeeper and Rego explicitly alongside Kyverno's own model, and `falco-overview-2026-08-23.md` covers runtime detection. **G5 status: OPEN and blocking §5 entirely.** **G6 status: OPEN, and it is an editorial decision rather than a fetch.** **G22 status: PARTIALLY OPEN.** See § Open questions #1–#4.
- **Note**: **[B3]** `ch12-fig02` must be *derived* from `ch04-fig04`, not presented as a memorization table — this is the payoff for cross-cutting theme #2. Pair `ch12-zenith` with Ch 10's NetworkPolicy additive semantics: two systems, one rule, no deny.

### Debts falling due in this chapter

**Twenty-four published cross-bearings point at Chapter 12** — the most of any chapter in the book — of which twelve name a section by number, plus four un-pointered promises in Ch 11's Voyage Ahead. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| `chapter-01` line 466 | *"Your reliable gaps are Chapter 8, Chapter 12, and Chapter 17"* — said to the experienced-developer reader in the reading-paths section | **Tone obligation, whole chapter.** A reader was told on page one that this is one of three chapters they most likely need. Do not open apologetically and do not pad; the promise was that the material is *unfamiliar*, not that it is hard |
| `chapter-02` line 393 | *"Ch 12 — signing, attestation, and the software supply chain"*, dropped on reproducible layers as *"the hinge on which supply-chain verification swings"* | **§7.** The hinge argument was already made; §7 completes it rather than restating it |
| `chapter-02` line 395 | *"Ch 12 — securing the image supply chain"*, with scanning, signing and bills of materials named | **§7.** Three named items; all three must appear |
| `chapter-02` line 459 | *"Ch 12 — restricting who can pull what"*, dropped on `imagePullSecrets` as *"a genuine security boundary rather than a convenience feature"* | **§7**, and §4 for the `dockerconfigjson` Secret type |
| `chapter-02` line 813 | *"Ch 12 — runtime protection for compute"*, on RuntimeClass and sandboxed runtimes as *"one control among several in the security lifecycle"* | **§1** names the runtime-compute area; **§5** refers back to Ch 2 §7 rather than re-teaching RuntimeClass. The phrase *"one control among several"* is the promise: §5 must show it sitting beside the others, not alone |
| `chapter-03` line 409 | *"Ch 12 — Secrets live in etcd, which is why encryption at rest is a separate decision you have to make"* | **§4.** The reader was given the *reason* nine chapters early; §4 supplies the mechanism |
| `chapter-04` line 565 | *"Ch 12 — deriving Role, ClusterRole, RoleBinding, and ClusterRoleBinding from this boundary"*, preceded by *"the four combinations are not a table to memorize"* | **§3, and this is the single most load-bearing debt in the chapter.** Ch 4 stated the derivation's premise in full — *"a permission over a cluster-scoped resource cannot be [granted inside one namespace], because there is no namespace to grant it in"* — so §3 owes the *conclusion*, not the premise again |
| `chapter-04` line 648 | *"Ch 12 — hardening Secrets, and the access-control model behind it"*, after Ch 4 explicitly withheld the fix: *"the lock is Chapter 12's; this chapter is only telling you the box did not ship with one fitted"* | **§4**, with §3 as the access-control half. Four items were enumerated there; all four land in §4 |
| `chapter-04` line 839 | *"Ch 12 — why RBAC names subjects instead of selecting them"*, with the warning that a reader who assumes otherwise *"will make a specific, confident, wrong prediction in Chapter 12"* | **§3.** The reader was promised an *explanation*, not just a correction. §3 owes the contrast with Ch 4 §5's everything-is-a-selector rule and a reason the exception exists |
| `chapter-04` line 1239 | *"Ch 12"* — dropped in an answer key on cluster-scoped resources belonging to *no* namespace rather than all of them, *"because 'in all namespaces' and 'in no namespace' imply very different things about who can be granted access"* | **§3.** This is graded material the reader has already been marked on; §3 must make the implication explicit |
| `chapter-05` line 779 | *"Ch 12 §2 — ServiceAccounts as RBAC subjects"* — **section-pinned**, and the promise enumerates FOUR things: what one can be granted, how RBAC binds permissions to it, how to harden its tokens, and the privilege-escalation path | **§2** (identity, tokens, hardening) and **§3** (what it can be granted, how binding works) and **§4** (the escalation path). Note the split: one promise, three sections. §2 should say where each half lands so the reader does not think something was dropped |
| `chapter-06` line 486 | *"Ch 12 — deleting a workload does not delete everything it referenced"*, dropped in the cascading-deletion and orphaning material | **§2**, and it is the easiest of the twenty-four to miss. The debt is: a deleted Deployment leaves behind its ServiceAccount, its Secrets and its RoleBindings. Identity and grants outlive the workload that used them, which is a stale-permission problem and one clause of least-privilege hygiene |
| `chapter-06` line 981 | *"Ch 12 — RBAC, where this permission model is taught"*, dropped on custom resources working with *"`kubectl get`, `kubectl describe`, `kubectl apply`, labels, selectors, namespaces, RBAC, all of it"* | **§3.** One clause: RBAC rules name custom resources exactly as they name built-in ones, because both live in the same API |
| `chapter-07` line 726 | *"Ch 12 — workload isolation"*, on dedicated nodes appearing *"later as an isolation control rather than a scheduling one"* | **§1** (the compute list includes partitioning workloads across nodes) and **§5**, with a back-bearing to Ch 7 §4. Do not re-teach taints |
| `chapter-08` line 426 | *"Ch 12 §3 — Role, ClusterRole, and the binding model"* — **section-pinned**, immediately after Ch 8 quoted the docs naming *"ABAC mode, RBAC Mode, and Webhook mode"* | **§3.** The ABAC exposure creates an obligation — see B7's orphan ruling and § Open questions #10 |
| `chapter-08` line 471 | *"Ch 12 §6 — Pod Security Standards and Pod Security Admission"* — **section-pinned**, with an unusually specific promise: *"when you meet Pod Security Admission four chapters from now, you will not be learning a new kind of thing. You will be learning one instance of the third gate"* | **§6.** The promise is a *derivation*, not a topic. §6 must open by discharging it — this is admission, which the reader already has — before any of the three levels appear |
| `chapter-08` line 577 | *"Ch 12 §3 — namespaced and cluster-scoped permissions"* — **section-pinned**, with *"Chapter 12 is going to derive the RBAC four-way matrix from exactly this boundary rather than asking you to memorize four combinations"* | **§3.** Two chapters have now promised the derivation in near-identical words. It is not optional and it is not a table |
| `chapter-08` line 967 | *"Ch 12 §4 — Secrets, and encryption at rest"*, with *"Chapter 12 covers why 'keep it encrypted' is not paranoia. It is the reason that clause is in the sentence"* | **§4.** The sentence in question was etcd backup guidance. §4 owes the connection: a backup of etcd is a backup of every Secret in the cluster, in the clear |
| `chapter-10` line 1035 | *"Ch 12 §5 — what a Pod may do to its node"* — **section-pinned**, drawn as the *other axis* from NetworkPolicy's L3/L4 reachability | **§5.** The two-axis framing is already in the reader's head; §5 fills the axis it named |
| `chapter-10` line 1201 | *"Ch 12 §9 — RBAC and NetworkPolicy as one shared semantic"* — **section-pinned** | **§9** |
| `chapter-10` line 1312 | *"Ch 12 §9 — additive, never deny"* — **section-pinned**, with *"Chapter 12 retrieves this exact semantic by name and builds an argument on it"* and an instruction to the reader to *"hold on to the phrasing about subtraction"* | **§9**, and the word to retrieve is **subtraction**, in Ch 10's phrasing. Do not coin a competing phrase |
| `chapter-11` line 440 | *"Ch 12 §5 — what a Pod may do to its node"* — **section-pinned**, on `hostPath` as *"the workload-to-host boundary problem, and… why an entire security apparatus exists to police it"* | **§5.** The reader was promised an *apparatus*, plural controls, not one field |
| `chapter-11` line 444 | *"Ch 12 §4 — Secrets are not encrypted"* — **section-pinned**, closing with *"File over environment variable is half an argument already, and you now hold that half"* | **§4.** The half the reader holds is the tmpfs fact. §4 supplies the other half and must say plainly which half was which; re-deriving the tmpfs point wastes the setup |
| `chapter-11` line 896 | *"Ch 12 §5 — what a Pod may do to its node"* — **section-pinned**, on an access mode not being a permission system | **§5** |
| `chapter-11` lines 1632–1641 (Voyage Ahead) | Four promises: (a) the chapter's question is *"what is a workload allowed to do, and who decided?"*; (b) the tell — *"the permission system you are about to learn has no way to say no. None."*; (c) *"by the end of the next chapter you will understand **why** two systems built for entirely different purposes arrived at the same design, and why that design is a feature rather than an omission"*; (d) *"Bring the `secret` volume with you. Chapter 12 §4 has an argument to make"* | (a) the whole chapter, and it is the right one-line statement of what §1–§6 are for; (b) **§3**, which must not act surprised — the reader was told; (c) **§9, and this is a commitment to an explanation, not a restatement** — see § Open questions #5; (d) **§4** |

### What this chapter owes forward

| Owed to | What must be plantable | Where it is planted |
|---|---|---|
| **Ch 13 §2** | A Pod that will not start because a referenced Secret or ConfigMap is missing, and a Pod rejected outright by admission rather than failing to start | §4 (Secret consumption) and §6 (enforce mode *rejects*, which is a different failure shape from a crash — Ch 13 will need the distinction) |
| **Ch 15 §4** | The delivery agent's own identity — its ServiceAccount and the permissions it must hold. Argo CD reconciles a cluster, which means it holds broad grants | §2 and §3. §2 must make "an in-cluster agent is a subject like anything else" available without naming Argo CD |
| **Ch 16 §3** | `kubectl debug` and ephemeral containers interact with a `restricted` namespace — a debug container can be refused by admission | §6, one clause. Plant, do not resolve |
| **Ch 17 §4** | Admission webhooks as an extension point, collected with the four pluggable interfaces | §8, where a policy engine *is* an admission webhook |
| **Ch 17 §5** | mTLS and zero trust — workload identity plus encryption in transit plus policy, at the infrastructure layer | §2 (workload identity), §4 (encryption **at rest** is a different decision from encryption **in transit** — say so once, here, so Ch 17 can build on it), §8 (policy as an infrastructure concern) |
| **Ch 19 §2** | Two confusion pairs for the matrix: PSS *levels* versus PSA *modes*; Role versus ClusterRole as objects versus RoleBinding versus ClusterRoleBinding as scope-setters | §6 and §3 |

---

## 1. Why This Chapter Matters

*Planning notes for drafting — not prose.*

**The curiosity gap.** Ch 11 pre-loaded it and named it precisely: *what is a workload allowed to do, and who decided?* Do not re-open a new one — inherit that one and hold it open. The specific gap that stays unresolved until §9 is the one Ch 11 planted as a tell: the reader has been told that Kubernetes' permission system has no way to say no, and told that they have already seen one other system with the same property. What they have not been told is **why**, and they were promised that answer explicitly. Everything from §2 to §8 is evidence; §9 is the argument.

**The identity frame.** The move this chapter teaches is the one that separates a person who can *use* a cluster from a person who can be trusted with *someone else's*. Every control in this chapter is an answer to a question a platform team gets asked in an audit, and the reader who can name which control answers which question is doing the job. Frame it that way rather than as a list of security features — the 4Cs and the lifecycle phases exist precisely because practitioners kept solving one layer and shipping the other three.

**The stakes.** Honest and specific, stated once. Two of this chapter's Fixed Points are things a competent engineer will get wrong on a real cluster: that a Secret is protected because it is base64-encoded, and that a namespace with a `view` RoleBinding is a safe place to let someone look around. Both are wrong in ways that are invisible until they are not. Say that plainly, once, without a breach anecdote — Part 14's subject-dignity guardrail applies here more than anywhere else in the book, and the wry register in this chapter stays aimed at *us*, never at anyone on the wrong end of a real incident.

**Dead Reckoning + Extended Analogy.** The chapter needs both, and the Extended Analogy is load-bearing rather than decorative because the chapter's title already commits to it. Dead Reckoning: security in Kubernetes is not one system; it is five independent systems that answer five different questions — *who are you*, *what may you do*, *what is stored where*, *what may your workload do to the machine*, and *what did you ship* — and no one of them substitutes for another. Extended Analogy: the ship's locks, keys and watchstanders — the key is not the permission (a key opens a lock; the *manifest of who holds which key* is the permission), the strongbox is not the safe, and the watch does not prevent anything, it reports. Keep it to one sidebar. The title is already carrying the metaphor and a second sidebar would be theme-dressing.

---

## 2. What You'll Learn

Five to six outcomes, active verbs, one with a wry parenthetical per Part 15:

- **Place** any Kubernetes security control on two maps at once — which layer it protects and which lifecycle phase it acts in — and say which of the two the exam is asking about.
- **Distinguish** an identity from a permission, and name the two separate objects Kubernetes keeps them in.
- **Derive** which of Role, ClusterRole, RoleBinding and ClusterRoleBinding a situation calls for, from the namespaced/cluster-scoped boundary you already have, rather than from a memorized table.
- **State** what protects a Secret, what does not, and the three ways someone reads one anyway (one of which is simply being allowed to create a Pod, which is not usually thought of as a permission to read secrets).
- **Read** a `securityContext` and a namespace's Pod Security labels together, and predict whether a given Pod is admitted, warned about, or refused.
- **Trace** an image from build to running container and name the checkpoint at each handoff, including which one a signature actually covers.

*Closing line, per house form:* You will also finish an argument Chapter 10 started and Chapter 11 refused to settle — why two Kubernetes systems built for entirely unrelated purposes both refuse to let you say no.

---

## 3. Soundings plan

Eight questions, per the content-chapter baseline. Rubric is the standard 6+ / 3–5 / 0–2 — **but per the PREREQ NOTE the 0–2 branch names sections, and singles out one.** Suggested 0–2 wording: *"Re-read Ch 4 §3 before you start this chapter — not alongside it, before it. Section 3 below is built as a derivation from that boundary and two earlier chapters have already promised you it would be. Ch 5 §6 (a Pod's identity), Ch 8 §2 (the three gates) and Ch 10 §6 (allowing, never denying) can be re-read as you reach the sections that need them."*

| # | Topic | Prerequisite / intuition tested | Why it works as a pre-test |
|---|---|---|---|
| 1 | Can a permission over a cluster-scoped resource be granted "inside one namespace"? Why is the answer forced rather than chosen? | **Ch 4 §3** (graded there) + **Ch 8 §5** | Retrieval at eight-back, satisfying the ≥4-back floor inside the Soundings at zero budget cost. The *why* clause is the real question: a reader who can only state the fact will find §3's derivation surprising; a reader who can state the reason will find it inevitable, which is what the derivation is for |
| 2 | A Pod's manifest names no ServiceAccount. What identity does it run as, and where did that identity come from? | **Ch 5 §6**, verbatim material | The early-easy-win, placed second per the dopamine schedule. It also primes §2's Fixed Point without stating it: the reader will answer "the `default` ServiceAccount" and will *not* be asked what that account can do, which is precisely the gap §2 opens |
| 3 | What does base64 do to a Secret's value, and what does it not do? | **Ch 4 §4**, which stated this outright and put it in its Chapter Summary | Confirms the reader still holds the fact Ch 4 planted. A reader who has quietly drifted back to "encoded means protected" in eight chapters gets that surfaced *before* §4 corrects it, which is the pretesting effect doing its actual job |
| 4 | Name the three gates an API request passes, in order. Which runs last? | **Ch 8 §2**, verbatim material | Sets up §6's derivation. Ch 8 line 471 promised the reader they would recognize Pod Security Admission as an instance of the third gate; this question checks whether they still hold the gate to recognize it *with* |
| 5 | Can one NetworkPolicy deny traffic that another NetworkPolicy allows? | **Ch 10 §6**, verbatim material | Four-back retrieval on Ch 10's own Fixed Point. **See the FIXED-POINT SPOILER CHECK ruling: stem and answer key stay entirely inside NetworkPolicy.** Its job is to have the semantic *loaded* when §9 reaches for it, not to preview §3 |
| 6 | In a permission system you have actually used — Unix modes, cloud IAM, a Windows ACL — can one rule subtract access that another rule grants? | General professional prior; no chapter | This is the question that makes §3 land. Most permission systems the reader knows *do* have deny, and several are famous for the order-dependence it creates. Establishing that expectation is what turns Kubernetes' answer from an arbitrary rule into a design choice worth explaining. Poses nothing about Kubernetes and reveals nothing |
| 7 | What does a signature on a software release prove, and what does it not prove? Would a signature covering a tag mean the same thing as one covering a digest? | General professional prior + **Ch 2 §3** retrieval at ten-back | The second clause is the whole question, and it is the deepest retrieval in the chapter. Ch 2 taught tags as mutable pointers and digests as identity as a *hygiene* matter; §7 reveals it was a security matter. This question makes the reader do the connecting before the section does it for them |
| 8 | A process runs as root inside a container. Is that the same root as the node's? What does Ch 2 §1 tell you that bears on the answer? | General professional prior + **Ch 2 §1** (namespaces and cgroups as the isolation primitives) | The misconception §5 exists to correct, surfaced before the correction. A reader who says "no, it's isolated" and a reader who says "yes, it's UID 0 either way" are wrong in opposite directions, and §5 needs both wrong answers in play. Names no `securityContext` field, so no Fixed Point is touched |

**Spoiler audit: clean, with one recorded ruling on Q5.** See the FIXED-POINT SPOILER CHECK block in frontmatter for the per-question reasoning.

---

## 4. Section plan

Nine sections, seven arcs. This chapter is **not** one ladder the way Ch 11 was, and drafting should not try to make it one — the material genuinely is several independent systems that share a domain. What holds it together is a single question asked of each system in turn (*who decided, and can they be overruled?*), and §9's answer to it.

The order is not arbitrary: §2–§3 are identity then permission, which is the order the API evaluates them in; §4–§6 walk outward from the object to the workload to the namespace; §7–§8 leave the cluster and come back. §1 supplies the map for all of it.

---

### §1 — ⚪ Four Layers and Four Phases

**Must cover.** The two framings and how they overlay. The **cloud native security lifecycle phases** — develop, distribute, deploy, runtime — as kubernetes.io currently presents them, with the runtime phase's three areas (access, compute, storage) called out because they are this chapter's own table of contents. The **4Cs** — Cloud, Cluster, Container, Code — as the layer framing. The distinction that makes both worth having: **the phases are a *when*, the layers are a *where*.** Close by mapping the rest of the chapter onto both, explicitly, so the reader knows where they are going.

**Objectives.** D2.2.

**Introduces.** cloud-native-security-lifecycle · develop-phase · distribute-phase · deploy-phase · runtime-phase · runtime-protection-access · runtime-protection-compute · runtime-protection-storage · four-cs.

**Figure.** `ch12-fig01-4cs-and-lifecycle-phases`.

**Fixed Point.** The phases answer *when* a control acts; the layers answer *where* it acts. A control has a position on both maps, and a question that seems to be about one is often about the other.

**Debts paid.** `chapter-02:813` (runtime protection for compute, named as an area), `chapter-07:726` (partitioning workloads across nodes appears in the compute list).

**Cross-bearings out.** Forward, all internal: §2 (runtime/access), §4 (runtime/storage), §5 (runtime/compute), §7 (distribute). Forward to Ch 15 — the deploy phase's *"restrictions on what can be deployed, who can deploy it, and where"* is a description of GitOps before the reader has the word. Back: Ch 2 §7 (RuntimeClass sits in runtime/compute), Ch 8 §3 (ResourceQuota and LimitRange appear in the compute list, which recontextualizes them as security controls rather than only fairness controls — a genuinely useful re-frame, one clause).

**Checkpoint after.** No.

**Note.** **BLOCKING — see § Open questions #1.** The cached snapshot of the kubernetes.io page records that the page *replaced* the 4Cs framing with the lifecycle phases. This section's title, its figure anchor and the arc outline all assume both. Do not draft §1 until that decision is made.

**Note.** Resist making this a security-vocabulary dump. §1's job is a map, and a map that names twelve controls the reader cannot yet place is not a map. Name the areas; let the sections fill them.

---

### §2 — ⚪ Who You Are

**Must cover.** ServiceAccount as the cluster's non-human identity: an object in the API server, **namespaced**, lightweight, portable, and distinct from a user account — which Kubernetes does not store at all. Every namespace gets a `default` ServiceAccount on creation, replaced by the control plane if deleted, and assigned to any Pod that does not name one. **The `default` account has no permissions beyond the API discovery that every authenticated principal gets.** `spec.serviceAccountName`. Credentials: since v1.22 the recommended path is a short-lived, automatically rotating token from the **TokenRequest** API, mounted as a projected volume; long-lived ServiceAccount token Secrets neither expire nor rotate and are a legacy risk. Users and groups as *external* identities that arrive at the authentication gate from outside. Close by naming **subject** and handing to §3.

**Objectives.** D2.2.

**Introduces.** serviceaccount-as-subject · rbac-subject · default-serviceaccount-permissions · user-and-group-external-identity · service-account-token · tokenrequest · projected-token-volume · long-lived-token-secret-legacy · service-account-name-field · orphaned-identity.

**Figure.** `ch12-fig03-serviceaccount-token-flow`.

**Fixed Point.** An identity and a permission are two different things, kept in two different objects. The `default` ServiceAccount proves it: every Pod in the cluster has an identity, and almost none of them can do anything with it.

**Trap.** B1 #62 — token Secrets are not current best practice; TokenRequest is.

**Debts paid.** `chapter-05:779` (**pinned**) — and note this promise enumerates four things across three sections; §2 should say where each lands. `chapter-06:486` — the ServiceAccount, its Secrets and its RoleBindings survive the workload that used them; stale identity is a least-privilege problem.

**Cross-bearings out.** Back: Ch 5 §6 (the object, planted there and collected here — *collect*, do not re-teach), Ch 8 §2 (authentication is the first gate; this is what arrives at it), Ch 11 §1 (the projected volume the reader met carrying exactly this token). Forward: Ch 15 §4 (a delivery agent is a subject like anything else) — plant without naming Argo CD; Ch 17 §5 (workload identity is the first leg of zero trust).

**Checkpoint after.** No.

**Note.** JWT and OIDC per B7 are **name-and-scope only**; the glossary owns the definitions. Sigstore's keyless flow in §7 uses an OIDC identity token, which is the one place the acronym does real work — name it there, not here.

---

### §3 — 🔵 What You May Do

**Must cover.** RBAC as *an* authorization mode, not *the* authorization mechanism — one clause, discharging the ABAC exposure Ch 8 created (§ Open questions #10). The `rbac.authorization.k8s.io` API group. **Role** (namespaced, and you must state the namespace) versus **ClusterRole** (non-namespaced), with the documentation's three ClusterRole uses. **RoleBinding** versus **ClusterRoleBinding**, and the fact that a RoleBinding may reference *either* a Role in its namespace *or* a ClusterRole, binding that ClusterRole into its namespace. **Then the derivation**: the four combinations fall out of Ch 4 §3's boundary, and the rule they fall out to is *the binding determines the scope of the grant*. Rules as verbs over resources — including custom resources, identically. Aggregated ClusterRoles. The four default user-facing roles and, for each, **what it cannot do**. Permissions are purely additive; there are no deny rules. A binding cannot be retargeted after creation. Least privilege as the practice all of this exists to make possible.

**Objectives.** D2.2.

**Introduces.** rbac · authorization-mode · role · clusterrole · rolebinding · clusterrolebinding · four-way-binding-matrix · binding-determines-scope · rule-verb-resource · subjects-are-named-not-selected · aggregated-clusterrole · default-role-cluster-admin · default-role-admin · default-role-edit · default-role-view · additive-permissions · no-deny-rule · binding-immutability · least-privilege.

**Figure.** `ch12-fig02-rbac-four-way-matrix` — **derived from `ch04-fig04`, not a memorization table.** [B3] This is the payoff for cross-cutting theme #2 and the figure must show its work: the boundary on the left, the four cells falling out of it on the right, with the derivation arrow visible. A four-cell grid with labels is the failure mode.

**Fixed Points.** Three, which is the most in any section of the book and is correct here:
1. **The binding determines the scope of the grant.** A ClusterRole bound by a RoleBinding grants that ClusterRole's permissions *inside one namespace only* — including `cluster-admin`, which is the trap.
2. **Permissions are purely additive. There is no deny rule.** Removing access means removing the grant.
3. **A binding cannot be retargeted.** After creation you cannot change which Role or ClusterRole it refers to.

**Dead Reckoning.** The four objects and the four default roles, stated flat, with no register and no metaphor. This section has the highest pure-recall density in the chapter and the reader deserves one block that is just the facts.

**⚠ Navigational Hazards.** Two: the no-deny-rule consequence (you cannot carve an exception out of a grant), and binding immutability (the fix is delete and recreate, which is a different operation with different consequences under GitOps — a plant for Ch 15).

**Traps.** B1 #53, #54, #55, #56, #57, #58, #59 — seven sourced traps, the densest cluster in the book's inventory. All seven are examinable and all seven belong here.

**Debts paid.** `chapter-04:565` (**the derivation**), `chapter-04:839` (why subjects are named, not selected), `chapter-04:1239` (in-no-namespace versus in-all-namespaces), `chapter-06:981` (RBAC covers custom resources identically), `chapter-08:426` (**pinned**), `chapter-08:577` (**pinned** — the derivation, promised twice), `chapter-05:779` (the "what one can be granted" half).

**Cross-bearings out.** Back: **Ch 4 §3** — a *use*, never a restatement; the whole section is built on it. **Ch 4 §5** — the deliberate contrast, and the debt at `chapter-04:839`: everything in Kubernetes is a selector *except this*, and §3 owes the reason. A selector is a query evaluated continuously against a changing set; a grant of privilege that silently expands when someone adds a label is not a grant anyone can audit. Ch 8 §2 (this is the second gate). Forward: §4 (what the `view` role cannot see, and why that matters), §9.

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #1.**

**Note.** **Open by disposing of the `binding` collision** — see Chapter-type note. One sentence, before any RBAC material.

**Note.** The reader already knows the no-deny fact; Ch 11's Voyage Ahead told them. §3 must state it as *confirmation of a thing they were promised* rather than as a reveal. Acting surprised at a fact you handed the reader a chapter ago reads as either forgetfulness or theatre, and the brand voice does neither.

---

### §4 — 🔵 Secrets Are Not Encrypted

**Must cover.** Retrieval, not restatement, of base64 as encoding (Ch 4 §4). **Secrets are stored unencrypted in etcd by default.** The three exposure paths: anyone with API access, anyone with etcd access, and **anyone able to create a Pod — or a Deployment — in the namespace**. Encryption at rest: what `EncryptionConfiguration` is, what it protects (the object as written to etcd) and what it does not (the object as returned by the API to an authorized caller). The hardening list, all four items Ch 4 promised: enable encryption at rest; least-privilege RBAC on Secrets specifically; restrict Secret access to specific containers; consider an external secret store. **File mounts over environment variables**, completing the argument Ch 11 §1 started. Secret types enumerated — Opaque, `service-account-token`, `dockercfg`, `dockerconfigjson`, `basic-auth`, `ssh-auth`, `tls`, bootstrap token.

**Objectives.** D2.2.

**Introduces.** base64-is-encoding (retrieved) · secret-storage-default-unencrypted · secret-exposure-paths · pod-creation-privilege-escalation · encryption-at-rest · encryptionconfiguration · secret-hardening · file-mount-over-env-var · external-secret-store · secret-type.

**Figure.** None — see § Open questions #7.

**Fixed Points.** Two:
1. A Secret is stored unencrypted in etcd by default. Encryption at rest is opt-in and is a cluster-operator decision, not a manifest field.
2. **Anyone authorized to create a Pod in a namespace can read every Secret in that namespace** — including indirectly, by creating a Deployment. This is the exposure path nobody thinks of as a permission to read secrets.

**⚠ Navigational Hazards.** The Pod-creation escalation path. It is the chapter's single most consequential practical fact and it is invisible in any RBAC audit that reads only `get secrets`.

**Traps.** B1 #60, #61. Plus the `view`-cannot-read-Secrets fact retrieved from §3 one section back — a deliberate short-spacing retrieval, which is the only one in the chapter and is justified because the two facts are two halves of the same audit question.

**Debts paid.** `chapter-03:409` (Secrets live in etcd, hence a separate decision), `chapter-04:648` (all four hardening items), `chapter-08:967` (**pinned** — and the specific connection: an etcd backup is a copy of every Secret in the cluster, in the clear, which is why the backup guidance said to keep it encrypted), `chapter-11:444` (**pinned** — file over env var; the reader holds the tmpfs half), `chapter-02:459` (the `dockerconfigjson` type), `chapter-05:779` (the escalation-path quarter of that promise).

**Cross-bearings out.** Back: Ch 4 §4 (base64, and the strongbox-without-a-lock framing Ch 4 used — reuse the image, it was good and it was theirs), Ch 3 §2 (etcd), Ch 8 §7 (etcd backup), Ch 11 §1 (tmpfs-backed `secret` volumes — the half they hold). Forward: Ch 13 §2 (a missing Secret is a Pod that never starts), Ch 17 §5 (encryption **in transit** is a different decision from encryption **at rest** — state the distinction once, here).

**Checkpoint after.** No.

**Note.** Ch 4 explicitly withheld the fix and said so — *"the lock is Chapter 12's."* Open by picking that up, not by re-alarming the reader. The alarming was done well eight chapters ago and repeating it is both padding and, per Part 14, drifting toward fear-framing when the reader has already agreed to be worried.

---

### §5 — 🔵 What a Pod May Do to Its Node

**Must cover.** `securityContext` at **Pod scope and container scope**, and that the container's setting wins where both are present. The fields that matter at associate tier: `runAsUser` / `runAsGroup` / `runAsNonRoot`; `privileged`; Linux **capabilities** (dropped and added); `readOnlyRootFilesystem`; `allowPrivilegeEscalation`. `seccomp` and **AppArmor** as the Linux security modules the security documentation names by name. The framing that ties them: by default a process running as root in a container is UID 0 as far as the kernel is concerned, and every field above is a way of making that less true. Then the apparatus around it — **refer** to Ch 2 §7 for RuntimeClass and sandboxed runtimes rather than re-teaching, and **refer** to Ch 7 §4 for node partitioning as an isolation control.

**Objectives.** D2.2.

**Introduces.** securitycontext · pod-scope-vs-container-scope · run-as-non-root · run-as-user · privileged-container · linux-capabilities · read-only-root-filesystem · allow-privilege-escalation · seccomp · apparmor · workload-to-host-boundary.

**Figure.** None by design — the fields taught here are shown in `ch12-fig04` in §6, against the levels that constrain them. See § Open questions #7.

**Fixed Point.** `securityContext` governs the **workload-to-host** axis. NetworkPolicy governs the **workload-to-workload** axis. They are different systems, they fail independently, and neither substitutes for the other — which Ch 10 told the reader was true and this section is the proof of.

**⚠ Navigational Hazards.** `privileged: true`. The Pod Security Standards' own definition of the `privileged` level is *"an absence of restrictions"* permitting a Pod to *"bypass typical container isolation mechanisms"* — quote it rather than editorializing, and let §6 make the consequence.

**Debts paid.** `chapter-10:1035` (**pinned** — the other axis), `chapter-11:440` (**pinned** — `hostPath` and the *apparatus*, plural), `chapter-11:896` (**pinned** — an access mode is not a permission system, and the docs' own sentence names `securityContext` as the thing that *is*), `chapter-02:813` (one control among several), `chapter-07:726` (workload isolation via dedicated nodes).

**Cross-bearings out.** Back: Ch 2 §1 (Linux namespaces and cgroups are what these fields tune), Ch 2 §7 (RuntimeClass and sandboxed runtimes — *refer*), Ch 7 §4 (taints as an isolation control — *refer*), Ch 10 §6 (the other axis), Ch 11 §1 (`hostPath`, whose warning was about credentials and escape, not disk). Forward: §6 (every field here is something a level constrains).

**Checkpoint after.** No.

**Note.** **BLOCKING — G5 is wide open and this section cannot be drafted.** See § Open questions #2.

**Note.** Write **"Linux namespace"**, never bare, throughout — §3 and §6 are both discussing the Kubernetes Namespace within a few pages.

**Note.** Acknowledge in one clause that the reader has already seen the word `securityContext`, in Ch 11's quoted storage documentation. Free retrieval; costs a sentence.

---

### §6 — 🔵 Three Levels, Three Modes

**Must cover.** **Open with the derivation Ch 8 promised**: this is the third gate, which the reader already has. Then the **Pod Security Standards** — three policies, cumulative, ranging from highly permissive to highly restrictive: `privileged` (unrestricted, for system- and infrastructure-level workloads run by trusted users), `baseline` (minimally restrictive, prevents known privilege escalations, allows the default minimally-specified Pod), `restricted` (current hardening best practice, at the cost of some compatibility). Then **Pod Security Admission**, the built-in controller that enforces them, applying a policy **per namespace** via labels of the form `pod-security.kubernetes.io/<MODE>: <LEVEL>`, where MODE is `enforce` (violations rejected), `audit` (violations recorded in the audit log) or `warn` (violations produce a user-facing warning). **Levels and modes are orthogonal** — one namespace can carry all three modes at three different levels, which is how a cluster migrates without breaking. PodSecurityPolicy named once, as removed and superseded.

**Objectives.** D2.2.

**Introduces.** pod-security-standards · pss-privileged · pss-baseline · pss-restricted · pod-security-admission · psa-enforce · psa-audit · psa-warn · namespace-label-control-surface · podsecuritypolicy-removed.

**Figure.** `ch12-fig04-pod-security-standards-levels` — **build it as levels against the `securityContext` fields they constrain**, so it does double duty for §5 and makes the levels concrete rather than adjectival. A figure that shows only three boxes labelled privileged/baseline/restricted teaches nothing the sentence did not.

**Dead Reckoning.** Three levels, three modes, the label form. Stated flat.

**Fixed Point.** Three levels × three modes, applied per namespace by label. **The level says *what* is checked; the mode says *what happens* when the check fails.** They are independent axes and confusing them is the chapter's most likely wrong answer.

**Trap.** Level/mode confusion — mark `[inferred]`, not `[source]`, per Ethical Guardrail #8 and B2's standing instruction. B1's inventory does not carry it.

**Debts paid.** `chapter-08:471` (**pinned** — and the promise was a *derivation*: "you will not be learning a new kind of thing").

**Cross-bearings out.** Back: **Ch 8 §2** (the third gate — the primary retrieval anchor of this section), Ch 4 §3 (the namespace as the control surface, which is a new job for an object the reader knows), §5 (the fields the levels constrain). Forward: Ch 13 §2 (a Pod *rejected* by admission has a different failure shape from a Pod that starts and dies), Ch 16 §3 (a debug container can be refused by a `restricted` namespace — plant, do not resolve), Ch 17 §4 (admission as an extension point).

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #2.**

**Note.** PodSecurityPolicy gets **one clause and no more**, per B7's orphan ruling, and is eligible as a *wrong option* in a PSA item and never as a correct one. It earns the clause because it saturates pre-2025 prep material, which B2 disclosure #3 already commits the book to warning about.

---

### §7 — 🟡 Trusting What You Ship

**Must cover.** The distribute phase as a chain of checkpoints, in order: **scan** (known vulnerabilities, CVEs), **sign** (attestation of origin), **record** (a transparency log), **verify** (at admission, before the image runs), **restrict** (a private registry that only authorized clients may pull from). Image scanning and what a CVE is. Signing and attestation via Sigstore: **Cosign** (the client), **Fulcio** (short-lived certificates bound to a verified identity rather than long-lived keys), **Rekor** (the immutable append-only transparency log), and keyless signing as the flow that ties them. **What a signature binds to** — the artifact's digest. SBOMs as a signable artifact class. `in-toto`, TUF, Notary and Harbor named as the further instances the ecosystem uses. Private registries and `imagePullSecrets` as the restrict step.

**Objectives.** D2.2.

**Introduces.** supply-chain-security · image-scanning · cve · image-signing · attestation · provenance · signature-binds-to-digest · sbom · sigstore · cosign · fulcio · rekor · keyless-signing · transparency-log · in-toto · tuf · notary · harbor · private-registry-restriction.

**Figure.** `ch12-fig05-supply-chain-checkpoints`.

**Fixed Point.** **A signature binds to a digest, not a tag.** Chapter 2 taught that a tag is a mutable pointer and a digest is identity, and framed it as build hygiene. It was not hygiene. It is the reason a signature means anything at all.

**Debts paid.** `chapter-02:393` (reproducible layers as the hinge — the argument was made there; complete it, do not repeat it), `chapter-02:395` (scanning, signing, bills of materials — three named items, all three appear), `chapter-02:459` (restricting who can pull what).

**Cross-bearings out.** Back: **Ch 2 §3** (tags versus digests — the chapter's deepest retrieval, and the one most likely to produce a genuine ☀️ reaction outside the Zenith itself), Ch 2 §2 (layers and reproducibility), Ch 2 §6 (`imagePullPolicy` and pull secrets), §1 (the distribute phase this section fills). Forward: §8 (Sigstore's Policy Controller is a policy engine; verification *happens* at admission).

**Checkpoint after.** No.

**Note.** **PARTIALLY BLOCKED — G22.** Signing is fully sourced; SBOM, in-toto, TUF, Notary, Harbor and image scanning are not. See § Open questions #4, which also recommends organizing this section by **checkpoint** rather than by project roster.

**Note.** 🟡 is deliberate. B1's 114-trap inventory contains **zero** supply-chain traps, which is the best evidence available that this material is tested at recognition depth rather than discrimination depth. Teach it as a chain the reader can name, not as a set of projects the reader can compare.

---

### §8 — 🔵 Rules That Watch

**Must cover.** Policy engine as a category, and the distinction that organizes the section: **when does the rule run?** At admission — **Kyverno** (policies as Kubernetes resources in YAML and CEL, able to validate, mutate, generate and clean up, plus verify images and metadata; deployable as an admission webhook or as a CLI scanner) and **OPA** with its **Gatekeeper** admission controller (policy expressed in **Rego**). After admission, at runtime — **Falco** (observes kernel events and syscalls, enriches them with container and Kubernetes metadata, evaluates against a rules engine, emits alerts; typical detections include privileged-container escalation, namespace manipulation, writes to `/etc`, and shells spawned inside containers). **How these exceed §6**: Pod Security Admission answers a fixed question extremely well; a policy engine answers an arbitrary question at the same gate. Falco answers a different question at a different time, and answers it by *reporting*, not preventing.

**Objectives.** D2.2.

**Introduces.** policy-engine · opa · gatekeeper · rego · kyverno · validate-mutate-generate · falco · runtime-detection · admission-time-vs-runtime.

**Figure.** None — see § Open questions #7.

**Cross-bearings out.** Back: **Ch 8 §2** (mutating versus validating admission webhooks — a policy engine *is* one, which is the cleanest possible payoff for that distinction), §6 (the fixed question versus the arbitrary one), §7 (Sigstore's Policy Controller enforces signature verification at exactly this gate). Forward: Ch 17 §4 (admission webhooks collected as an extension point).

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #3.**

**Note.** G23 is CLOSED; this section is draftable now. The Kyverno snapshot names OPA, Gatekeeper and Rego in its own text, which means the OPA material is sourced without a second fetch.

**Note.** Do not use **eBPF**. B7 rules it glossary-only and not eligible for graded text, and the Falco source describes the mechanism as kernel events and syscalls without needing the word. Naming it here would create a fourth chapter with a claim on an unowned term.

---

### §9 — ☀️ Additive, Never Deny

**Must cover.** The synthesis, and **no new material whatsoever**. Two systems — RBAC, which governs what an identity may ask the API for, and NetworkPolicy, which governs which Pod may open a connection to which — built by different people for unrelated purposes, at different layers, on different objects. Both are purely additive. Neither has a deny rule. Both are configured by many authors at once, in a cluster whose contents change without anyone's involvement, and in both the removal of access means the removal of a grant rather than the addition of a prohibition. Close the Ch 11 hook explicitly and by name, using Ch 10's word: **subtraction**.

**Objectives.** D2.2.

**Introduces.** one-shared-semantic. Nothing else.

**Figure.** `ch12-zenith-additive-never-deny`. The figure's job is *rhyme*: two systems, side by side, at different layers, with the same shape. It should be visually parallel in the way `ch15-zenith` will be parallel to `ch03-fig02`.

**Cross-bearings out.** Back: **Ch 10 §6** (*refer*, do not restate — NetworkPolicy is taught once and this is not the second time), **Ch 10 §7** (what NetworkPolicy cannot do, which includes explicit deny), §3 (RBAC's additive rule). No forward pointers; this is a closing.

**Checkpoint after.** No. Exam Alert follows.

**Note — the honesty constraint, and it is the most important note in this outline.** Ch 11's Voyage Ahead promised the reader they would *understand why* two systems arrived at the same design and *why that design is a feature rather than an omission*. The book is committed to an explanation. **But no cached source states a design rationale for either system's additive semantics.** Both sources state the property; neither states the reason. Ethical Guardrail #4 forbids claiming certainty where legitimate uncertainty exists, and Guardrail #5 requires acknowledging where the book is simplifying or reasoning rather than reporting.

So §9's argument must be **explicitly and visibly the author's**, in the book's established uncertainty-signal form — something in the shape of *"the documentation states the property and does not explain it; here is the reading that makes the best sense of it, offered as a reading"* — followed by the argument, which is available and is good: a deny rule makes the effect of a grant non-local. With deny, you cannot know what a grant does without reading every other rule that might contradict it, and evaluation order becomes semantics. In a system where rules are written by many teams and evaluated against a set of objects that changes without anyone's involvement, additive-only is what makes a single rule readable in isolation. That reasoning is defensible and it is not sourced, and §9 must say which of those two things it is.

This is also the honest answer to *"a feature rather than an omission"*, and it should not be oversold. The cost is real and §9 should name it: you cannot carve an exception out of a grant, and sometimes an exception is exactly what you want.

---

## 5. Taking Your Bearings checkpoints

Three checkpoints of five, total **15**, exceeding B4's minimum of 10 per the arc outline's explicit override for this chapter. Placement matches the section plan: after §3, §6 and §8.

Each checkpoint has a theme rather than being a grab-bag of the sections it follows: **#1 who may act and how we know**, **#2 what the workload gets and what it may do**, **#3 what you trust and what watches**.

**Retrieval-practice load: 3 of 15 = 20%**, the Ch 5+ target exactly.

### ☆ Taking Your Bearings #1 — after §3

Covers §1–§3. Five questions.

| # | Tests | Retrieval? |
|---|---|---|
| 1 | Placing a named control on both maps — which layer, which phase | — |
| 2 | The `default` ServiceAccount: a Pod has an identity and can do nothing with it | — |
| 3 | **The derivation.** A scenario requiring a ClusterRole bound by a RoleBinding, answerable only by reasoning from the namespaced/cluster-scoped boundary. Trap answers built from B1 #54 and #55 | **Yes — Ch 4 §3, eight-back** |
| 4 | Binding immutability, and what you actually do about it (B1 #56) | — |
| 5 | The default roles: what `view` and `edit` each cannot do (B1 #57, #58) | — |

### ☆ Taking Your Bearings #2 — after §6

Covers §4–§6. Five questions.

| # | Tests | Retrieval? |
|---|---|---|
| 1 | The Pod-creation exposure path, posed as an audit scenario: an RBAC review shows nobody has `get secrets`, and the Secrets are still readable (B1 #61) — **the chapter's designated challenge item; label it as such per Part 10B** | — |
| 2 | What encryption at rest protects and what it does not | — |
| 3 | Pod-scope versus container-scope `securityContext`, and which wins | — |
| 4 | Level versus mode: a namespace labelled with two modes at two levels; predict the outcome for a given Pod | — |
| 5 | **Pod Security Admission as an instance of the third gate**, answerable from Ch 8 §2 plus §6 | **Yes — Ch 8 §2, four-back** |

### ☆ Taking Your Bearings #3 — after §8

Covers §7–§8, with one deliberate long-spacing item back to §3. Five questions.

| # | Tests | Retrieval? |
|---|---|---|
| 1 | **What a signature covers, and why a tag would not do** | **Yes — Ch 2 §3, ten-back; the deepest retrieval in the chapter** |
| 2 | The checkpoint chain in order, from build to running container | — |
| 3 | Where a policy engine sits relative to Pod Security Admission, and what it buys | — |
| 4 | Admission-time versus runtime: which tool answers which question, and what Falco does *not* do | — |
| 5 | Spaced item back to §3: the additive rule, applied to a "remove this one permission" request | — (within-chapter spacing, not counted against the retrieval budget) |

---

## 6. Exam Alert plan

**High-priority topics** — the six that carry the most weight per unit of study:

1. **The four-way matrix**, stated as a rule rather than a table: the binding determines the scope of the grant. The single highest-yield fact in the chapter.
2. **RBAC is additive with no deny rule**, and its consequence for "remove access" questions.
3. **The four default roles and their negative space** — what `view`, `edit`, `admin` and `cluster-admin` each *cannot* do, and that `cluster-admin` in a RoleBinding is namespace-limited.
4. **Secrets are unencrypted in etcd by default**, and the three exposure paths.
5. **TokenRequest, not token Secrets**, with the v1.22 boundary.
6. **Three PSS levels × three PSA modes, applied per namespace by label.**

**Common traps** — B1's ten sourced D2.2 traps, framed as loss aversion per Part 10 without inventing a frequency claim:

| Trap | Correct understanding | Tag |
|---|---|---|
| RBAC has deny rules | Purely additive; remove the grant | `[source]` #53 |
| ClusterRole is only for cluster-scoped resources | It can also cover namespaced resources, bound into one namespace or across all | `[source]` #54 |
| The four combinations must be memorized | They derive from one boundary; the binding sets the scope | `[source]` #55 |
| A binding can be retargeted | It cannot, after creation | `[source]` #56 |
| `view` can read Secrets | It cannot — nor roles nor bindings | `[source]` #57 |
| `edit` can manage RBAC in its namespace | It cannot; `admin` can | `[source]` #58 |
| `cluster-admin` always means the whole cluster | In a RoleBinding it is scoped to that namespace | `[source]` #59 |
| Secrets are encrypted | Unencrypted in etcd by default; encryption at rest is opt-in | `[source]` #60 |
| An RBAC audit that shows no `get secrets` means Secrets are safe | Pod creation in the namespace reads any Secret in it, including via a Deployment | `[source]` #61 |
| Token Secrets are current best practice | TokenRequest, short-lived and rotating, since v1.22 | `[source]` #62 |
| PSS levels and PSA modes are the same axis | Levels say what is checked; modes say what happens | `[inferred]` |
| PodSecurityPolicy is a current control | Removed; superseded by Pod Security Admission | `[source]` |

**Two inferred traps, labelled.** The level/mode confusion and any "frequently tested" claim about supply-chain projects. Per B2's standing instruction and Guardrail #8, describe both as *easy to confuse*, never as *frequently tested*.

---

## 7. Practice Questions plan

**Target: 21**, per `question_budget.practice_questions` and B4.

**Distribution across sections** — weighted toward the two sections that carry seven of the chapter's ten sourced traps:

| Section | Items | Rationale |
|---|---|---|
| §1 Layers and phases | 2 | Recognition depth; placement on both maps |
| §2 Identity | 2 | The `default` account; TokenRequest versus token Secrets |
| §3 RBAC | **5** | Seven sourced traps live here; this is the chapter's centre of gravity |
| §4 Secrets | **4** | Two Fixed Points, two sourced traps, and the highest practical consequence |
| §5 `securityContext` | 2 | Field-level recognition plus the two-axis distinction |
| §6 PSS / PSA | 3 | Levels, modes, and the label surface |
| §7 Supply chain | 2 | Chain order and what a signature covers |
| §8 Policy engines | 1 | Category recognition and the admission/runtime split |
| §9 Zenith | 0 | Tested through the interleaved items below rather than on its own |

**Retrieval-practice items: 4 of 21 = 19%**, which with the Bearings brings the chapter's graded retrieval to **7 of 36 = 19.4%**, hitting the 20% target. The four:

1. Ch 4 §3 → the derivation, in a form the checkpoint did not use
2. Ch 2 §3 → digests as what a signature binds to
3. Ch 8 §2 → admission as the gate PSA and policy engines both occupy
4. Ch 10 §6 → NetworkPolicy's additive semantics, in an item that also requires §3 — this is the §9 item

**Interleaving strategy** — four items that cannot be answered from one section alone, which is where discrimination is actually tested:

- **§3 + §4**: an audit scenario in which the RBAC grants look correct and the Secrets are readable anyway.
- **§5 + §6**: a Pod spec and a namespace's labels; predict admitted, warned, or refused.
- **§2 + §3**: a workload that authenticates successfully and can do nothing, distinguishing an authentication failure from an authorization failure.
- **§7 + §8**: signature verification enforced at admission — which component does which half.

**Trap-answer construction.** Every distractor in the §3 and §4 items must be built from a *named* B1 trap rather than from a plausible-sounding wrong answer, and the why-wrong explanation must name the misconception. Per B7's orphan rulings: **ABAC** may appear as a distractor only if §3 writes its one clause; **PodSecurityPolicy** may appear only as a wrong option in a PSA item; **PodDisruptionBudget**, **eBPF** and **SLA** may not appear at all.

---

## 8. Required figures

Six anchors, matching `figures_planned` and the arc outline's stubs exactly.

### `ch12-fig01-4cs-and-lifecycle-phases` — §1

**Purpose.** Establish that the chapter has two maps, not one, and that a control has a position on both.

**Content.** The four lifecycle phases as a left-to-right sequence (develop → distribute → deploy → runtime), the four Cs as a nested containment (Cloud ⊃ Cluster ⊃ Container ⊃ Code), and a small number of named controls plotted on both. Keep the plotted controls to four or five — Part 18.12 caps useful labels near seven and this figure already carries eight structural labels before any control is added. The runtime phase should visibly split three ways (access / compute / storage) because that split is the chapter's table of contents.

**Blocked on § Open questions #1.** If the 4Cs are dropped, this anchor's slug and content both change.

### `ch12-fig02-rbac-four-way-matrix` — §3

**Purpose.** [B3] The payoff for cross-cutting theme #2 — a derived result, not a memorized table.

**Content.** Must **show its work**. Left: the namespaced/cluster-scoped boundary as `ch04-fig04` drew it. Right: the four objects, each connected to the boundary property that produces it, with the governing rule — *the binding determines the scope of the grant* — as the figure's conclusion rather than its caption. A reader who covers the left half should be unable to reconstruct the right half; a reader who covers the right half should be able to reconstruct it from the left. **Build as a deliberate visual echo of `ch04-fig04`** — the recognition is half the pedagogy, and it fails if the two figures do not rhyme.

### `ch12-fig03-serviceaccount-token-flow` — §2

**Purpose.** Make the identity/permission separation visible, and show where the token physically is.

**Content.** ServiceAccount object → TokenRequest → projected volume in the Pod → API request carrying the token → the authentication gate. The permission side stays deliberately *empty* in this figure, with a forward marker to §3 — the emptiness is the Fixed Point.

### `ch12-fig04-pod-security-standards-levels` — §6

**Purpose.** Make three adjectives concrete, and carry §5's field material at the same time.

**Content.** The three levels as columns; a selected set of `securityContext` fields from §5 as rows; each cell showing what the level permits. Then, separately and visually distinct, the three modes as an orthogonal axis with the namespace label form written out. **The orthogonality must be visible** — this is the figure that prevents the chapter's most likely wrong answer.

### `ch12-fig05-supply-chain-checkpoints` — §7

**Purpose.** Turn a project roster into a sequence.

**Content.** Build → scan → sign → record → verify → restrict → run, as a linear chain, with the artifact identity (the digest) carried along it and the tools named at the checkpoint each serves. The point the figure makes that prose struggles with: verification happens at *admission*, inside the cluster, and everything before it happened outside.

### `ch12-zenith-additive-never-deny` — §9

**Purpose.** Recognition, not information.

**Content.** Two panels, deliberately parallel in structure and deliberately different in subject: RBAC (identity → API request → grant) and NetworkPolicy (Pod → connection → allow rule). Same shape, different layer. Both panels end at the same statement. This figure fails if the two halves do not look like each other at a glance — the whole effect is the visual rhyme, exactly as `ch15-zenith` will need to rhyme with `ch03-fig02`.

---

## 9. Open questions for the author

### 1. **BLOCKING EDITORIAL — the 4Cs may no longer be a live framing, and §1 is named for it.**

The cached snapshot `k8s-docs-cloud-native-security-2026-08-23.md` carries an explicit note in its own text: *"this page replaced the older '4C's of Cloud Native Security' framing — Cloud, Cluster, Container, Code — with the CNCF whitepaper's lifecycle phases."* B6 titles §1 "Four Layers and Four Phases", the arc outline lists both, and the figure anchor is `ch12-fig01-4cs-and-lifecycle-phases`.

This is not a fetch problem. It is a decision about what the book teaches, and there are three defensible answers:

- **(a) Teach both, with the phases as current and the 4Cs as the framing the reader will meet everywhere else.** Requires one source for the 4Cs — the archived kubernetes.io page or the CNCF TAG Security whitepaper the current page cites.
- **(b) Teach the phases only**, and note in a clause that older material organizes this as four layers.
- **(c) Teach the 4Cs only**, on the grounds that third-party KCNA prep is saturated with it.

**Recommendation: (a).** It is consistent with what the book already does about the blueprint change — B2 disclosure #3 commits to telling readers where their older material has gone stale — and the 4Cs is genuinely useful as a *where* map alongside the phases' *when*. (c) is wrong: it would have the book teaching a framing its own primary source has retired. (b) is safe but wastes an opportunity, since the reader will meet the 4Cs within a day of opening any other study guide.

If (b) or (c) is chosen, §1's title, its figure anchor and its Fixed Point all change, and this outline needs a revision before drafting.

### 2. **BLOCKING RESEARCH — G5 is wide open, and §5 cannot be drafted at all.**

A grep across all 168 cached sources returns **zero** matches for `securityContext`, `runAsNonRoot`, `allowPrivilegeEscalation` or Linux capabilities in a teaching context. The only mentions of `securityContext` in the corpus are incidental — one in the storage documentation, one in the Falco detection list. §5 is a full section against a pinned cross-bearing that three shipped chapters point at.

**Fetch required:**
- `kubernetes.io/docs/tasks/configure-pod-container/security-context/` — the field surface, Pod versus container scope, capabilities, seccomp, AppArmor
- `kubernetes.io/docs/concepts/security/pod-security-admission/` — the PSA concept page, which the PSS snapshot summarizes in one paragraph and §6 needs in full (mode/level combinations, exemptions, the label form)

Both are single fetches from the primary authority. §6 is *partially* draftable from the existing PSS snapshot; §5 is not draftable at all.

### 3. **BLOCKING RESEARCH — encryption at rest has no source.**

§4's headline claim is well covered (`k8s-docs-secrets-good-practices-2026-08-24.md` plus the domain analysis carry "unencrypted in etcd by default" and the three exposure paths). What is *not* covered anywhere is what encryption at rest actually **is**: `EncryptionConfiguration`, the provider options, that it encrypts the object as written to etcd and not as returned to an authorized API caller, and that it is a control-plane configuration rather than a manifest field. That last distinction is exactly the sort of thing an exam item is built on, and §4 currently cannot state it.

**Fetch required:** `kubernetes.io/docs/tasks/administer-cluster/encrypt-data/`.

Consider also `kubernetes.io/docs/concepts/security/rbac-good-practices/` — it is the authoritative home of the privilege-escalation framing that §3 and §4 both lean on, and the current RBAC snapshot does not cover it.

### 4. **G22 is partially open, and the section may be better organized than the arc outline implies.**

`sigstore-overview-2026-08-23.md` is genuinely good and covers signing, attestation, keyless flow, Cosign/Fulcio/Rekor and the transparency log, and it names SBOMs as a signable artifact class. **Not covered anywhere:** what an SBOM *is*, `in-toto`, TUF, Notary, Harbor, and image scanning as a practice.

**Fetch recommended:** CNCF glossary entries for *software bill of materials* and *supply chain security*, plus overview pages for in-toto, TUF and Harbor. Four project pages for one section is a lot of fetching for a 🟡 section, which leads to the second half of this question:

**Structural recommendation — organize §7 by checkpoint, not by roster.** The figure anchor the arc outline already assigned (`ch12-fig05-supply-chain-checkpoints`) points this way, and it is the right instinct. A reader who can name *scan → sign → record → verify → restrict* and say what each step buys is better prepared than one who can list five project names, and B1's inventory containing zero supply-chain traps suggests the exam agrees. Under that shape, in-toto, TUF, Notary and Harbor become *instances named at their checkpoint*, which needs one sentence each and a much lighter research load than a comparative treatment would.

**Author's call**: is the lighter treatment acceptable, or should §7 carry a fuller project comparison? The lighter one is this outline's recommendation.

### 5. **§9 is committed to an explanation the sources do not supply.**

Shipped Ch 11 line 1638 promises the reader: *"by the end of the next chapter you will understand why two systems built for entirely different purposes arrived at the same design, and why that design is a feature rather than an omission."*

No cached source states a design rationale for either RBAC's or NetworkPolicy's additive semantics. Both state the property; neither explains it. The chapter must therefore either deliver an argument that is explicitly the author's, or break a promise the reader was given in as many words.

**Recommendation: deliver it, visibly marked as a reading.** The argument is sound (a deny rule makes a grant's effect non-local and makes evaluation order into semantics; additive-only is what lets a single rule be read in isolation by one of many authors), and the book already has a form for this — the "Simple Version / Full Picture" uncertainty-signal pattern in skill Part 11. What is *not* acceptable is presenting the rationale in the same register as the sourced facts around it. The full drafting instruction is in §9's note above.

**This is a promise the book made, so declining to answer is also a decision** — if the author would rather not reason beyond the sources here, Ch 11 line 1638 needs an edit, and that is a change to shipped text.

### 6. **The `binding` collision is not in B7's Canonical forms table as a live risk, and it should be.**

B7 records the three senses (scheduler binding Ch 7 §1, PV/PVC binding Ch 11 §2, the RBAC objects) and rules that the RBAC objects are never shortened to "binding". What it does not record is that **the reader's most recent encounter with the word was one chapter ago**, in a section whose Fixed Point was that binding is exclusive and one-to-one — a property RBAC bindings emphatically do not have. A reader carrying that forward will make a wrong prediction.

**Recommendation:** §3 opens by disposing of it in one sentence (already specified in the section plan), and B7's Canonical forms row for `binding` gains a note that Ch 12 §3 must do so. The second half is a ledger edit and is the author's call; the first half is a drafting instruction and stands regardless.

### 7. **Three sections have no figure. Two are deliberate; one is arguable.**

- **§5** has none *by design*: `ch12-fig04` is specified to carry the `securityContext` fields against the levels that constrain them, which serves §5 better than a standalone field table would and avoids two figures teaching the same rows.
- **§8** has none *by design*: the section's content is a two-way split (admission-time versus runtime) that a sentence carries as well as a diagram, and Part 18.9 rules against illustrating what a text list already handles optimally.
- **§4 is the arguable one.** The three exposure paths are the chapter's most consequential practical fact and they have a genuinely spatial structure — three different actors reaching the same object by three different routes. That is a strong figure candidate by Part 18.9's own criteria, and the arc outline simply did not allocate one.

**Recommendation: add `ch12-fig06-secret-exposure-paths` to §4.** This is the one place this outline proposes exceeding the arc outline's figure allocation, and it is a small deviation with a clear pedagogical case. Ch 11's outline made no such addition, so this establishes a precedent — hence flagging it rather than doing it. **Author's call.** If declined, §4 stands on its ⚠ Navigational Hazards block, which is adequate but less memorable.

### 8. **The ABAC clause is required before ABAC can be used as a distractor.**

Shipped Ch 8 line 426 quotes the documentation naming *"ABAC mode, RBAC Mode, and Webhook mode"*, so the reader has met the acronym. B7 rules ABAC **glossary-only**, with an explicit condition: *"Ch 12 §3 may name it in a single clause establishing that RBAC is an authorization mode rather than the authorization mechanism. It must not appear as a distractor unless that clause is written."*

The section plan writes the clause. Recording it here so a later question-quality audit does not remove it as apparent padding — it is load-bearing for the Practice Questions, and it is also simply true and useful.

### 9. **Non-blocking: nine sections, and whether §7 and §8 could merge.**

B6 states outright that this chapter's count should not be compressed, and §7 and §8 are the only two that could plausibly fuse (both are ecosystem-facing, both are 🟡-adjacent, and Sigstore's Policy Controller already bridges them). This outline keeps them separate because they answer different questions at different times, and because merging them would produce one section with four project rosters in it.

Recorded only so a later stage does not re-open it as a fresh idea. **No action recommended.**

### 10. **Non-blocking: does §5's difficulty glyph undersell it?**

§5 is marked 🔵 alongside §3, §4 and §6, but it is the only section in the chapter whose material has *no* cached source at all and whose content (Linux capabilities, seccomp, AppArmor) reaches further below the Kubernetes API than anything since Ch 2 §1. An argument exists for 🟡.

**Recommendation: keep 🔵.** Three shipped chapters point at §5 by number and one of them frames it as *"an entire security apparatus"*. Marking it Advanced would tell the reader it is optional depth immediately after three chapters told them it was the answer to a question they were promised. Revisit after G5 closes and the real field surface is known.
```