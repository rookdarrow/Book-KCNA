Verified callbacks and retrieval questions directly against the shipped Chapters 1–3, the book outline, and the Chapter 3 knowledge-base ledger. `Write` isn't available to this stage by design — emitting the artifact to stdout:

```markdown
# Integration Check — KCNA Chapter 4

**Artifact audited:** `.pipeline-state/ch-04/draft-v2.md` (121,709 bytes, written 05:40) — confirmed identical to the revised draft in this stage's prompt by heading comparison.
**Verified against:** shipped `chapter-01-taking-departure.md`, `chapter-02-cargo-in-standard-crates.md`, `chapter-03-the-ship-s-company.md`; `.pipeline-state/book-outline/chapter-lineup.md`; `.pipeline-state/ch-03/kb-manifest.md`; `sources/`.

> **Note on inputs.** The stage prompt reported `[no knowledge-base shards tagged]`. Rather than guess, I read the three shipped chapters and the Chapter 3 kb-manifest from disk. Every callback verdict below is checked against actual earlier-chapter text with a line reference, not inferred. Forward cross-bearings into undrafted chapters (Ch 5–15) are checked against `chapter-lineup.md` for **chapter** correctness only; their **§ numbers** cannot be verified and are treated separately in "Contradictions."

## Summary

- Terminology consistency: **fail** — prose terminology is clean; section-label convention is not
- Callbacks to earlier chapters: **10 correct / 3 incorrect** (13 checked; 2 of the 3 are the same defect stated twice)
- Retrieval-practice accuracy: **pass** — 6 of 6 tagged items land on material the named chapter actually covers
- Glossary coverage: **34 concepts introduced, 30 defined in-chapter, 4 require glossary entries** (+5 deferral-hygiene gaps in the surfaced-elsewhere set)
- Contradictions with earlier canon: **5 flagged**
- Ethical guardrails (skill Part 14): **fail** — 1 item cannot be certified (see below), 2 borderline; the chapter itself is clean on the other 4

> ⚑ **Gate hole that outranks everything else in this report.** `diagnostics/fact-accuracy.md` for this chapter is a **BLOCKER notice, not an audit**. Stage 6 received `[file not available]` for both `draft-v2.md` and `draft-voice.md` and performed zero claim verification; its own report says "the zeroes above are the absence of an audit, **not a clean bill of health**." Chapter 4 therefore has **no fact-accuracy gate at all**. Stage 7 and 8 hit the same prompt-assembly bug and recovered by locating the draft on disk; Stage 6 did not. This report cannot substitute for that stage (rule 3), and the ethical checklist item that depends on it is marked unverifiable rather than passed.

---

## Terminology consistency

Prose terminology is consistent with Chapters 1–3. I checked every component name, resource kind, and branded marker for casing and spacing drift and found **none**: no `Kubelet`, `Kubectl`, `Etcd`, `APIserver`, `Config Map`, `Network Policy`, `Service Account`, `Persistent Volume`, `Storage Class`, `Shoals Ahead`, `Landfall`, or `Road Ahead` anywhere in the draft. Chapter 3's proposed convention lock on `kube-apiserver` (component name) versus "the API server" (prose form) is observed correctly throughout.

The failures are all in **section-label convention**, and they are load-bearing because Chapters 1 and 2 address this chapter by section number.

| Term / convention | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| Section headings | `## §N — ⚪ Title` (ch2 L267–885, ch3 L256–908) | 6 × `## ⚪ 1. Title` form | **Yes — see (a)** |
| Checkpoint headings | `## ☆ Taking Your Bearings #N: Topic` (ch2 L463/675/817, ch3 L481/676/836) | 3 × unnumbered | **Yes — see (b)** |
| § in body prose | matches the heading label | 11 (`§2`, `§3`, `§4`, `§5`, `§6`) | **Yes — headings carry no §** |
| `★ Fixed Point` | split book-wide: `**★ Fixed Point**` (ch1, ch3) vs `★ **Fixed Point:**` (ch2) | 3 × ch2 form | Pre-existing split; ch4 matches ch2 |
| `⚠ Navigational Hazards`, `⚓ Worth Securing`, `🪝 Snag`, `🔭 Closer Look`, `🪢 Mnemonic`, `— Dead Reckoning`, `Extended Analogy` | glyph outside bold, colon inside | all conforming | No |
| `☀️ Zenith` | `☀️ **Zenith**` inline (ch3 L910) | `### ☀️ Zenith` H3 + blockquote | Minor format variance |
| `🏆 Safe Harbor` | inline bold line (ch1 L567, ch2 L1324, ch3 L954) | promoted to `## 🏆 Safe Harbor` H2 | Minor; placement already varies book-wide |
| Metadata line | ch1/ch2/ch3 each differ | fourth variant, split across two lines, adds `Prerequisites:` | Pre-existing drift, extended |
| `kubelet`, `etcd`, `kube-apiserver`, `control plane`, `kubectl` | as shipped in ch2/ch3 | 28 combined, all conforming | No |
| `ConfigMap`, `Secret`, `NetworkPolicy`, `ServiceAccount`, `ReplicaSet`, `DaemonSet`, `StatefulSet`, `PersistentVolume`, `StorageClass` | CamelCase resource kinds | all conforming | No |

