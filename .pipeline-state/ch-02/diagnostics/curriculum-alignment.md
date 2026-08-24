I have everything I need. The audit's central finding: the draft was written **without** Stage 2's research output — Stage 2 could not write files, so its 17 new snapshots never reached `sources/`, and the draft consequently narrowed two sections against gaps the research had already closed.

```markdown
# Curriculum-Alignment Audit — KCNA Chapter 2

**Draft audited:** `.pipeline-state/ch-02/draft-v1.md` (1068 lines, post-voice; `draft-voice.md` does not exist as a separate artifact — the voice stage wrote back into `draft-v1.md`, with `draft-v1-prevoice.md` retained as the pre-voice copy).
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23`, `lf-kcna-exam-page-2026-08-23`, `lf-kcna-program-changes-2026-08-23` (post-2025-11-24 four-domain blueprint).

## A note on what can and cannot be checked

CNCF publishes **domain** weights (44 / 28 / 16 / 12) and the **competency names** inside each domain. It publishes **no sub-objectives beneath a competency** and **no competency-level weights**. There is therefore no authoritative "1.1 / 1.2 / 2.3" objective list to audit against for this chapter, and any table pretending otherwise would be inventing its own authority.

This audit accordingly checks two things:

1. **Published level** — does the draft cover the one competency it claims (Kubernetes Fundamentals → Containerization)?
2. **Contract level** — does the draft deliver the outline's own operational decomposition of that competency (`kb_tags.concepts`, 28 concepts)? This is the only checkable contract that exists.

The chapter's `domain_weight_pct: 9` is authored judgment, not published data. The draft discloses this correctly in its metadata line ("authored allocation — CNCF publishes domain weights, not competency weights"). **That disclosure is correct and should be preserved.**

## Objectives the outline claims to cover

### Published competency

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.4 | Kubernetes Fundamentals → **Containerization** | YES | appropriate |

No other published competency is claimed, and none is required. Container security (D2), container networking (D2), and container storage (D2) are separate competencies correctly routed to Ch 12, Ch 9, and Ch 11.

### Contract level — the outline's 28 concepts

