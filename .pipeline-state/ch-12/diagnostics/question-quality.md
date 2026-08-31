Running the Stage 8 question-quality audit against `draft-v1.md`. Output follows (stdout, per the executor contract in CLAUDE.md — not written to a CWD-relative path).

---

# Question-Quality Audit — Chapter 12

## Summary

- Chapter type: **content**
- Total questions inspected: **44**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints)
  - Practice questions: **21**
- Question budget compliance: **met** (all four rows)
- Weak distractors (WARN): **14** (of ~108 distractor slots across 36 multiple-choice items — ~13%)
- Trap answers that don't target real misconceptions (WARN): **6**
- Missing or incomplete why-wrong explanations (FAIL): **4 incomplete, 0 missing**
- Retrieval-practice spacing: **compliant** (checkpoints 20.0%; whole-chapter graded 19.4%)
- Soundings spoiler check: **1 question reveals a Fixed Point in its answer disclosure — FAIL** (Q7); 1 additional WARN (Q6)
- **Additional FAIL category not in the template — defective stems / unsatisfiable correct answers: 3** (Bearings #1 Q3, Bearings #2 Q1, Practice 12). Two of these are architectural, not typographic, and one of them is the chapter's designated challenge item.
- **Additional FAIL — checkpoint revision prompts absent: 3 of 3.** No checkpoint carries a score-based revision prompt (skill Part 11 "Revision Prompts", Part 13 "Micro-Progress After Checkpoints", Part 17 Ethical Checkpoint). Soundings has its rubric; the Bearings checkpoints have "You've Now Mastered" progress markers only.

---

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 15 | 15 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline: 3) | 3 | met |
| Practice Questions | 21 | 21 | met |
| **Chapter total** | **44** | **44** | **met** |

The outline's upward override of B4's Bearings minimum (10 → 15, three checkpoints of five) is delivered exactly. Placement matches the plan: after §3, §6, §8. Distribution across sections also matches the outline's weighting (§3 five practice items, §4 four, §6 three, §1/§2/§5/§7 two each, §8 one, §9 zero-and-tested-by-interleave).