**(a) Section-heading numbering — the significant one.** Chapters 2 and 3 both ship `## §N — ⚪ Title`. Chapter 2's own frontmatter (L17–21) marks this explicitly: *"⚠ Section NUMBERING IS LOAD-BEARING. Chapter 1 shipped with two published cross-bearings that name sections of this chapter by number… Do not renumber without editing chapter-01."* Chapter 4 ships `## ⚪ 1. You File a Declaration`. Two consequences:

- **Two already-published cross-bearings address this chapter by §.** `chapter-01:148` points to *"Ch 4 §1 — declarative versus imperative"* and `chapter-02:459` points to *"Ch 4 §4 — Secrets, and the `dockerconfigjson` type"*. Both resolve **topically** — §1 is the declarative section, §4 is the Secrets section — but a reader following the pointer finds no `§1` or `§4` label in Chapter 4 to land on.
- **The chapter contradicts itself.** Body prose uses § notation 11 times ("That is §3's scope-for-names rule", "§4 will want it", "Six of those ten live in §4") while no heading carries a §.

**(b) Checkpoint numbering.** The Attention Budget table lists "☆ Taking Your Bearings #1 / #2 / #3", but all three headings drop the number. Internally inconsistent, and it breaks the ch2/ch3 convention.

Both are single-pass mechanical fixes.

---

## Callback correctness

Thirteen backward references checked against shipped chapter text.

| # | Callback in ch4 | Claim | Verified against | Verdict |
|---|---|---|---|---|
| 1 | §1 `Ch 3 §5 — the API server as the only way in` | — | ch3 L610 `## §5 — 🔵 The Only Door In` | ✅ |
| 2 | §1 `Ch 1 §5 — the Soundings answer that pointed here` | Ch 1 promised Ch 4 would name declarative vs imperative | ch1 **L148, Soundings answer 5** | ❌ **wrong address** |
| 3 | §2 `Ch 3 §6 — the field that holds desired state, and its status counterpart` | Ch 3 withheld the field name and promised Ch 4 | ch3 L784 + L830 — the pointer text matches Ch 3's forward bearing **verbatim** | ✅ exemplary |
| 4 | §2 "Chapter 3 taught… *those objects carry a field that represents the desired state*" | quoted phrasing | ch3 L784, exact | ✅ |
| 5 | §4 `Ch 2 §4 — five ways to reach a private registry` | — | list is at **ch2 L457, inside §3 (Registries, Tags, and Digests)**. ch2 §4 is *The Container Runtime Interface* (L533) | ❌ **wrong section** |
| 6 | §4 "Chapter 2 established that images are immutable" | — | ch2 L334–342 (§2) | ✅ content correct (no bearing given) |
| 7 | §4 "Chapter 2… deferred the most common one to this section" | — | ch2 L459 defers `imagePullSecrets` to Ch 4 §4 | ✅ loop closed |
| 8 | Bearings #2 Q4 answer "re-read Chapter 2 §4" | — | same defect as #5 | ❌ **wrong section** |
| 9 | Bearings #1 Q5 answer "re-read Chapter 3 §5" | etcd / kube-apiserver | ch3 L614 (§5) carries both facts | ✅ |
| 10 | Soundings rubric "re-read Chapter 3 §5–§6" | prerequisites for Q3/Q4 | §5 = the door, §6 = the loop | ✅ precisely right |
| 11 | §6 "Chapter 3 put it in the documentation's words" (*A to C*) | — | ch3 L924/928/942 (§7), quoted three times | ✅ |
| 12 | §6 "the same discipline Chapter 3 applied to 'nobody is in charge'" | Ch 3 audited its own slogan | ch3 L944–946: *"⚠ One precision, because the heading overstates… The accurate claim is narrower and better"* | ✅ **structurally mirrored** — ch4 §6 performs the identical move on its own subtitle |
| 13 | Practice Q3 answer B "Chapter 3's hub-and-spoke pattern" | — | ch3 L614 (§5) | ✅ |