| Concept | Section | Covered? | Depth |
|---|---|---|---|
| `container` | §1 | YES | appropriate |
| `container-vs-virtual-machine` | §1 | YES | appropriate |
| `shared-kernel-isolation` | §1 | YES | appropriate (see Gap 8 — framing unresolved) |
| `container-image` | §2 | YES | appropriate |
| `image-layers` | §2 | **partial** | **shallow** |
| `immutability` | §2 | YES | appropriate |
| `base-image` | §2 | **partial** | **shallow** |
| `buildpacks` | §2 | YES | **deep — over-covered** |
| `registry` | §3 | YES | appropriate |
| `image-tag` | §3 | YES | appropriate (Fixed Point #1) |
| `image-digest` | §3 | YES | appropriate (Fixed Point #1) |
| `latest-tag` | §3 + §6 | YES | appropriate — both halves delivered |
| `container-runtime` | §4 | YES | appropriate |
| `cri` | §4 | YES | appropriate (sourcing at risk — see Gap 3) |
| `containerd` | §4 | YES | appropriate |
| `cri-o` | §4 | YES | appropriate |
| `runc` | §4, §5 | YES | appropriate (sourcing at risk — see Gap 3) |
| `kubelet-runtime-boundary` | §4 | YES | appropriate |
| `oci` | §5 | YES | appropriate (Fixed Point #3) |
| `oci-image-spec` | §5 | YES | appropriate |
| `oci-distribution-spec` | §5 | YES | appropriate |
| `oci-runtime-spec` | §5 | YES | appropriate |
| `filesystem-bundle` | §5 | **partial** | **shallow — named and tested, never defined** |
| `imagepullpolicy` | §6 | YES | appropriate |
| `imagepullbackoff` | §6 | YES | appropriate — recognition-only, correctly scoped to defer diagnosis to Ch 13 |
| `runtimeclass` | §7 | YES | appropriate |
| `sandboxed-runtime` | §7 | YES | appropriate |
| `pluggable-interfaces` | §4, §8 | YES | appropriate |

**24 of 28 appropriate · 3 shallow · 1 over-covered · 0 missing.**

No objective is absent. Every item in the arc outline's "Covers" list for D1.4 appears in the draft. The failures are all depth failures, and three of the four trace to a single mechanical cause documented under *Gaps* below.

**Question-budget compliance (passes):** Soundings 8/8 · Taking Your Bearings 12/12 across three checkpoints · Practice Questions 25/25 · chapter total 45/45. Matches `question_budget` exactly.

## Objectives covered in the draft but NOT in the outline

Drift is modest and mostly confined to distractors. Flagged for author decision; none of it is fabricated, and all of it is source-tagged.

| Material | Where | Belongs to | Assessment |
|---|---|---|---|
| CNCF project **maturity levels** (graduated) | §4 line 428; PQ 18-D, PQ 20-D | D4 Ecosystem — **Ch 17** | Minor. One sentence used as evidence that the CRI socket has two mature occupants, plus two distractors. Defensible; cross-beared. **Keep.** |
| **Docker origin story** — March 2013 lightning talk, "set the stage for orchestration at scale" | §4 🪝 Snag, line 426 | Deployment-era history — **Ch 3** (B2 assignment) | Real drift. The outline's §1 scope boundary says plainly: "Do not narrate the historical progression here." The Snag needs the *four-meanings* point, not the origin date. **Trim.** |
| **Control-plane components** (kube-apiserver, kube-scheduler, kube-controller-manager, kube-proxy) | Bearings #2 Q1 distractors; PQ 15 distractors | Cluster architecture — **Ch 3** | Acceptable. Distractor-only; the correct answer is derivable from §4 alone without knowing them. No reader dependency created. |
| **kubeconfig** | PQ 4-B | D1 Administration — **Ch 3 / Ch 8** | Acceptable. Distractor-only, one-line explanation. |
| **`imagePullSecrets` + Secret type `kubernetes.io/dockerconfigjson`** | §3 line 295 (named, correctly deferred); **PQ 13 as the correct answer** | Secrets — **Ch 4** | Borderline. §3 handles it exactly as instructed. PQ 13 then makes it the *correct answer*, against the outline's forward-compatibility rule ("No item may depend on … Secrets"). It is answerable from §3's list without Secret semantics, so this is a judgment call, not a defect. **Author decision.** |
| **`crictl`** | §4 line 438 | Ch 13 | Fine. Named only, cross-beared. |
| **Runtime security restrictions** | §7 line 635 | D2 Security — **Ch 12** | Fine. One clause, cross-beared. |

## Depth mismatches

No per-concept exam weight is published, so the "weight" column states the weight *basis* honestly rather than inventing a percentage.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D1.4 Containerization (whole) | 44% domain; ~9% authored allocation | deep | OK |
| `imagepullpolicy` (3 policies + 4 defaults) | High — conditional rules, exam-favoured | deep (Dead Reckoning + figure + 3 PQs) | OK — best-calibrated section in the chapter |
| `image-tag` / `image-digest` | High — Fixed Point #1, densest exam surface | deep (5 PQs incl. integrative) | OK |
| `cri` / `kubelet-runtime-boundary` | Highest reuse in the book (Ch 3, 8, 13, 17) | deep (4 PQs, Fixed Point #2) | OK on coverage; **sourcing flagged open in-draft** — see Gap 3 |
| `runtimeclass` | Small surface, high skip-rate | appropriate (2 PQs, motivation before mechanism) | OK — outline's instruction followed exactly |
| `imagepullbackoff` | Recognition tier here; diagnosis is Ch 13 | appropriate | OK — scope discipline held |
| `image-layers` | Load-bearing for digests (§3) and Ch 12 supply chain | **shallow** — qualitative only; dedup, stack order, and cache behaviour all withheld | **under-covered** |
| `base-image` | Planned ⚓ beat; feeds Ch 12 | **shallow** — selection guidance dropped, replaced by build/run split | **under-covered** |
| `filesystem-bundle` | Vocabulary load-bearing in §5 and Bearings #2 Q3 | **shallow** — used as an answer token, never defined | **under-covered (mild)** |
| `buildpacks` | Ecosystem-awareness tier for an associate exam | **deep** — 7 terms defined (buildpack, builder, build image, run image, stack, platform, lifecycle), plus ⚓, plus 🔭, plus **2 of 25 PQs** | **over-covered — consider trimming** |
| OCI **dates** (June 2015, May 2020) | Trivia tier | **2 of 25 PQs** (Q14, Q19) + a 🔭 Closer Look that concedes "depth beyond what the exam asks" | **mildly over-covered** |

**Two structural observations on distribution:**

- **§5 (OCI) is thin on pure items.** The outline allocated 4 practice questions; the draft delivers **1 pure item (Q19)** plus 3 integrative items that touch §5. Coverage is real, but a reader drilling §5 alone has one item. The Buildpacks over-allocation is the natural donor.
- **Integrative shortfall.** The outline requires "**At least 6 of the 25** must require combining two sections." The draft delivers and marks **5** (Q9, Q14, Q20, Q22, Q24) and its own preamble says so: "Five require combining two sections." One short of contract. This matters more than usual here, because with no earlier chapters to retrieve from, cross-section interleaving is this chapter's *only* interleaving.

## Gaps the research stage flagged

**The controlling finding of this audit.** `research-manifest.md` reports G29 **CLOSED**, §4 CRI sourcing **CLOSED**, and `filesystem-bundle` **CLOSED**, via 17 new snapshots (A1–A17). The draft treats all three as **open**, and narrowed §2 and §4 accordingly.

**Verified root cause — the snapshots were never written to disk.**

- The manifest opens with: *"Writes are blocked in this session… The 17 new snapshots in Appendix A must be written to `../Book-KCNA/sources/` before Stage 3 runs."*
- `Book-KCNA/sources/` contains **zero** files matching `*2026-08-24*`. A recursive glob across the entire book repo returns **no files found**. The directory holds only the 87 snapshots dated 2026-08-23.
- The draft's AUTHOR-REVIEW at line 424 asks Stage 2 to fetch `kubernetes.io/docs/setup/production-environment/container-runtimes/`. That is **exactly snapshot A2's `source_url`**. The drafting stage independently requested a source that had already been fetched and embedded one file away.

This is a pipeline-plumbing failure, not an authoring failure. The drafting stage behaved correctly given what it could see, and its restraint — refusing to assert dedup mechanics it could not source — is the right instinct. **Appendix A contains all 17 snapshot bodies with complete frontmatter, so recovery is a mechanical extraction; no re-fetching is needed.**

| Gap | Manifest status | How the draft handled it | Verdict |
|---|---|---|---|
| **G29** — layer mechanics, caching, multi-stage, base-image guidance | **CLOSED** (A4–A6, A9–A12) | Treated as open. §2 narrowed to qualitative layers; base-image ⚓ replaced; `ch02-fig02` left gated; PQ 6 carries a self-flag | **Inappropriate — but not the draft's fault.** Fix by restoring, not by rewriting |
| **G30** — RuntimeClass motivation | **CLOSED**, confirmed | Drafted from cache; motivation before mechanism, Kata/gVisor, handlers, overhead all present | **Correct.** No action |
| **§4 CRI sourcing** (unlisted gap) | **CLOSED** (A1, A2, A3, A17) | Treated as open. Fixed Point #2's containerd→runC hop flagged unsourced, with a proposal to *soften the Fixed Point* | **Inappropriate.** Softening the book's most-retrieved item would be a real loss; A17 sources it directly |
| **`filesystem-bundle` definition** (unlisted gap) | **CLOSED** (A8) | Term used, never defined | **Inappropriate** — mild, one clause fixes it |
| **Trap #30** — no verbatim "an image contains no kernel" | **OPEN — soft** | §2 line 176 *derives* the negative space from §1's sharing model ("it's §1 read in reverse") rather than asserting a quotation | **Correct — exemplary.** Exactly the handling the manifest recommended. Preserve, and warn the fact-accuracy stage not to hunt for a verbatim source |
| **Containerization sub-competency weight** | **OPEN — unchanged** | Disclosed in the metadata line as authored allocation; no in-chapter restatement | **Correct.** No action |
| **Epigraph / Open Question #9** — McLean quote unsourceable | **OPEN — blocks epigraph only** | Refused the unverifiable attribution, shipped an original Lodestar epigraph, left an AUTHOR-REVIEW | **Correct.** Ethical Guardrail #2 upheld. Manifest offers a stronger alternative if wanted: **ISO 668**, a sourced standardization fact that serves §8's argument better than a quote |
| **Open Question #1** — kernel vs. operating system | **RESOLVED by manifest** with a third option: both registers authoritative, differing by speaker; CNCF glossary says "operating system," Docker says "kernel" | Draft carries both but demotes the kernel formulation to "an explicit editorial precision note rather than as a sourced claim," and leaves Ch 1's line-140 comment open | **Over-cautious.** A13/A14 make the sharpening sourced. Unresolved across two chapters, this is what the reconcile pass will surface |

## Recommended fixes

Ordered by severity. R1 is a precondition for R2–R7.

**R1 — Extract Appendix A to `sources/` before any revision drafting.** *(root cause; unblocks 4 gaps)*
Write the 17 snapshot bodies from `research-manifest.md` §Appendix A (lines 192–1050) to `../Book-KCNA/sources/` as `A1…A17`'s named files. Mechanical copy — bodies and frontmatter are complete. Verify with a glob for `*2026-08-24*` returning 17 files. Nothing below is safe to do first.

**R2 — `image-layers`: restore full treatment.** *(under-covered)*
Using A4 (layer = "a changeset that describes a container's filesystem"), A5 ("one or more layers are applied on top of each other"), A6 ("base layer at index 0… subsequent layers MUST follow in stack order"), A9 (reuse "reduce[s] the amount of storage and bandwidth"), A10 ("once a layer changes, all downstream layers need to be rebuilt"). Delete the AUTHOR-REVIEW at line 219. Un-gate `ch02-fig02`'s left half and record **Open Question #2 → option (a)** so Stage 10 does not re-litigate it. **Do not rename the anchor.**

**R3 — `base-image`: restore the planned ⚓ Worth Securing.** *(under-covered)*
A12: "A small image with minimal dependencies can considerably lower the attack surface." Keep the build/run-image split — it is good and sourced — but the selection beat was the outline's plan and is now quotable. Delete the AUTHOR-REVIEW at line 233.

**R4 — Practice Q6: source the dedup claim, keep the item.** *(under-covered, assessment)*
Cite A9 for layer reuse reducing storage and bandwidth. Delete the AUTHOR-REVIEW at line 831. No reframing needed — the item was right, only its warrant was missing. A9's sentence is also Soundings Q4's answer key verbatim.

**R5 — §4 Fixed Point #2: source the chain, do not soften it.** *(sourcing at risk on the book's most-retrieved item)*
A17 (containerd README): "Most interactions with the Linux and Windows container feature sets are handled via runc." This closes the containerd→runC hop end to end. Delete the AUTHOR-REVIEW at line 424 and **reject its softening proposal** — Ch 3, Ch 8, Ch 13, and the Ch 17 secondary Zenith all retrieve this chain as written.

**R6 — §4: name the pluggability pattern on a sourced line.** *(depth of the chapter's highest-reuse concept)*
Quote A1: "The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components." This is cross-cutting theme 6 stated by Kubernetes itself, and it is what lets Ch 9 / Ch 11 / Ch 6 each say "same move again."
⚠ **Scope guard:** take only that sentence and optionally "the kubelet acts as a client… via gRPC." Leave `--container-runtime-endpoint`, the v1-CRI-API version requirement, the 16 MiB gRPC limit, and the `CRIListStreaming` feature gate in the snapshot. None is associate-tier.

**R7 — §5: define `filesystem-bundle` in one clause.** *(under-covered)*
A8: a set of files containing all data and metadata needed for a compliant runtime to operate on it, with `config.json` required at the bundle root. One clause; the three-beat flow then has a defined middle artifact. Optionally anchor §5's ⚠ OCI/CRI hazard on CRI-O's own sentence (A17) — "an implementation of the Kubernetes CRI… to enable using OCI compatible runtimes" — which draws the boundary in a primary source rather than the book's voice, and is the cleanest answer key for Bearings #2 Q3.

**R8 — Trim Buildpacks; redistribute the slot.** *(over-covered)*
Collapse PQ 7 (detect phase) and PQ 8 (builder definition) into **one** item testing the value proposition: source → runnable OCI image without hand-authored build files, CNCF graduated. Verbatim lifecycle-phase and builder-definition recall is platform-engineering depth, not associate tier. Keep §2's prose treatment; it is proportionate. Reassign the freed slot per R9.

**R9 — Close the integrative shortfall (5 → 6).** *(contract breach)*
Add one marked integrative item using the slot freed by R8. Best available pairing is **§2 + §3** (layer structure → content hash → digest identity), which the outline lists as a high-value pairing and which R2 makes fully sourced. A12 supplies the hinge sentence: "you can pin the image version to a specific digest." Update the Practice Questions preamble from "Five" to "Six."

**R10 — Resolve Open Question #1 across both chapters.** *(consistency; reconcile-pass risk)*
Adopt the manifest's third option: keep the kernel sharpening, cite A13 for it, and have §1 name both registers in one clause — kernel as the mechanism, "shares the OS" as the phrasing the exam is likelier to use (CNCF glossary, A14). Note the internal warrant already in cache: `k8s-docs-runtime-class`'s "user-space kernel (such as gVisor)" only parses if the ordinary case is the *host's* kernel. Then **delete Chapter 1's line-140 AUTHOR-REVIEW** so the two chapters agree before reconcile runs.

**R11 — Trim the Docker origin story in §4's Snag.** *(drift into Ch 3)*
Cut the March 2013 lightning-talk sentence and "set the stage for orchestration at scale." The Snag needs only the four-meanings point. If a historical warrant is wanted, re-anchor on A3 (the Kubernetes dockershim FAQ), which documents the misconception directly — but keep it to one Snag and one Soundings answer line. B2 assigns the era narrative to Chapter 3.

**R12 — Author decision: PQ 13's `imagePullSecrets` correct answer.** *(borderline drift into Ch 4)*
The item is answerable from §3's credential-path list, but its correct answer names a Secret type, against the outline's "no item may depend on … Secrets." Either accept it as recognition-tier, or rephrase option B to foreground the credential *path* rather than the Secret type. Low severity; flagging for the author rather than prescribing.

**R13 — Optional: reduce OCI date redundancy.** *(mild over-coverage)*
PQ 14 and PQ 19 both hinge on dates. PQ 14 uses the date as a legitimate discriminator inside an integrative item; PQ 19's date is more nearly trivia. Consider recasting PQ 19 to test governance-body-versus-software (Fixed Point #3) with the date demoted to a distractor cue.

---

**Summary.** Objective coverage is complete — D1.4 is fully addressed and nothing in the outline's claimed scope is missing. Depth is well-calibrated in §3, §4, §6, and §7, and the chapter's scope discipline against later chapters is unusually good. Three under-covered concepts (`image-layers`, `base-image`, `filesystem-bundle`) and one flagged-unsourced Fixed Point all share a single mechanical cause: Stage 2's 17 snapshots were researched, embedded in the manifest, and never written to `sources/`. R1 unblocks all of them and requires no re-fetching. One contract breach (5 integrative items against a required 6) and one over-coverage (Buildpacks) are independent and resolve into each other via R8 + R9.
```