Format requirements: Soundings answers are inside a `<details>` collapsible ✓; the 6+/3–5/0–2 reading-strategy rubric is present and the 0–2 branch correctly names **sections** and singles out Ch 4 §3 as the pre-read ✓; the designated challenge item (Bearings #2 Q1) carries the explicit difficulty label required by Part 10B ✓.

---

## Soundings spoiler check

Chapter ★ Fixed Points, for reference: (FP1) phases = *when*, layers = *where*; (FP2) identity ≠ permission, proved by the `default` ServiceAccount; (FP3) the binding determines the scope of the grant; (FP4) permissions purely additive, no deny rule; (FP5) Secrets unencrypted in etcd by default, encryption at rest opt-in; (FP6) Pod-creation reads every Secret in the namespace; (FP7) `securityContext` = workload-to-host, NetworkPolicy = workload-to-workload; (FP8) three levels × three modes, level = what, mode = what happens; (FP9) a signature binds to a digest, not a tag.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Cluster-scoped resource, granted "in one namespace"? | no | Stem and key stay on Ch 4 §3's boundary ("belongs to no namespace at all"). Sets up FP3's derivation without performing it. Exactly as the outline ruled. |
| 2 | Identity of a Pod naming no ServiceAccount | no | Key answers provenance only — "the `default` ServiceAccount for its namespace." Says nothing about permissions, leaving FP2's payload intact. |
| 3 | What base64 does / does not do | no | Ch 4 §4 material verbatim. FP5's payload (etcd storage, opt-in encryption) untouched. |
| 4 | The three gates, in order | no | Ch 8 §2 material. FP8 untouched; no Pod Security term appears. |
| 5 | Can one NetworkPolicy deny what another allows? | no | Key stays entirely inside NetworkPolicy and does **not** append "and RBAC is the same." The outline's recorded ruling is honoured. |
| 6 | Deny in a permission system you've used | **WARN** | Key closes: *"Hold on to that expectation. **This chapter is going to violate it twice.**"* Paired with Q5, "twice" telegraphs FP4. Mitigating: shipped Ch 11 line 1638 and the chapter subtitle both state FP4 outright by design, so the Soundings is not the leak. Recorded as WARN, not FAIL. |
| 7 | What a signature proves; tag vs digest | **yes — FAIL** | Key states FP9's entire load-bearing argument: *"a signature over a tag would prove close to nothing, because a tag is a mutable pointer: whatever it named at signing time is not necessarily what it names now."* |
| 8 | Root in a container vs root on the node | no | Delivers §5's *opening baseline*, not FP7 (the two-axis claim), and explicitly defers: "Which of those two facts dominates is exactly what §5 is about." Clean, generous but correctly bounded. |

### Q7 finding in detail

The **stem** is clean — it poses the question without answering it, which is the intended pre-test. The **answer disclosure** is where it fails. Skill Part 11 specifies Soundings answers as "*1-line rationale each*"; this one runs the full argument. The reader is instructed to open the `<details>` block after attempting, so a reader following the Soundings correctly receives §7's reveal before reaching §7 — and §7's Fixed Point block is explicitly built as a turn ("It was not hygiene. It is the reason a signature means anything at all"), which lands flat once the reasoning is already in hand.

**Recommended fix (minimal):** compress the Q7 rationale to withhold the *why*.

> **7.** A signature proves that some specific bytes were signed by the holder of some specific key, and nothing more. It does not prove the software is safe, correct, or free of vulnerabilities. On the second half: if you answered that a tag-signature and a digest-signature are not the same thing, hold that answer — §7 shows what signing tools actually do about it. *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*

That preserves the pretesting effect (the reader still commits to an answer), keeps the Ch 2 retrieval hook, and leaves both the mutable-pointer argument and the resolve-to-digest mechanic for §7.

---

## Per-question findings

### Q[Bearings #1] 3: "Your team needs a group of engineers to be able to read `PersistentVolume` objects…"

**Issue:** The keyed-correct answer does not satisfy the stem's stated constraints, and the scenario as posed requires two grants rather than one combination. This is the chapter's flagship derivation item, so the defect is expensive.

The stem imposes three requirements: (a) read cluster-scoped `PersistentVolume`; (b) a wider set of namespaced read permissions reusable across three namespaces; (c) **no access in a fourth namespace**. Answer D — one ClusterRole holding both rule sets, bound by a ClusterRoleBinding — grants the *namespaced* rules in the fourth namespace too, violating (c). The answer key acknowledges only the cluster-scoped half: "the namespace-limiting requirement in the scenario is not achievable for the cluster-scoped half." True, and incomplete.

**Distractor analysis:**
- A) Role in each of three namespaces + RoleBinding — fails at question one (a Role cannot hold a cluster-scoped rule). Strong, targets the real misconception.
- B) ClusterRole + RoleBinding in each of three namespaces, "but note this does not grant the PersistentVolume access" — **this option best satisfies (b) and (c) and self-labels its own limitation.** It is the more defensible answer to the stem for two of three requirements, which makes the item ambiguous rather than difficult.
- C) ClusterRole + ClusterRoleBinding, "cluster-scoped resources require a cluster-wide binding" — good: right cells, wrong reasoning. The key handles this well.
- D) keyed correct — see above.

**Why-wrong explanation status:** present and specific for A, B, C; the correct answer's explanation is **incomplete** (does not address the fourth-namespace conflict it creates).

**Recommended fix:** Split the requirement so one combination genuinely answers it. Simplest edit — delete requirement (b) and (c)'s coupling:

> Your team needs a group of engineers to be able to read `PersistentVolume` objects — which are cluster-scoped — as part of a reusable read-only permission set. Which combination of objects does this call for, and what forces the choice?

Then D is correct without qualification, and B remains a strong trap (it grants the namespaced rules but silently drops the PV rule). If the author wants to keep the two-grants insight, make it the *point* of the question and add an option E-equivalent: *"Two grants: a ClusterRole + ClusterRoleBinding for the PersistentVolume rule, and a ClusterRole + RoleBinding in each of the three namespaces for the rest."* That is genuinely the best answer to the stem as written, and it is a better lesson than either current option.

---

### Q[Bearings #2] 1: "You are auditing a namespace called `payments`…" — the designated challenge item

**Issue:** The stem contradicts itself against the chapter's own sourced text.

