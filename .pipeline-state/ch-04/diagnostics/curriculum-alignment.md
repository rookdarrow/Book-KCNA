`Write` isn't in this stage's allowed tools by design — stage output flows through stdout so the orchestrator captures it atomically into `diagnostics/curriculum-alignment.md`. Emitting the artifact:

Stage 7 complete. The draft audited is `draft-v1.md` (the voice stage swaps in place; `draft-voice.md` is never written under that name).

# Curriculum-Alignment Audit — KCNA Chapter 4

**Chapter:** 4 — Records of Intent
**Objective claimed:** D1.1 (Kubernetes Fundamentals / Kubernetes Core Concepts)
**Artifact audited:** `draft-v1.md` (104,386 bytes, 1,095 lines, written 05:04)
**Stage 7 run:** 2026-08-24

---

## Two notes on method, before the tables

**1. The artifact named in the stage prompt does not exist under that name.** The prompt requested `draft-voice.md`; no such file is written. The voice stage swaps in place — it moved the pre-voice draft to `draft-v1-prevoice.md` (04:54) and wrote the voiced output back to `draft-v1.md` (05:04, matching `.draft-voice.md.progress.log`). This audit reads `draft-v1.md`, which **is** the voiced draft. No content was unavailable. Flagging only so the runner's artifact naming can be reconciled; this is pipeline plumbing, not a drafting defect.

**2. There is no sub-objective ID scheme to audit against, and inventing one would be worse than saying so.** CNCF publishes **four domains and twelve competency names, and nothing finer** — no numbered learning objectives, no per-competency weights (`cncf-kcna-curriculum-pdf-2026-08-23`, `lf-kcna-exam-page-2026-08-23`, and `lf-kcna-program-changes-2026-08-23` all agree, and all three are silent below the competency line). "D1.1" is this book's internal handle for *Kubernetes Fundamentals → Kubernetes Core Concepts*, not a CNCF identifier. Every section of the outline claims the same single objective, so a table keyed on objective IDs would be one row saying YES.

The only auditable granularity is the outline's **own** claim set: the arc-outline "Covers" list plus `kb_tags.concepts`. That is what the first table decomposes. This is a reporting choice, not a finding against the chapter.

---

## Objectives the outline claims to cover

Published anchor: **Kubernetes Fundamentals = 44%** of the exam. Kubernetes Core Concepts is one of its four competencies; CNCF publishes no split among them.