**Fix for #2.** Chapter 1 does not number its sections at all, and if you count content sections its fifth is *"How This Book Is Built"* (L388) — the wrong target. The material is in Chapter 1's Soundings answer block, which sits *before* §1. **Chapter 3 already established the correct citation form for exactly this case** at L932: `*[cross-bearing: see Ch 1 🧭 Soundings A2 — …]*`. Recommended replacement:

```
*[cross-bearing: see Ch 1 🧭 Soundings A5 — the distinction this section names]*
```

**Fix for #5 / #8.** Change both to `Ch 2 §3`. Note that `Ch 2 §4` is not a harmless miss — Chapter 1's Soundings A2 already routes readers to Ch 2 §4 for the Container Runtime Interface, so Chapter 4 currently sends readers to a section about CRI expecting a registry-credentials list.

---

## Retrieval-practice accuracy

Six tagged retrieval items. **All six land on material the named chapter genuinely covers.**

| Item | Tag | Topic | Covered in named chapter? |
|---|---|---|---|
| Bearings #1 Q5 | `ch3` | desired/current state fields; component that stores the object | ✅ ch3 §6 (L784) + §5 (L614) |
| Bearings #2 Q4 | `ch2` | five mechanisms for private-registry credentials | ✅ ch2 §3 (L457) — *topic correct, the answer's "§4" pointer is not* |
| Practice Q1 | `ch3` | kube-apiserver receives, etcd stores | ✅ ch3 §2 / §5 |
| Practice Q2 | `ch3` | controller responds to a changed `spec` | ✅ ch3 §6 (L760, L802) |
| Practice Q3 | `ch3` | Job controller tells the API server; does not run Pods itself | ✅ ch3 §6 (L788) — **verbatim source match**, and Ch 3's own Bearings #3 Q2 (L847) tested the identical fact, making this a correctly spaced re-test rather than a duplicate |
| Practice Q13 | `ch2` | ConfigMap immutability, with distractor A discriminating against ch2's image rule | ✅ ch2 §2 (L336) — the distractor correctly encodes *"build a new image, then recreate the container"* |

Two notes for the author, neither a failure:

- **Soundings Q3 and Q4 are retrieval items in Soundings clothing.** Both are answerable only from Chapter 3, not from general priors. The skill (Part 11, rule 2) requires Soundings to be answerable from prerequisites — Chapter 3 *is* the stated prerequisite, so this is compliant, and the rubric handles it well by naming ch3 §5–§6 as the remediation. Flagging only because it shifts the pre-test's function toward continuity checking.
- **Practice-section count error.** The section intro reads *"Twenty-one questions. **Five** test material from earlier chapters and are tagged as such."* There are 21 questions ✅ but only **four** tagged items in that section (Q1, Q2, Q3, Q13). Either add a fifth or change the word to "Four."

---

## Glossary coverage

### A — Concepts this chapter owns