It asserts: *"No subject holds `get`, `list`, or `watch` on `secrets`"* and, two sentences later, *"Eight engineers hold the `edit` ClusterRole via RoleBindings."* But §3 quotes the documentation directly: `edit` *"allows accessing Secrets and running Pods as any ServiceAccount in the namespace"*, and the answer key itself concedes *"`edit` does have access to Secrets."* If `edit` grants Secret access, the audit premise is false as stated, and distractor D's stated reason is **true**, not a misconception.

**Distractor analysis:**
- A) Nobody — the audit finding. Strong; this is the misconception the item exists to break.
- B) Only cluster administrators via etcd; enable encryption at rest — strong; real control applied to the wrong route.
- C) keyed correct — the workload-creation path, with the namespace-separation remediation. The right lesson.
- D) All eight, because `edit` includes `get secrets`; replace `edit` with `view` — **premise is correct**, only the remediation is wrong. A distractor whose stated reasoning is accurate is not a trap; it is a second defensible answer with a bad tail.

**Why-wrong explanation status:** present and specific for A, B, D — but D's explanation has to argue against a claim the chapter elsewhere endorses, which is why it reads strained.

**Recommended fix:** replace `edit` with a hand-built role, which preserves the entire intended lesson and removes the contradiction:

> Eight engineers hold a custom `deployer` Role, granting `create`, `update`, `patch` and `delete` on `deployments`, `pods` and `services` — and nothing on `secrets`.

Now the audit premise is literally true, D becomes cleanly wrong (`deployer` grants no Secret verbs), and the Pod-creation escalation path is the *only* explanation available. This is the strongest question in the chapter once fixed; it is worth fixing rather than trimming.

---

### Q[Practice] 12: "Which**12.** Which statement about mounting a Secret is correct?"

**Issue:** Garbled stem — the number and the opening word are duplicated, apparently a splice artifact. Reads as a rendering error and will be visible in the shipped EPUB.

**Distractor analysis:** the options themselves are sound.
- A) volume mount updates automatically, except `subPath` — correct, and the `subPath` carve-out makes it precise rather than lucky.
- B) env var updates automatically — the inversion; real and common.
- C) both update; the difference is only file permissions — plausible to a reader who half-remembers the section.
- D) neither updates — plausible to a reader who over-generalizes from immutable Secrets.

**Why-wrong explanation status:** present for B; **incomplete** for C and D, which are dismissed jointly as "both get the asymmetry wrong" without naming each error.

**Recommended fix:** restore the stem to `**12.** Which statement about mounting a Secret is correct?` and split the C/D explanation: *"**C** is wrong because the two mechanisms differ in update behaviour, not in permissions — `defaultMode` governs permissions and is a volume-only concern regardless. **D** is wrong because volume mounts do propagate; it generalizes the environment-variable behaviour to both."*

---

### Q[Practice] 4: "Which is the current recommended way for a Pod to obtain ServiceAccount credentials?"

**Issue:** Effectively a two-option question. Only A is a real trap.

**Distractor analysis:**
- A) `kubernetes.io/service-account-token` Secret — strong, and the legacy/current boundary is exactly what §2's 🪝 Snag flags.
- B) keyed correct.
- C) Store the token in a ConfigMap and reference as an env var — borderline. A real anti-pattern, but the chapter has spent two sections on Secret-vs-ConfigMap and no reader who has reached §7 will pick it.
- D) Pass the token as a command-line argument at container start — implausible; nothing in the chapter or in practice suggests it.

**Why-wrong explanation status:** present and specific for A, C, D.

**Recommended fix:** replace D with a plausible near-miss that tests the *mechanism* rather than the object type — e.g. *"Mount the ServiceAccount's token from a `secret` volume referencing the account's auto-created token Secret."* That is what pre-1.22 clusters actually did, so it targets a real and dated mental model rather than a straw option.

---

### Q[Practice] 14: "Which statement about `privileged: true` is correct?"

**Issue:** Two of three distractors are implausible, reducing a high-value ⚠ Navigational Hazards concept to a two-option item.

**Distractor analysis:**
- A) grants a single additional capability, `CAP_SYS_ADMIN` — good. Real understatement, and `CAP_SYS_ADMIN` is the capability people associate with privilege.
- B) applies only to init containers — fabricated scope limit; nothing suggests it.
- C) keyed correct.
- D) required for a container to mount any volume — fabricated; the reader mounted volumes for a whole chapter without it.