| Claimed sub-topic (outline's own claim set) | Covered in draft? | Where | Depth |
|---|---|---|---|
| Objects as persistent entities / "record of intent" | YES | §1 | appropriate |
| `spec` vs `status`, and the authorship asymmetry | YES | §2, Fixed Point | deep — correctly so |
| Manifests; YAML by convention | YES | §2 | appropriate |
| The four fields: `apiVersion` / `kind` / `metadata` / `spec` | YES | §2, Dead Reckoning | deep — correctly so |
| `kubectl apply` | YES | §1, §2 | deliberately shallow (Ch 8 boundary) — appropriate |
| **Object-management techniques** (imperative commands / imperative object config / declarative object config) | **NO** | — | **absent** |
| Object name | YES | §2 | appropriate |
| Object UID | partial | §2 (one word) | shallow |
| Namespaces as a scope for names | YES | §3 | appropriate |
| Namespaces do not nest; one namespace per resource | YES | §3 + Snag | appropriate |
| The four initial namespaces | YES | §3 table | appropriate |
| Namespaced vs cluster-scoped | YES | §3, Fixed Point, fig04 | deep — correctly so |
| Namespace DNS form | YES | §3 (one sentence) | plant only — appropriate by design |
| ConfigMaps: definition, 1 MiB ceiling, same-namespace, 4 consumption paths, immutability | YES | §4 | deep — appropriate |
| Secrets: definition and contrast with ConfigMap | YES | §4 + fig05 | deep — appropriate |
| Secret storage default (unencrypted in etcd; who can read) | YES | §4, Fixed Point | deep — appropriate |
| Secret types table, incl. `dockerconfigjson`, `tls`, SA-token | YES | §4 | appropriate |
| **Secret `data` is base64-encoded** | **NO** | — | **omitted** |
| Secret hardening: the four steps, named and handed to Ch 12 | YES | §4 | appropriate (correct restraint) |
| Labels: definition, syntax, character set | YES | §5 | appropriate |
| Label selectors: equality-based and set-based | YES | §5 + fig03 | deep — correctly so |
| `matchLabels` ≡ `matchExpressions` + `In` | YES | §5 | appropriate |
| Annotations | partial | §5 (~9 lines) | **shallow** |
| `kubectl explain` | YES | §2 | appropriate |
| `kubectl api-resources --namespaced` | YES | §3, Worth Securing | appropriate |
| `kubectl get` (claimed in `kb_tags.commands`) | NO | — | see G-D — correct omission |
| `kubectl create` (claimed in `kb_tags.commands`) | NO | — | falls with the taxonomy above |

**Both pinned cross-bearings resolve.** Ch 1 line 150 → §1 names the declarative/imperative distinction (draft line 143). Ch 2 line 459 → §4 delivers `imagePullSecrets` and `dockerconfigjson` by name and in the open, not buried in the table (draft line 485). Neither published chapter needs editing.

---

## Objectives covered in the draft but NOT in the outline

**Drift is minimal. This draft under-covers; it does not over-reach.** Scope discipline against Chapters 5, 8, 11, and 12 holds throughout — the Secret hardening steps are named and handed off without being taught, `apply` gets exactly one sentence, and the DNS form gets exactly one. That is the outline's instruction followed literally.

One item is genuine and needs an author decision:

- **`subPath` volume-mount update behavior** (line 569, Bearings #2 Q3 answer B). Cites `k8s-docs-volumes-2026-08-23`, a source the outline did not assign to §4, and introduces a Chapter 11 storage concept inside a Chapter 4 answer key. It is doing real pedagogical work — it defuses "it's a volume, so it's live," the most seductive wrong answer in that item — but it is out-of-scope material arriving without a cross-bearing. **Author decision:** keep with an explicit `[cross-bearing: see Ch 11 §3]`, or cut the clause and let the answer rest on the kubelet-at-launch rule alone.

Three further items were checked and are **not** drift:

- Field selectors (line 647) — the outline permitted "one passing mention at most." The draft gives one parenthetical. Compliant.
- API traffic TLS protection (line 1009) and ServiceAccount namespacing (lines 562, 991) — one clause each, both inside distractor rebuttals, both needed to explain why a wrong option is wrong. Acceptable.
- Node conditions/heartbeats (line 406) and Pod ephemerality/UID (line 1091) — forward plants carrying cross-bearings, exactly as specified.

---

## Depth mismatches

Depth is judged against exam weight and downstream contract, not volume. Weight below is the published domain figure where one exists; everything finer is this book's authored estimate (see G-A).

| Sub-topic | Weight signal | Draft depth | Mismatch |
|---|---|---|---|
| Four fields; `spec`/`status` | Highest-confidence testable facts in the competency; retrieved by Ch 5, 6, 13 | deep | OK |
| Namespaced vs cluster-scoped | Load-bearing for Ch 12's RBAC derivation (B3 contract) | deep | OK |
| Label selectors | Retrieved 5× downstream; "core grouping primitive" | deep | OK |
| ConfigMap + Secret | 5 of the chapter's 8 documented traps | deep, at ceiling | OK — justified by trap density |
| **Object-management techniques** | Core-concepts page; cross-cutting theme 4; Ch 14 `apply` vs `helm install` (≥4-back floor), Ch 15 OpenGitOps "declarative" | **absent** | **under-covered — highest priority** |
| **Annotations** | Billed as high-priority topic #5 in the draft's own Exam Alert; assessed twice (Bearings #3 Q3, Q17) | **~9 lines of body prose** | **under-covered vs. its own billing** |
| **Secret base64 encoding** | Pre-tested by Soundings Q6, which promises "§4 will want it" | **omitted** | **under-covered — breaks a pretest arc** |
| Object UID | Voyage Ahead leans on "a different UID" (line 1091) to make the Ch 5 hook land | one word, no gloss | mildly under-covered |
| §6 "The honest correction" (lines 777–787) | Synthesis section; outline says "short" | restates §1's precision note (line 153) at length | **mildly over-covered — this is the budget to reallocate** |

**No topic is over-covered relative to exam weight in a way that warrants cutting for its own sake.** The single over-coverage item is a duplication, and it is worth flagging precisely because it funds two of the under-coverages at zero net length.

**One arc is broken, and it is the clearest defect in the chapter.** Soundings Q6 asks whether base64 is encryption, and its answer key says *"Hold onto that answer; §4 will want it."* §4 never wants it. The outline designed Q6 as the pretest that surfaces the misconception so §4's correction lands against a model the reader has been made to notice — the pretesting effect, deliberately engineered. As drafted, the reader is told to hold a thought that is never collected. That is the same category of failure as an unresolved pinned cross-bearing, and it is caused entirely by the stale-source problem below.

---

## Gaps the research stage flagged

The research manifest lists four standing gaps (G-A–G-D) and declares the outline's three Open Questions **resolved**. Handling:

| Gap | Draft handling | Verdict |
|---|---|---|
| **G-A** — CNCF publishes no per-competency weight; the ~6% is authored | Line 19 carries an explicit disclosure naming the published 44% and stating the 6% is the book's estimate. Never presented as a CNCF figure. | **Handled correctly** |
| **G-B** — LFS250 sub-topic weighting unavailable | Not draft-visible; nothing required. | N/A |
| **G-C** — no numeric size limit published for a Secret | The draft asserts **no** Secret ceiling anywhere. `MaxSecretSize` appears nowhere. Q13 option B ("a Secret, which has no size limit") is rebutted via the sourced *"small amount of sensitive data"* phrasing rather than by inventing a number. The 1 MiB figure appears only against ConfigMap, where it is fully sourced. | **Handled correctly** — this was flagged as the single most likely place for a plausible invented fact to enter the chapter, and it did not |
| **G-D** — `kubectl get -l` invocation not in the cached labels snapshot | Selector *syntax* taught; invocation absent, per guidance. Minor residue: `kb_tags.commands` still claims `kubectl-get`. | **Handled correctly**; metadata cosmetic only |

**The real gap-handling failure is not a research gap at all.** The draft carries three `AUTHOR-REVIEW` comments (lines 151, 456, 659) that narrow §1, §4, and §5 on the stated grounds that the needed sources "were not fetched at Stage 2." **All three sources were fetched, harvested, and on disk at 04:48 — six minutes before the draft stage ran at 04:54:**

- `k8s-docs-object-management-2026-08-24.md` (5,993 bytes) — closes Open Question #1
- `k8s-docs-secrets-good-practices-2026-08-24.md` (3,347 bytes) — closes Open Question #2, and states the security property verbatim: *"Base64 encoding is not an encryption method, it provides no additional confidentiality over plain text."*
- `k8s-docs-annotations-2026-08-24.md` (4,283 bytes) — closes Open Question #3

All three are also present in the Stage 7 cached source set handed to this audit. The draft stage worked from a stale view of `sources/`. This is a **pipeline input defect, not an authoring judgment** — the drafter's reasoning was correct given what it believed it had, and its refusal to write the taxonomy or the base64 claim from memory was exactly the right call under that belief. Every under-coverage in the table above traces to it.

**Retrieval contract held.** 5 retrieval items across a 32-item Bearings+Practice pool (Bearings #1 item 5 and #2 item 4; Practice Q1, Q2, Q12) = 15.6% against B3's 15% target, drawn from Chapters 2–3 only, with all three B3 named anchors placed in their assigned sections. No fix needed.

---

## Recommended fixes

One per issue, in priority order. Fixes 1–3 share a root cause and should be applied together.

**1. §1 — restore the object-management taxonomy.** Delete the `AUTHOR-REVIEW` at line 151. Add the three techniques with the docs' comparison axes (operates on / recommended environment / supported writers), the `kubectl create deployment nginx --image nginx` example, and the quotable warning that an object *"should be managed using only one technique… results in undefined behavior."* Restore the `🔭 Closer Look` the outline gated on this. Source: `k8s-docs-object-management-2026-08-24.md`. Recovers `imperative-object-configuration`, `declarative-object-configuration`, and `kubectl-create`.

**2. §1 — re-source the imperative/declarative definition.** Line 145 currently cites `k8s-docs-custom-resources-2026-08-23` for the core distinction. That page is about CRDs; the object-management page is the canonical home for this claim and is now cached. The swap costs one citation. While there: the object-management page documents imperative commands as *"the recommended way to get started or to run a one-off task"* with the cost *"no history of previous configurations"* — a more honest framing than declarative-good/imperative-bad, and it strengthens §1's existing precision guard.

**3. §4 — restore the base64 clause to the Fixed Point, and close the Soundings Q6 loop.** Delete the `AUTHOR-REVIEW` at line 456. Cite the two halves separately, per research manifest Note 2: mechanism (`data` holds base64-encoded strings) from `k8s-api-ref-secret-v1-2026-08-24.md` or `k8s-docs-secret-config-file-2026-08-24.md`; security property (base64 is not encryption, adds no confidentiality) from `k8s-docs-secrets-good-practices-2026-08-24.md`. **Keep unencrypted-in-etcd as the load-bearing claim and base64 as the supporting clause** — the outline's instinct that the storage claim lands harder was right, and both are now available. One sentence in §4 should explicitly retire Soundings Q6 so the promise at line 87 is collected.

**4. §5 — expand annotations to match their Exam Alert billing.** Delete the `AUTHOR-REVIEW` at line 659. From `k8s-docs-annotations-2026-08-24.md`, add two or three conventional-use examples (build/release info, pointers to monitoring or audit repositories, contact details for the responsible team) and the sharper form of the label/annotation rule: labels are **selectable and constrained** (values capped at 63 characters), annotations are **unselectable and unconstrained** (no character-set restriction, any string including JSON, subject only to a 256 KiB total per object). Heed research Note 5 on density — §5 already carries a Fixed Point, a Hazards block, and a Worth Securing marker, which is why fix 6 exists.

**5. §2 — one clause on UID.** Add that a UID is unique across the whole cluster **and across time** — *"every object created over the whole lifetime of a Kubernetes cluster has a distinct UID… intended to distinguish between historical occurrences of similar entities"* (`k8s-docs-names-and-uids-2026-08-24.md`). This is the non-obvious half and the reason the field exists, and it makes the Voyage Ahead's "replaced by a new, near-identical Pod with a different UID" land as a payoff rather than a detail. **Do not** add the three RFC name standards — below associate tier, and the outline's "do not teach `metadata` exhaustively" guard applies.

**6. §6 — trim "The honest correction" and reallocate.** Lines 777–787 restate the precision note already made at line 153. Compress to the `kubectl scale` example and the one-line narrow claim, both load-bearing; drop the re-listing of `delete`/`exec`/`port-forward`. This frees roughly the length fixes 4 and 5 need, holding the chapter at its current size.

**7. Bearings #2 Q3 — author decision on `subPath`.** Keep the clause with an explicit `[cross-bearing: see Ch 11 §3 — ConfigMap and Secret volumes]`, or cut it. Recommend keeping with the cross-bearing: the misconception it defuses is real, and Ch 11 is already cited three lines later at draft line 530.

**8. Housekeeping (low priority).** Drop `kubectl-get` from `kb_tags.commands` in `outline.md`, or accept it as aspirational per G-D. No draft change.

---

**Net assessment.** Coverage of the claimed objective is strong, and the scope boundaries against Chapters 5, 8, 11, and 12 are held with unusual discipline. Every material gap traces to one cause — the draft stage ran against a stale view of `sources/` and correctly declined to write from memory. Fixes 1–5 are restorations, not rewrites, and all five sources are already on disk.