34 introduced, 30 fully defined in-chapter, 4 partial.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Kubernetes object / "record of intent" | yes — sourced definition | no (harvest verbatim) |
| declarative vs imperative interface | yes — §1, both sides | no — **and this closes the term Ch 3's ledger reserved for Ch 4** |
| imperative commands (technique) | yes — with the "no history" cost | no |
| imperative object configuration | yes | no |
| declarative object configuration | yes | no |
| manifest | yes | no |
| `apiVersion` / `kind` / `metadata` / `spec` | yes — all four, twice (prose + Dead Reckoning) | no |
| `status` | yes — with authorship asymmetry | no |
| name (object) | yes — reusable after deletion | no |
| UID | yes — "distinguish historical occurrences" | no |
| namespace | yes — scope for names | no |
| namespaced vs cluster-scoped | yes | no |
| `default` / `kube-system` / `kube-public` / `kube-node-lease` | yes — all four, with the convention-vs-enforcement correction | no — **closes `kube-system`, reserved for Ch 4 by ch3's ledger** |
| ConfigMap | yes — plus size ceiling, namespace rule, 4 consumption paths, immutability | no |
| Secret | yes — plus the unencrypted-by-default caveat | no |
| base64 encoding | yes — Soundings A6 + §4, explicitly "not encryption" | no |
| `Opaque` | yes — named as the default | no |
| `kubernetes.io/dockerconfigjson` | yes — **closes Ch 2's open loop from L459** | no |
| `imagePullSecrets` | yes | no |
| label | yes — incl. key/value syntax limits | no |
| label selector | yes — "the core grouping primitive" | no |
| equality-based / set-based selectors | yes — operators enumerated | no |
| `matchLabels` / `matchExpressions` | yes — with the exact `In` equivalence | no |
| annotation | yes — plus the value-constraint contrast table | no |
| `kubectl apply` | **partial** — one clause; full surface deferred to Ch 8 | **yes** |
| `kubectl explain` | **partial** — "gets documentation for resources" | **yes** |
| `kubectl api-resources` | **partial** — usage shown, term not defined | **yes** |
| `kubectl scale` | yes — "updates the size of a workload" | no |
| field selector | **partial** — one parenthetical gloss, explicitly marked non-load-bearing | **yes** |

### B — Surfaced here, owned by a later chapter (deferral hygiene)