**Recommended fix:** replace B and D with departures the section actually warns about:
- *"It grants all Linux capabilities but leaves the applied seccomp and AppArmor profiles in force."* (targets the real belief that hardening layers stack independently — the exact thing the source sentence contradicts)
- *"It is required to set `hostNetwork: true`."* (targets conflation of privileged mode with host-namespace access, two distinct Baseline violations)

---

### Q[Bearings #1] 1: "A cluster administrator enables encryption at rest for API objects…"

**Issue:** Two implausible distractors; the item reads as A-versus-B for any prepared reader, and the why-wrong explanation for the weak pair is joint and vague.

**Distractor analysis:**
- A) Distribute phase; Container layer — strong. It is image signing's position, which is the exact coordinate-swap the question exists to test.
- B) keyed correct.
- C) Deploy phase; Code layer — implausible on both axes.
- D) Develop phase; Cluster layer — implausible on the phase axis.

**Why-wrong explanation status:** **incomplete.** "C and D put a storage control in phases that end before storage exists" handles both jointly and is imprecise (the deploy phase does not "end before storage exists"; it precedes runtime).

**Recommended fix:** make C and D single-axis errors so each targets one real confusion — e.g. C) *"Runtime phase (storage); Container layer"* (right phase, wrong layer — tests whether the reader knows etcd is Cloud/Cluster, not Container) and D) *"Deploy phase; Cluster layer"* (right layer, wrong phase — tests whether "the operator configures it" gets misread as a deploy-time act). Then explain each individually.

---

### Structural: all three checkpoints lack revision prompts

**Issue:** Skill Part 11 requires revision prompts when a checkpoint reveals gaps, Part 13 specifies the 5/5 · 3–4 · 0–2 micro-progress pattern after checkpoints, and Part 17's Ethical Checkpoint lists "Revision prompts included for low checkpoint scores." All three checkpoints close with a "**Checkpoint: You've Now Mastered**" progress marker and no score-conditional guidance.

This is the only self-correction mechanism the chapter is missing — trap answers, why-wrong explanations and the Soundings rubric are all present and mostly strong, which makes the omission conspicuous rather than systemic.

**Recommended fix:** add three lines after each checkpoint's answer key, before the progress marker. Section pointers matter more than encouragement here, because this chapter's sections are independent arcs:

> **5/5:** move on. **3–4:** re-read the section behind each miss before continuing — this chapter's sections do not scaffold each other, so a gap here stays a gap. **0–2:** re-read §3 in full before §4; the Secret exposure argument is built on the default roles and the additive rule.

Checkpoint #2's 0–2 branch should point at §5 before §6 (the levels are meaningless without the fields); #3's at §7 before §8.

---

### Minor: near-duplicate architecture — Bearings #1 Q2 and Practice 3

Both test "authentication succeeds, authorization fails" with the same four-way misconception set (namespace-implies-read / scheduling failure / token failure / correct). They differ meaningfully in setup — Q2 uses the auto-assigned `default` account, P3 uses an explicitly created account with no bindings — so they test adjacent claims ("the default grants nothing" vs "creating an account grants nothing") rather than one claim twice. Defensible as spacing; recorded so a later pass does not read it as accidental.

If one is to be repurposed, P3 is the candidate, and the best use of the slot is **`orphaned-identity`** (see coverage gaps below): a ServiceAccount and its RoleBindings surviving the Deployment that used them. That concept pays a Ch 6 debt, is currently untested, and reuses the same object model.

---

## Weak-distractor register

Compact list of the 14 flagged options, for a revision pass:

| Question | Option | Problem |
|---|---|---|
| Bearings #1 Q1 | C | Deploy/Code for a storage control — implausible on both axes |
| Bearings #1 Q1 | D | Develop phase for a runtime control — implausible |
| Bearings #2 Q2 | D | "base64 over ciphertext, which is why values look different" — fabricated mechanism, self-refuting |
| Bearings #2 Q4 | B | "a namespace cannot carry three Pod Security labels" — invented constraint |
| Bearings #2 Q5 | A | admission running "during authentication, before the API server knows who the requester is" — internally nonsensical against the gate order just taught |
| Bearings #3 Q2 | D | verify → scan → sign — verification before the artifact exists |
| Bearings #3 Q4 | B | "Kyverno will mutate the container to remove the shell" — not a coherent operation |
| Practice 4 | C | token in a ConfigMap (borderline — real anti-pattern, but pre-empted by two sections) |
| Practice 4 | D | token as a command-line argument |
| Practice 5 | D | "either, depending on preference" — treats a structural constraint as taste |
| Practice 6 | D | "staging and any namespace they can also list" — invented rule |
| Practice 8 | D | "labels cannot be applied to ServiceAccount objects" — obviously false |
| Practice 14 | B | privileged applies only to init containers |
| Practice 14 | D | privileged required to mount any volume |
| Practice 21 | D | "designed by the same working group" — directly contradicted by §9's own argument |

**Fabricated-trap subset (6):** Bearings #2 Q2 D, Bearings #2 Q4 B, Bearings #3 Q4 B, Practice 6 D, Practice 8 D, Practice 21 D. Each invents a mechanism the answer key then corrects as though it were a known confusion. Practice 21 D is the most worth replacing: §9's entire argument is that the two systems converged *without* coordinating, so an option asserting shared authorship is refuted by the section the question is testing. A stronger substitute: *"Both were retrofitted with deny semantics in later API versions."*

**Distractor sets that are working well** and should not be touched: Bearings #1 Q4 (option C is the deny-semantics misconception in disguise — excellent), Bearings #1 Q5, Bearings #3 Q3 (option D retrieves the no-deny rule as a wrong answer), Bearings #3 Q5, Practice 2 (all three wrong options are real items from the *other* runtime areas), Practice 9, Practice 11 (four real controls, three applied to the wrong exposure route), Practice 13 (all three wrong options are *other real `securityContext` fields* — the exact confusion §5 produces), Practice 16 (option A is Baseline's documented property offered as Restricted's), Practice 18, Practice 20.

---

## Why-wrong explanation status

**Missing entirely: 0.** Every multiple-choice item in the chapter has an answer key that addresses the wrong options. This is a genuine strength — the chapter clears the skill's self-correction bar for answer keys.

**Incomplete (4):**

| Question | Options | Problem |
|---|---|---|
| Bearings #1 Q1 | C, D | Handled jointly and imprecisely ("phases that end before storage exists") |
| Bearings #2 Q5 | A, B | "A and B put it at the wrong gates" — names the error, does not say what each misconception is |
| Practice 12 | C, D | "both get the asymmetry wrong" — C and D fail in opposite directions and need one clause each |
| Practice 20 | A, C | "A, C, and D each place verification somewhere plausible but wrong" then treats only D. A (runtime, at pull) and C (registry, before serving) are meaningfully different errors |

**Correct-answer explanation incomplete (1):** Bearings #1 Q3 D — see the per-question block; the key does not address the fourth-namespace conflict the keyed answer creates.

---

## Retrieval-practice spacing

- Chapter 12 target: **20%** (arc outline; skill Part 10 band for Ch 6+ is 20–25%)
- Checkpoint retrieval: **20.0%** — 3 of 15
  - Bearings #1 Q3 — `[retrieval: ch4]`, eight-back (namespaced/cluster-scoped)
  - Bearings #2 Q5 — `[retrieval: ch8]`, four-back (the three gates)
  - Bearings #3 Q1 — `[retrieval: ch2]`, ten-back (tags vs digests) — the deepest in the chapter
- Practice retrieval: **19.0%** — 4 of 21 (Practice 8 `[ch4]`, 15 `[ch10]`, 18 `[ch8]`, 19 `[ch2]`)
- Whole-chapter graded: **19.4%** — 7 of 36
- Status: **compliant.** The ≥4-back spacing floor is satisfied several times over, and the checkpoint figure hits the target exactly. The combined 19.4% sits a fraction under the Ch 6+ 20–25% band.

**Two bookkeeping notes:**

1. **Practice 21 is the planned §9 interleave item but carries no retrieval tag.** The outline specified the fourth practice retrieval as "Ch 10 §6 → NetworkPolicy's additive semantics, in an item that also requires §3." That is Practice 21, which genuinely requires Ch 10 material (option A's claim about the API server, option B's claim about selectors). The tag landed on Practice 15 instead — also a legitimate Ch 10 item, but the axis question rather than the additive-semantics one. Tagging Practice 21 as well brings the whole-chapter figure to **8 of 36 = 22.2%**, squarely inside the band, at the cost of one tag and no new question.