| Term | Owner per `chapter-lineup.md` | Deferral restated in ch4? |
|---|---|---|
| Pod | Ch 5 | ⚑ **only in The Voyage Ahead** — used ~80× before that point. This is the *same* gap ch3's kb-manifest flagged ("used ~40×, never defined, deferral never restated"). Ch 4 half-closes it. Recommended fix is ch3's: one sentence at first use. |
| custom resource / operator | Ch 6 | ⚑ **no** — `kind: CronTab` "from some vendor's operator" (Bearings #1 Q1) and "a custom resource for a database operator" (§2) carry no bearing |
| PersistentVolume / StorageClass | Ch 11 | ⚑ **no** — used as the canonical cluster-scoped examples in §3, the Fixed Point, and Q7, with no bearing |
| ServiceAccount | Ch 5 (planted) / Ch 12 (full) | partial — bearing to Ch 5 §6 given in §4, but Bearings #2 Q1 answer C asserts a ServiceAccount fact with no bearing |
| Lease | ⚑ **disputed** — ch3's ledger says Ch 5/Ch 12; ch4 bears to Ch 8 §4; the lineup's Ch 8 row says "node lifecycle (…node conditions, leases)" | functional gloss only. **The lineup supports Ch 8; ch3's ledger entry looks stale. Needs one owner.** |
| Deployment / ReplicaSet / Job | Ch 6 | ✅ explicit parenthetical deferral in §2 |
| NetworkPolicy | Ch 10 | ✅ bearing given (and **correct** — see Contradictions #4) |
| RBAC / encryption at rest / TokenRequest | Ch 12 | ✅ bearings given |
| `subPath` | Ch 11 | ✅ bearing given |
| twelve-factor app | Ch 15 | ✅ bearing given |
| ResourceQuota | Ch 8 | ✅ bearing given |
| cluster DNS / FQDN form | Ch 9 | ✅ bearing given, deliberately shallow |
| **reconciliation** | ⚑ open | Ch 3 L804 promised *"when later chapters say **reconciliation**, this closing-the-gap work is exactly what the word names"*, and ch3's ledger logged it as a **GAP**. Ch 4 uses "reconciles"/"reconciler" three times casually and never names the term. **Gap still open.** |

---

## Ethical guardrails check

- [ ] **No fabricated statistics or claims** — ⚑ **CANNOT CERTIFY.** The fact-accuracy stage did not run (see the banner at the top). What I can report from inspection, which is not a substitute: the chapter makes no invented statistics of the "73% of breaches" kind. Every number is documented and tagged (1 MiB, 63/253 characters, 256 KiB, v1.19, v1.22). All 32 distinct `[source: …]` tags resolve to real cached snapshots in `sources/` — I checked every one. The `~6%` chapter weight is explicitly labelled an authored estimate with the CNCF-publishes-no-competency-weights caveat stated inline, which is the correct handling. **Stage 6 must be re-run against `draft-v2.md` before this chapter ships.**
- [x] **Fear-based content uses real examples** — PASS, and notably so. §4's Secret material is genuinely alarming and *every* alarming clause is tagged to Kubernetes' own documentation. No invented breach scenarios. The subject-dignity guardrail (skill v5.7 Part 14) is observed: the "usually at two in the morning" beat is aimed at the practitioner's own experience, not at anyone harmed.
- [x] **Simplification acknowledged** — PASS, strongly. One `— Dead Reckoning` block, plus §1's precision note ("slogans overclaim") and §6's "The honest correction," which audits the chapter's own subtitle. This mirrors ch3 §7's L944 move and is the strongest structural echo between the two chapters.
- [x] **Authority claims cite legitimate sources** — PASS at the referential level. Kubernetes documentation and API reference throughout; all snapshot filenames verified present. Content-level verification is Stage 6's, and it did not run.
- [ ] **"Frequently tested" claims verifiable** — ⚑ **BORDERLINE.** Several unsourced prevalence and frequency assertions: *"the single most common day-one surprise with ConfigMaps"* (§4); *"This pair produces more confident wrong answers than anything else in this chapter"* (§4); *"a piece of knowledge a surprising number of working practitioners have wrong"* (Safe Harbor); *"the detail that gets asked"* and *"the one candidates miss"* (Exam Alert). These are qualitative practitioner judgments in the register the brand licenses, not fabricated statistics — but "the single most common" is a superlative stated as fact. Author call on whether to hedge.
- [ ] **No strawmanning of alternative study methods** — ⚑ **BORDERLINE.** §3 asserts *"more restrained than most preparation material admits"* and *"Preparation material routinely states it as a hard property of the namespace."* This criticises third-party accuracy rather than a study *method*, and on the `kube-public` point it is defensible, but it is an unsourced claim about competitors. Author call.

---

## Contradictions with earlier canon

**1. "Chapter 4 of 15 complete" — the book has 20 chapters.** (Safe Harbor, draft L1176.) `chapter-lineup.md` runs to row 20 (`Full Mock Exam`), with row 19 the synthesis chapter. Chapter 1 (L376) and Chapter 3 (L950) both reference **Chapter 17** by name, so "of 15" is contradicted by shipped text as well as by the plan. Fix to "of 20."

**2. Fifteen forward `§N` bearings into undrafted chapters violate a convention Chapter 3 proposed.** `.pipeline-state/ch-03/kb-manifest.md` (Tier 2, "Convention locks proposed at Chapter 3") records: *"**No `§N` into undrafted chapters** — A cross-bearing may name `§N` only when the target chapter has shipped."* Chapter 3 largely complies (its forward bearings are bare `Ch N`). Chapter 4 pins §-numbers into Ch 5, 6 (×2), 7, 8 (×2), 9 (×2), 10, 11, 12 (×3), 13, and 15. The lock was proposed precisely because this produces the next three findings.

**3. Three Chapter 12 §-number collisions with Chapter 2.** Chapter 2 has already claimed §1–§4 of Chapter 12 for supply-chain topics; Chapter 4 claims §2–§4 for access control:

| Ch 12 § | Chapter 2's claim | Chapter 4's claim |
|---|---|---|
| §2 | signing, attestation, software supply chain (ch2 L393) | why RBAC names subjects instead of selecting them |
| §3 | restricting who can pull what (ch2 L459) | deriving Role / ClusterRole / RoleBinding / ClusterRoleBinding |
| §4 | runtime protection for compute (ch2 L813) | hardening Secrets, and the access-control model behind it |

Both cannot hold. Chapter 12's outline will have to pick, and one shipped chapter will need editing.

**4. `Ch 6 §3` now carries three different topics.** ch1 L435 → *StatefulSets and stable identity*; ch2 L600 → *CRDs and extending the API*; ch4 → *a controller's selector and the Pods it owns*. Chapter 4 adds the third claim to a pre-existing two-way collision.

**5. `Ch 9 §4` collision — and here Chapter 4 is the correct party.** ch2 L871 points to *"Ch 9 §4 — NetworkPolicy"*; ch4 points to *"Ch 9 §4 — cluster DNS, Service records, and FQDNs"* and separately routes NetworkPolicy to *Ch 10 §3*. `chapter-lineup.md` row 10 lists NetworkPolicy under Chapter 10, and ch3's kb-manifest independently records **NetworkPolicy → Ch 10**. **Chapter 4 is right; `chapter-02:871` is wrong and should be retargeted to Ch 10.** Surfacing it here because this gate is where it becomes visible.

Two things I checked and am **not** flagging as contradictions:

- **The "see front matter" promise.** Chapter 4's weight note says the front matter explains how each estimate was derived, and no front-matter file exists in the repo. `chapter-02:132` already makes the identical promise, so this is a **standing book-level dependency**, not a Chapter 4 defect.
- **The epigraph reusing Chapter 3's "A to C" quote.** Deliberate and well-built: it plants at the top what §6 pays off, and §6 names Chapter 3 as the origin. Structured redundancy, not drift.

---

## Recommended fixes

Everything below survived the revision stage. Items 5 and 6 were raised earlier and are carried forward unresolved.

**Blocking**

1. **Re-run Stage 6 (fact-accuracy) against `draft-v2.md`.** Chapter 4 currently has no fact verification of any kind. Nothing else in this list matters as much.
2. **`Ch 2 §4` → `Ch 2 §3`**, in both places (§4 body, Bearings #2 Q4 answer). As written, the pointer collides with Chapter 1's published route to Ch 2 §4 for CRI.
3. **`Ch 1 §5` → `Ch 1 🧭 Soundings A5`.** Chapter 1 has no numbered sections; use the form Chapter 3 established at L932.
4. **"Chapter 4 of 15" → "of 20."** Contradicted by the lineup and by two shipped chapters.

**Author decision required**

5. *(carried forward from Stage 10, still open)* **Anchor `ch04-zenith-declaration-not-order` is malformed** — missing the `fig{MM}` segment. `image-specs.md` L14 proposes `ch04-fig06-declaration-not-order` and notes the draft and specs must change in the same pass or the join key breaks.
6. *(carried forward from Stage 10, still open)* **Figure numbering does not follow document order** — `fig01 → fig02 → fig04 → fig05 → fig03 → zenith`. `image-specs.md` L18 asks the author to renumber or accept.
7. **Section-heading convention.** Adopt `## §N — ⚪ Title` to match ch2/ch3 and to make the two published inbound bearings (`Ch 4 §1`, `Ch 4 §4`) landable — or ratify the new form and sweep ch2/ch3. Do not leave the split. Same pass: restore `#1/#2/#3` to the three Taking Your Bearings headings so they match this chapter's own Attention Budget table.
8. **Ch 12 / Ch 6 §-number collisions** (Contradictions 3 and 4). Cheapest resolution consistent with Chapter 3's proposed lock: demote Chapter 4's forward bearings to bare `Ch N` and let each target chapter's outline assign § numbers. That also prevents the next chapter from adding a fourth claim to `Ch 6 §3`.
9. **Retarget `chapter-02:871`** from `Ch 9 §4 — NetworkPolicy` to Chapter 10. Chapter 4 exposed this; the edit belongs to Chapter 2.
10. **Assign one owner for `Lease`.** The lineup supports Ch 8; ch3's ledger says Ch 5/Ch 12. Update whichever is stale.
11. **Hedge or source the prevalence superlatives** listed under guardrail 5, particularly "the single most common day-one surprise."

**Cheap, mechanical**

12. **"Five test material from earlier chapters" → "Four,"** or tag a fifth. Four are tagged.
13. **Restate the Pod deferral at first use in §1**, not only in The Voyage Ahead — the fix ch3's kb-manifest already recommended for the identical gap.
14. **Add cross-bearings** for *custom resource / operator* (→ Ch 6) and *PersistentVolume / StorageClass* (→ Ch 11). Both are used as load-bearing examples with no forward pointer.
15. **Close the `reconciliation` gap** Chapter 3 opened at L804 — one sentence naming the word where §2 or §6 already describes the behavior.
16. **Re-run `structural_lint.py` against `draft-v2.md`.** `diagnostics/structural.md` reports 0F/0W but audited `draft-v1.md`; the revised draft is ~17 KB longer. I was not able to run it from this stage.
17. *(optional)* Chapters 1, 2, and 3 each carry a **Logbook Entry** sidebar; Chapter 4 carries only an Extended Analogy. Within skill tolerance (1–3 combined), noted for series texture only.

**What the revision stage got right, and should not be undone:** the Chapter 3 §6 handoff (callback #3) reproduces Chapter 3's forward-bearing text verbatim, and §6's "The honest correction" deliberately mirrors Chapter 3 §7's self-audit. Those two are the strongest cross-chapter seams in the book so far.
```