2. **Bearings #3 Q5 is correctly untagged.** It is within-chapter spacing back to §3, which the outline explicitly excluded from the retrieval budget. Correct as shipped.

**Interleaving (outline planned four cross-section items):**

| Planned | Delivered | Status |
|---|---|---|
| §3 + §4 — audit scenario, RBAC looks correct and Secrets readable | Bearings #2 Q1 | present (defective stem — see findings) |
| §5 + §6 — Pod spec + namespace labels, predict admitted/warned/refused | — | **thin.** Bearings #2 Q3 is §5-only; Bearings #2 Q4 and Practice 16 are §6-only. No item requires reading a `securityContext` *against* a namespace label. |
| §2 + §3 — authenticates, can do nothing | Bearings #1 Q2, Practice 3 | present (twice) |
| §7 + §8 — signature verification enforced at admission | Practice 20 | present |

The §5+§6 gap is worth closing, because it is the one the *What You'll Learn* block promises verbatim ("**Read** a `securityContext` and a namespace's Pod Security labels together, and predict whether a given Pod is admitted, warned about, or refused"). A single item showing a four-line Pod spec beside two namespace labels would discharge it, and `ch12-fig04` already supplies the row data to build it from.

---

## Coverage vs concepts

Tested-and-fine concepts are summarized rather than enumerated; gaps are listed in full.

**Well covered** — lifecycle phases and the runtime split (P1, P2, B1Q1) · 4Cs (P1, B1Q1) · ServiceAccount as object and as subject (P3, P8) · `default` account permissions (B1Q2) · TokenRequest vs legacy token Secret (P4) · the four RBAC objects and the derivation (B1Q3, P5, P6) · binding-determines-scope (P6) · `resourceNames` (P7) · subjects-named-not-selected (P8) · the four default roles and their negative space (B1Q5, P9) · additive/no-deny (B3Q5, P21) · binding immutability (B1Q4) · base64 (P10) · unencrypted-in-etcd and encryption at rest (B2Q2, P11) · the three exposure paths and the Pod-creation path (B2Q1) · file-over-env-var (P12) · Pod vs container scope (B2Q3) · `runAsNonRoot` (P13) · `privileged` (P14) · the two axes (P15) · three levels (P16) · levels × modes (P17) · PSA as admission (B2Q5, P18) · signature-binds-to-digest (B3Q1, P19) · verification at admission (P20) · policy engine vs PSA (B3Q3) · admission-time vs runtime, Falco detects-not-prevents (B3Q4) · the shared semantic (P21).

**Not tested anywhere:**

| Concept introduced in chapter | Tested? | Note |
|---|---|---|
| `develop-phase` | **NO** | Named in §1 with three specific practices; no question touches it |
| `deploy-phase` | **NO** | No question names it, though B3Q2's "verify" is its enforcement |
| `user-and-group-external-identity` | **NO** | §2 spends a full subsection on "Kubernetes has no User object" and the `system:serviceaccount:` / `system:serviceaccounts:` singular/plural detail |
| `orphaned-identity` | **NO** | §2's closing subsection; pays the `chapter-06:486` debt. Untested = the debt is paid in prose only |
| RBAC escalation prevention (`escalate` / `bind` verbs) | **NO** | A full §3 subsection, and the chapter's epigraph quotes it |
| `system:masters` | **NO** | §3 gives it "its own beat" as un-revocable and audit-invisible — high-consequence, zero questions |
| `kubectl auth can-i` | **NO** | Taught in §3's closing |
| `list`/`watch` on Secrets ⇒ effective read | **NO** | §4, sourced, and directly adjacent to the challenge item's audit premise |
| `external-secret-store` (Secrets Store CSI Driver) | **NO** | One of the four documented hardening steps |
| `secret-type` (the eight built-in types) | **NO** | Including the `dockerconfigjson` ⇒ `imagePullSecret` connection that pays `chapter-02:459` |
| `linux-capabilities` (as a concept) | distractor only | P13 A and P14 A/C reference it; nothing tests the drop-`ALL`-then-add model or the `CAP_` prefix omission |
| `read-only-root-filesystem` | distractor only | P13 C, B3Q4 D |
| `allow-privilege-escalation` | **NO** | Appears in P16's key and the figure; never a stem |
| `seccomp`, `apparmor` | **NO** | Substantial §5 coverage — enforcing vs complain mode, path-based vs inode-based, the "use the runtime default" guidance. Zero questions |
| namespace-label patching as a privilege | **NO** | §6's sourced warning that patching a Namespace can lower its policy |
| `podsecuritypolicy-removed` | **NO** | The outline explicitly budgeted it as "eligible as a wrong option in a PSA item"; it appears in the Exam Alert table but is never used as a distractor |
| `image-scanning`, `cve` | **NO** | Named in B3Q2's ordering only; nothing tests scan-vs-sign as different guarantees |
| `attestation`, `provenance` | **NO** | |
| `sbom` | distractor only | P19 D |
| `cosign`, `fulcio`, `rekor`, `keyless-signing`, `transparency-log` | **NO** | Sigstore appears in P20 as a component name; the keyless argument (ephemeral key, discarded after one signing, nothing durable to steal) — §7's most distinctive content — is untested |
| `in-toto`, `tuf`, `notary`, `harbor` | **NO** | TUF's four quoted attacks (all involving *correctly signed* artifacts) are the section's sharpest material and carry no question |
| `rego` | **NO** | |
| `validate-mutate-generate` — generate and clean up | **NO** | Validate and mutate are covered via P18; the other two verbs are not |
| All six tagged `kb_tags.commands` | **NO** | `kubectl auth can-i`, `create role`, `create rolebinding`, `describe clusterrole`, `get serviceaccount`, `label namespace` — none appears in any question |

**Assessment of the gaps.** Three clusters, in descending priority:

1. **§7 is the largest coverage deficit in the chapter.** Nineteen tagged concepts against 2 practice items and 2 checkpoint items. The outline's rationale — 🟡, recognition depth, zero sourced traps in B1's inventory — justifies the *count*, but not the *selection*: both items test the same fact (what a signature binds to), leaving keyless signing, transparency logs, SBOMs, provenance, TUF and scan-vs-sign entirely unexamined. Recommend re-pointing one of the two §7 practice items at a different concept rather than adding count. A TUF item is the highest-value single swap, because its four attack scenarios all involve correctly signed artifacts and therefore *discriminate* rather than merely recognize.

2. **§3's escalation-prevention and `system:masters` material.** Both are consequential, both are sourced, both are quoted at length, and neither is tested. `system:masters` in particular is the chapter's clearest example of a control that is invisible to the audit method the chapter otherwise teaches — a natural pairing with Bearings #2 Q1's theme. One practice item covering both would be efficient.

3. **`seccomp` / `apparmor` and the command surface.** §5 devotes real space to the two security modules and the chapter tags six `kubectl` commands, none of which appear in a question. For a KCNA-tier book this is defensible for the commands (the exam is not performance-based), less so for seccomp/AppArmor, which the Restricted level's requirements depend on — Practice 16's correct answer cites "an explicit seccomp profile" as a Restricted requirement, so the reader is being graded on a concept they were never asked about directly.

None of these requires exceeding the question budget. The chapter has four items whose slots are currently spent on near-duplicate or two-option questions (Practice 3, Practice 4, Bearings #1 Q1, and one of the two signature items), which is exactly the number needed to close the highest-priority gaps.

---

## Priority order for a revision pass

1. **Bearings #2 Q1** — repair the contradictory stem (`edit` → custom `deployer` role). Highest severity: it is the designated challenge item and the chapter's most consequential fact.
2. **Bearings #1 Q3** — repair the unsatisfiable correct answer. Second highest: it is the flagship derivation item that two shipped chapters promised.
3. **Soundings Q7** — compress the answer-key rationale to stop spoiling §7's Fixed Point.
4. **Practice 12** — fix the garbled stem (mechanical; will otherwise ship).
5. **Add revision prompts** to all three checkpoints.
6. **Tag Practice 21** `[retrieval: ch10]` — one-word edit, brings whole-chapter retrieval to 22.2%.
7. **Replace the 6 fabricated traps** and the worst of the 14 weak distractors (Practice 14 B/D and Practice 8 D first).
8. **Re-point 3–4 existing question slots** at the untested concepts in priority-cluster order above; add a §5+§6 interleave item to discharge the *What You'll Learn* promise.
9. **Split the 4 incomplete why-wrong explanations** into per-option clauses.