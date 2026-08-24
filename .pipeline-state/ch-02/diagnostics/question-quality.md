I have the full draft. Producing the audit.

```markdown
# Question-Quality Audit — Chapter 2

## Summary

- Chapter type: **content**
- Total questions inspected: **45**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **12** (across 3 checkpoints, 4 + 4 + 4)
  - Practice questions: **25**
- Question budget compliance: **met** (45 / 45, all four categories exact)
- Weak distractors (WARN): **10** (across 9 questions)
- Trap answers that don't target real misconceptions (WARN): **0** — all five B1 traps (#30–#34) are used, each maps to a documented or genuinely observed misconception, and both `[inferred]` traps (#33, #34) are framed as "easy to confuse" with no frequency claim. Grep for `frequently tested` / `commonly missed` returns nothing.
- Missing or incomplete why-wrong explanations (FAIL): **1** (Bearings #2 Q4). One further item is present-but-vague (Practice Q6 option A) — WARN.
- Retrieval-practice spacing: **compliant** (0% required, 0% delivered; first content chapter, [B3] excludes Ch 1)
- Soundings spoiler check: **clean at the stem level** — no ★ Fixed Point text appears in any question stem. **2 answer keys (A5, A6) partially disclose Fixed-Point conclusions** — WARN, not FAIL.
- **Additional structural finding (WARN, high priority):** 7 of 8 Soundings questions are binary. Expected score from pure guessing ≈ 3.5/8, which places a zero-knowledge reader in the "3–5: read at normal pace" band and makes the "0–2: read carefully" band nearly unreachable. The rubric is miscalibrated by construction. See § Soundings calibration.
- **Additional structural finding (WARN):** Practice Question answers appear one blank line below option D, in the same visual block as the stem. Bearings correctly separates its answer key behind a rule. See § Practice answer placement.

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 12 | 12 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3) | 3 | met |
| Practice Questions | 25 | 25 | met |
| **Chapter total** | **45** | **45** | **met** |

Per-section Practice distribution against the outline's plan:

| Section | Planned | Actual (primary) | Note |
|---|---|---|---|
| §1 container vs VM | 3 | 3 (Q1–Q3) | on plan |
| §2 image contents / layers / build | 4 | 5 (Q4–Q8) | **+1** |
| §3 registries / tags / digests | 5 | 4 (Q10–Q13) | **−1**; effective 6 with integratives Q14, Q22 |
| §4 CRI chain | 4 | 4 (Q15–Q18) | on plan |
| §5 OCI | 4 | 4 (Q9, Q14, Q19, Q20) | on plan |
| §6 imagePullPolicy | 3 | 3 (Q21–Q23) | on plan |
| §7 RuntimeClass | 2 | 2 (Q24, Q25) | on plan |

The ±1 drift between §2 and §3 is immaterial — §3's two integrative items more than restore its share. No action needed.

**Integrative-item shortfall (WARN).** The outline sets a floor: *"At least 6 of the 25 must require combining two sections."* The draft delivers **5** (Q9 §2+§5, Q14 §3+§5, Q20 §4+§5, Q22 §3+§6, Q24 §1+§7) and its own lead-in says so ("Five require combining two sections"). Short by 1. This matters more than the raw count suggests: the outline designated within-chapter interleaving as this chapter's *substitute* for cross-chapter retrieval, which is otherwise zero. Recommended addition below.

## Soundings spoiler check

The chapter's three ★ Fixed Points:

- **FP1** (§3): a tag identifies a series and can be moved; a digest is a content hash and is immutable; two pulls of `myapp:v2` a week apart are not guaranteed to be the same bytes.
- **FP2** (§4): kubelet → CRI → containerd/CRI-O → runC → running process; Kubernetes defines the CRI and implements nothing below it.
- **FP3** (§5): OCI is a governance body publishing three specifications — not a runtime, not a company, not a product.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Editing a running container vs rebuilding | no | Immutability carries no ★ marker. Stem asks; A1 answers in one line without the rollback rationale. Clean. |
| 2 | Same tag, one week apart — same bytes? | **stem no / answer key partial** | Stem reuses FP1's own example (`myapp:v2`) but states nothing. A2 = "No, not guaranteed" + cross-bearing. Discloses FP1's *conclusion*, withholds the tag/digest mechanism that is the load-bearing half. Outline sanctioned this explicitly. WARN. |
| 3 | Where an unqualified name resolves from | no | A3 deliberately withholds `docker.io`: "a default registry that Kubernetes assumes when you don't name one." Exemplary answer-key discipline. |
| 4 | Shared base stored once or twice | no | Layers carry no ★. A4 spends two sentences where one would do ("Images are assembled from stacked layers, and a shared base is a shared layer") — minor over-spend, no Fixed Point at risk. |
| 5 | Is Docker specifically required? | **stem no / answer key partial** | A5: "Kubernetes talks to a runtime through an interface, and several different runtimes satisfy it." That is FP2's conceptual core minus the named chain. WARN. |
| 6 | Who defines the image format? | **stem no / answer key partial** | A6: "Not a single company. The format is governed by a standards body." That is one of FP3's three negations, pre-spent. Withholds the OCI name and the three specs. WARN. |
| 7 | Is isolation strength fixed? | no | RuntimeClass carries no ★. A7 withholds the mechanism correctly. |
| 8 | Re-download an already-present image? | no | A8 = "It depends, and what it depends on will surprise you." Best answer key in the block. Clean. |

**Verdict: not a FAIL.** No stem contains or paraphrases Fixed-Point text; the reader can still be genuinely wrong on every item. But three answer keys (A2, A5, A6) hand over the *conclusion* of a Fixed Point the chapter is about to spend properly — exactly the risk the outline's "one line per question, then stop" discipline was written against. A2 and A6 are the easiest to tighten.

**Recommended fixes:**
- **A5** → "No. Several different runtimes can run containers under Kubernetes. §4 explains what makes them interchangeable." (Removes "through an interface," which is FP2's payload.)
- **A6** → "Not a single company. §5 names who does." (Removes "governed by a standards body," which is FP3's first clause.)
- **A2** → leave as is. A yes/no pre-test cannot withhold its yes/no, and the mechanism is intact.

## Soundings calibration (WARN — rubric is miscalibrated by construction)

Seven of eight Soundings questions are answerable by a coin flip:

| Q | Form | Guessable |
|---|---|---|
| 1 | "the intended way… or something else entirely?" | binary |
| 2 | "Are you guaranteed the same bytes?" | binary |
| 3 | "Where does that image get fetched from?" | open — the only genuinely open item |
| 4 | "stored once, or twice?" | binary |
| 5 | "Does that require Docker specifically?" | binary |
| 6 | "A single company, or something else?" | binary |
| 7 | "True or false?" | binary |
| 8 | "does it download it again?" | binary |

A reader with zero domain knowledge scores ≈ 3.5/8 by guessing, landing squarely in **"3–5 right: read at normal pace"** — the band the outline reserves for readers for whom "the material is in reach." The **0–2 "read carefully, in its own session"** band, which is the band this chapter's most vulnerable readers belong in, is reachable only by a reader who guesses badly.

Two further problems compound it. Q6 and Q7 are *self-telegraphing*: "A single company, or something else?" and "Every container… gets the same strength of isolation… True or false?" both use the study-guide convention where the naive absolute is the wrong answer. Test-savvy adults answer both correctly without knowing anything about OCI or RuntimeClass.

**Recommended fix (does not change the question count or the topics):** convert Q2, Q5, Q6 and Q7 to short multiple-choice with three or four options, keeping the same targeted priors. Q7 in particular becomes far better as *"A workload must run untrusted third-party code with a stronger boundary than a normal container gives. What are your options inside one cluster?"* — same prior tested, no coin flip, and it still doesn't spoil §7. Q6 becomes *"Who publishes the specification that defines the container image format?"* with options: the Docker company / the Kubernetes project / an industry standards body / each registry vendor independently.

## Per-question findings

### Bearings #2 Q4: "Match the concern to the specification that standardizes it…"

**Issue:** **FAIL — incomplete why-wrong.** The answer key covers three of four options in a single clause and never states what is wrong with each.

**Distractor analysis:**
- A) i = runtime-spec, ii = image-spec, iii = distribution-spec — full rotation; plausible to a reader who has the three names but no scope mapping
- B) correct
- C) i = distribution-spec, ii = runtime-spec, iii = image-spec — the other full rotation; same plausibility
- D) i = image-spec, ii = runtime-spec, iii = distribution-spec — **the near-miss**: gets (i) right and swaps only (ii) and (iii). This is the tempting distractor for a reader who correctly maps image-spec but hasn't separated "moving it" from "running it," and it is precisely the reader Chapter 17 will later depend on. It gets no individual treatment.

**Why-wrong explanation status:** **present but grouped** — "**A, C, and D** each rotate at least one pairing." A shared heuristic follows, but no option is diagnosed. Violates skill Part 11 ("For EACH question: why correct is correct, why wrong answers are wrong") and the ethical checklist line "Why-wrong explanations provided for all self-assessment checkpoint questions."

**Recommended fix:** split into three lines. Give D its own, and name why it's the near-miss:
> - **A is wrong** on all three: it assigns the artifact's layout to runtime-spec, which governs execution, and pushes the registry API onto image-spec.
> - **C is wrong** on all three in the opposite rotation: it makes distribution-spec responsible for the manifest and runtime-spec responsible for the transfer.
> - **D is wrong** on two, and it is the tempting one because it gets image-spec right. It then swaps *moving* and *running*: the registry API is `distribution-spec` (v1.0, May 2020), and executing an unpacked bundle is `runtime-spec`. If you picked D, the mapping you need is the lifecycle order — the image exists, then it moves, then it runs.

### Practice Q12: "Why does the documentation advise against `:latest` in production?"

**Issue:** Effectively a one-real-option question. The answer key self-reports all three distractors as fabricated.

**Distractor analysis:**
- A) Harder to know which version is running, harder to roll back — correct
- B) "`:latest` images are excluded from registry caching" — borderline. There *is* a real caching interaction (the pull-policy default), so a confused reader could reach for it. Weakest-acceptable.
- C) "`:latest` is reserved for the Kubernetes project's own images" — **implausible**; targets no identifiable misconception
- D) "`:latest` cannot be used with private registries" — **implausible**; the key concedes it ("nothing about `:latest` interacts with registry privacy")

**Why-wrong explanation status:** present and specific.

**Recommended fix:** replace C and D with the two beliefs readers actually hold. C → *"`:latest` always points to the most recently pushed image, so it is guaranteed current"* (a real and widespread belief, and false in a subtle way — it points wherever it was last moved). D → *"`:latest` is re-resolved on every request, so two nodes may run different builds of the same Deployment"* (true-sounding, conflates tag mutability with pull policy, and sets up Q22).

### Practice Q13: "Which is a documented way to supply credentials for a private registry?"

**Issue:** Two of three distractors are implausible, and the source material offered four unused real alternatives.

**Distractor analysis:**
- A) Embedding credentials in the image — acceptable; the circularity is a real beginner error
- B) `imagePullSecrets` referencing a `kubernetes.io/dockerconfigjson` Secret — correct
- C) "`imagePullPolicy: Always`, which prompts an interactive credential request" — **implausible**; an interactive prompt in a declarative control loop is nonsensical to anyone who has seen a manifest
- D) "Adding the credentials to the image's tag" — **implausible**; no identifiable misconception

**Why-wrong explanation status:** present and specific.

**Recommended fix:** §3 names five documented credential paths and the question uses only one. Build the distractors from the *other* real ones, made subtly wrong — e.g. C → *"Configuring the kube-apiserver to authenticate to the registry on the nodes' behalf"* (targets the very common control-plane/node confusion, and the node-configuration path is real but belongs to the node), D → *"Pre-pulling the image on one node, which makes it available cluster-wide"* (pre-pulled images are a real documented path; the "cluster-wide" clause is the error). Both are wrong for reasons a reader can learn from.

### Practice Q25: "A Pod omits `runtimeClassName`. What runs it?"

**Issue:** One weak distractor in an otherwise good item.

**Distractor analysis:**
- A) Pod rejected until a RuntimeClass is specified — plausible to a reader who thinks the field is mandatory
- B) The default runtime handler — correct
- C) The most secure available handler, as a safe default — plausible, and the why-wrong correctly explains that this inverts the tradeoff. Good distractor.
- D) A randomly selected configured handler — **implausible**; targets no belief

**Recommended fix:** D → *"The handler configured on whichever node the scheduler picked"* — plausible (handlers *are* node-level configuration, per §7's two-level indirection), wrong for an instructive reason (the default handler is a cluster-level RuntimeClass concept, and a RuntimeClass can carry `nodeSelector` precisely so this doesn't happen), and it reinforces the indirection §7 teaches.

### Bearings #1 Q1 / Q2: redundant coverage inside a 4-item checkpoint

**Issue:** Two of the checkpoint's four questions test the same discrimination. Q1's correct answer C turns on "an image carries no kernel"; Q1 option A is "specify the required kernel in the image"; Q2 option A is "The host's kernel," and its why-wrong reads in full: "**A is wrong.** See question 1." Fifty percent of the checkpoint's budget lands on trap #30.

Meanwhile the checkpoint tests nothing from §2's immutability material (the chapter's organizing principle, pre-tested by Soundings Q1) and nothing from §2's Buildpacks material.

**Weak distractors in the same two items:**
- Q1 D) "Use a container, since kernel version is negotiated at start-up" — **implausible**; no one believes kernel version is negotiated. The key concedes it: "Nothing about kernel version is negotiated at container start-up."
- Q2 C) "The node's network configuration" — **implausible** as an image-contents belief

**Recommended fix:** keep Q1 (the applied, scenario-framed version), and repurpose Q2 to immutability, which Bearings currently does not touch at all:
> **2.** A running container's application needs a configuration change that must survive the container being replaced. Which describes the correct process?
> A) Edit the file in the container; the change is written to the image's top layer
> B) Build a new image containing the change, then recreate the container from it
> C) Edit the file and restart the container so the change is committed
> D) Edit the file and record it in the Pod spec so it is reapplied on restart

That preserves pre/post symmetry with Soundings Q1, tests trap #31 in the checkpoint rather than only in Practice, and frees Q1 to own trap #30 alone. Then fix Q1's option D → *"Use a container built from a base image matching the required kernel version"* — plausible (base images *do* carry a distribution's userspace, so a reader can reasonably think they carry its kernel), and it defuses trap #30 from a second angle.

### Bearings #1 Q3, Bearings #3 Q1, Bearings #3 Q4: single weak distractor each

- **Bearings #1 Q3 D)** "The bytes may differ, because Kubernetes re-resolves tags on a random schedule" — **implausible**. Replace with *"The bytes may differ, because the kubelet's cache expires and the image is re-pulled"* — plausible (cache mental model), wrong for a learnable reason (caching is keyed on digest, and cache behavior is a pull-policy question, not an identity question), and it usefully separates §3 from §6.
- **Bearings #3 Q1 D)** "Never, because the image is from a private registry" — **implausible**, and it imports a premise the stem never states (nothing marks `internal.registry.example` as private). Replace with *"Always, because `imagePullPolicy` defaults to `Always` whenever a registry hostname is present"* — a plausible half-rule that produces the right answer for the wrong reason, which is exactly what the why-wrong should catch.
- **Bearings #3 Q4 D)** "`imagePullPolicy: Never` for customer workloads, to prevent them from fetching arbitrary images" — **implausible** as an isolation answer; the key itself says "Different axis entirely." Replace with *"Run the customer workloads in a separate namespace with a restrictive NetworkPolicy"* — plausible (a real control, and a real thing teams reach for), wrong for the stated requirement (network segmentation is not a kernel-isolation boundary), and it plants a Ch 9/Ch 12 cross-bearing.

### Practice Q6 option A: vague why-wrong

**Issue:** "**A** is wrong and is the intuition the chapter's Soundings Q4 pre-tests." That names the misconception; it does not say why the option is false. The correct-answer sentence above carries the reasoning, so a reader can recover it, but as a standalone why-wrong it is a pointer.

**Recommended fix:** "**A is wrong.** Both images' manifests reference the same base layer by identity, so the registry and the node each hold one copy, not one per image. Duplication would defeat the reason images are layered at all."

### Practice Q11: degenerate option structure

**Issue:** Options are "A tag / A digest / Both / Neither." Both and Neither are structurally weak — a reader who knows either half eliminates two options for free. The item also tests FP1 at pure recognition level, one checkpoint after Bearings #1 Q3 tested it at application level.

**Recommended fix:** low priority; the redundancy is defensible spaced practice on the chapter's sharpest fact. If tightened, make it four content statements rather than a two-item enumeration — e.g. *"Which statement is correct?"* A) A tag is immutable; a digest can be re-pointed · B) A digest is a content hash and cannot be re-pointed; a tag can be moved · C) Both are immutable once pushed to a registry · D) Both can be moved, but only by the registry operator. D in particular catches the reader who believes mutability is a permissions question rather than a mathematical one.

## Retrieval-practice spacing

- Chapter 2 target: **0%** — first content chapter; skill Part 10's ramp begins at Chapter 3, and [B3] excludes Chapter 1 from the retrieval schedule entirely. The arc callback map records Ch 2 as `—`.
- Actual: **0%** (0 of 12 checkpoint questions tagged `[retrieval: chN]`; grep confirms no retrieval tags anywhere in the draft)
- Status: **compliant**

Two things worth recording positively. First, the draft did **not** manufacture Chapter 1 retrieval to fill the slot — [B3]'s do-not-retrieve list #1 forbids exactly that, and the temptation (Ch 1's exam-mechanics material is trivially quizzable) was real. Second, the substitute the outline specified — within-chapter cross-section interleaving — is present and well chosen: Q20 (§4+§5) and Q22 (§3+§6) are the two best integrative items in the chapter, and Bearings #2 Q3 correctly requires holding §4 and §5 together as the outline's design note demanded.

**Recommended addition (closes the 5-vs-6 integrative shortfall).** The missing pairing is **§2 + §6** — immutability meeting pull behavior, which the draft already gestures at in §6's 🪝 Snag ("which is §2's immutability principle showing up in an unexpected place") but never tests:

> **[integrative: §2 + §6]** A team fixes a bug by rebuilding their image and pushing it under the same tag, `api:v4`, then waits for the running Pods to pick it up. Nothing changes. Which pair of facts explains it?
>
> A) The image was rebuilt but not re-tagged, so the registry rejected the push
> B) `imagePullPolicy` was resolved when the Pod was created and is not updated when the tag later moves; and with a tag other than `:latest` the default is IfNotPresent, so the kubelet never goes looking
> C) Kubernetes caches images by tag, so a moved tag is only detected after the cache expires
> D) The rebuild produced a new digest, and Pods are pinned to the digest they started with

B is correct. D is the strongest distractor — it is *nearly* true and gets the right answer for the wrong mechanism (the Pod is pinned to a reference, not to a resolved digest), which is precisely the discrimination FP1 and §6 jointly install. This item also gives `ImagePullBackOff`'s neighbourhood — "why didn't my image update" — a Practice-tier home it currently lacks.

## Coverage vs concepts

Against `kb_tags.concepts` in the outline frontmatter. `kb_tags.commands` is empty, so there is nothing to check there.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `container` | yes (B1.1, P1, P2, P3) |
| `container-vs-virtual-machine` | yes (B1.1, P1, P2) |
| `shared-kernel-isolation` | yes (B1.1, P1, P2, P24) |
| `container-image` | yes (B1.2, P4) |
| `image-layers` | yes (P6, P9) |
| `immutability` | yes (P5) — **thin: Practice only; no Bearings item.** See Bearings #1 fix above |
| `base-image` | yes (P6, P8-D) — indirectly, via layer sharing and the Buildpacks stack. Base-image *selection* is untaught (AUTHOR-REVIEW, G29 open) and correctly untested |
| `buildpacks` | yes (P7, P8) — well constructed; P8's three distractors each name a different real Buildpacks term |
| `registry` | yes (P10, P13, P14) |
| `image-tag` | yes (B1.3, B1.4, P10, P11, P12, P22) |
| `image-digest` | yes (B1.3, P11, P21) |
| `latest-tag` | yes (P12, P22) |
| `container-runtime` | yes (B2.1, P15, P17) |
| `cri` | yes (B2.1, B2.3, P16, P20) |
| `containerd` | yes (B2.1, P17, P20) |
| `cri-o` | yes (B2.1, P17) |
| `runc` | yes (P17-C, P18) |
| `kubelet-runtime-boundary` | yes (B2.1, P15, P16) |
| `oci` | yes (B2.2, P19) |
| `oci-runtime-spec` | yes (B2.3, B2.4) |
| `oci-image-spec` | yes (B2.4, P9) |
| `oci-distribution-spec` | yes (B2.4, P14) |
| `filesystem-bundle` | yes (B2.3) |
| `imagepullpolicy` | yes (B3.1, B3.2, P21, P22, P23) — **but only 3 of the 4 conditional defaults are ever the correct answer**: no-tag (B3.1), digest (P21), `:latest` (P22). "Any other tag → IfNotPresent" appears only inside why-wrong prose (B3.1-C). Given Figure 2-5 and the Dead Reckoning block both foreground the four-case rule, the fourth case deserves a stem. Cheapest fix: rotate P21 to `myapp:v3.2` instead of a digest, and move the digest case into the new §2+§6 integrative item's distractor set. |
| `imagepullbackoff` | yes (B3.3) — **thin: one recognition item, zero Practice items.** This is a *named Chapter 13 retrieval anchor*; Ch 13 will call it back by name and diagnose it. One item is a fragile encoding to hand forward. Add a Practice item testing what BackOff implies (retry with growing delay, 300s cap) versus what it does not (give up, crash-loop, disk pressure) — the material is already in the Dead Reckoning block. |
| `runtimeclass` | yes (B3.4, P24, P25) |
| `sandboxed-runtime` | yes (B3.4, P24) — Kata/gVisor named in the keys and in P17-D |
| `pluggable-interfaces` | **NO** |

**The one genuine coverage gap: `pluggable-interfaces`.**

The pattern — *Kubernetes defines an interface and lets the ecosystem implement it* — is planted deliberately and repeatedly: §4's ⚓ "Worth Securing" names it and enumerates all four sockets; Figure 2-3 is explicitly designed as a reusable socket motif for Ch 9, Ch 11 and Ch 17; §8's Zenith is built entirely on it; the Chapter Summary's last row is "The pattern | Kubernetes defines interfaces and lets the ecosystem implement them. CRI is the first of four"; and cross-cutting theme 6 (`2 → 9 → 11 → 6 → 17`) makes it half of the book's secondary Zenith.

It is never tested. Practice Q16 tests *CRI is an interface Kubernetes defines* — the instance, not the pattern. Q20 tests the CRI/OCI layering. Nothing asks the reader to recognise the move as a move.

That is the largest question-architecture defect in the chapter, because Chapter 17's Zenith is designed to land as *recognition*, and recognition requires that the reader encoded something to recognise. A planted-but-never-retrieved concept is a concept the reader has read, not one they hold.

**Recommended addition** (§4-scoped, no forward dependency on Ch 9/11/17 content, so it is safe here):

> **[integrative: §4 + §5]** Kubernetes supports containerd, CRI-O, "and any other implementation of the CRI." Which design principle does that phrasing express, and where else does the documentation apply it?
>
> A) A compatibility guarantee — Kubernetes commits to supporting any runtime that has ever worked, and applies the same commitment to deprecated APIs
> B) An extension point — Kubernetes publishes an interface and lets the ecosystem supply implementations, and it does the same for pod networking and for storage
> C) A conformance programme — runtimes are certified by the CNCF, as are storage drivers and network plugins
> D) A vendor-neutrality policy — Kubernetes refuses to name a default runtime, and likewise ships no default networking or storage

B is correct. C is the strongest distractor: CNCF conformance programmes genuinely exist, containerd and CRI-O genuinely *are* CNCF graduated projects (§4 says so), and the reader who has conflated "graduated project" with "certified implementation" is making a real and instructive error. D is plausible to a reader who over-reads the pluggability argument into "Kubernetes ships nothing," which §7's default-handler material contradicts.

This item costs one slot and simultaneously closes the integrative shortfall, so the two fixes can be taken together: adding it plus the §2+§6 item brings integratives to 7 of 27, or to 7 of 25 if two of the weak-distractor items flagged above (P12, P13) are cut rather than repaired.

## Framing note — unsupported prevalence superlatives (low priority)

Four answer keys make superlative claims about misconception prevalence that the book has no data for:

| Line | Claim |
|---|---|
| B1.1-A | "it is the single most common misconception in this chapter" |
| B1.3-A | "This is the prior most readers arrive with" |
| B2.2-A | "this is the most common misconception about the OCI" |
| P16-A | "the single most consequential misreading" |

None of these is an *exam-frequency* claim, so none violates Ethical Guardrail #8 or [B3]'s do-not-retrieve #4 — and the chapter is otherwise scrupulous about this (the Exam Alert closes with an explicit disclosure that the two `[inferred]` traps "appear here because they are conceptually slippery, not because this book has data on how often they show up," and a grep for `frequently tested` / `commonly missed` returns nothing). But "single most common" is a ranking the book cannot defend, and the chapter has already established the honest register elsewhere. Softening to "a common misconception" / "the prior most readers arrive with" → "a prior many readers arrive with" costs nothing and keeps the voice consistent with its own disclosure.

Not counted in the WARN totals.

## Practice answer placement (WARN)

Bearings gets this right: four questions, then `---`, then **Answers with Explanations**. The reader has to commit before seeing the key, which is the entire mechanism of the testing effect (skill Part 10).

Practice Questions do not. Each answer sits one blank line below option D:

```
**1.** Which single architectural difference accounts for...
A) ...
D) ...

> **B.** Containers have relaxed isolation properties...
```

On a phone or tablet — and this book is ebook-primary — the stem, the options and the answer are all on screen at once. Twenty-five questions, twenty-five spoiled attempts. Whatever retrieval value the chapter's largest question block was supposed to carry is substantially forfeited by layout alone.

**Recommended fix:** adopt the Bearings pattern — all 25 stems, then a rule, then a numbered answer key. Alternatively wrap each answer in `<details><summary>Answer</summary>…</details>`, which preserves the per-question adjacency for review passes while still requiring a deliberate reveal on first attempt. The `<details>` route is already proven in this chapter (Soundings uses it correctly) and is the lighter edit.

## What is working

Recording this because a findings list read alone misrepresents the chapter.

- **Bearings #2 is the strongest checkpoint in the chapter.** All sixteen options across its four items map to identifiable beliefs. Q1's distractor set (apiserver / kubelet / runtime / scheduler) is genuinely hard, and naming the kubelet as "the most tempting distractor" in the key is the right call — that *is* the misconception FP2 exists to break. Q3's 2×2 design (governing body × artifact) tests the OCI/CRI boundary at the level Ch 17 will need it.
- **Trap fidelity is clean.** All five B1 traps are deployed, both `[inferred]` traps are framed as "easy to confuse" in every location they appear (§4 Snag, §5 Hazards, Exam Alert table, Bearings #2 Q3 key), and the Exam Alert closes with an explicit disclosure of *why* those two are framed differently. That disclosure is unusual and worth keeping.
- **Practice Q8, Q17, Q20, Q24 are exemplary.** Each builds every distractor from a *real* term in the chapter's own vocabulary — Q8 from platform/export/stack, Q17 from Docker/runC/Kata, Q24 from a "half-right in a misleading way" node-level reading of RuntimeClass. That is what distractor construction should look like, and it is the standard the weak items above should be raised to.
- **Scope discipline holds throughout.** No Bearings or Practice item requires Pod phases, container states, `kubectl describe`, Secrets, or scheduling — all of which are later chapters and all of which §6 and §7 name in passing. Bearings #3 Q3 tests `ImagePullBackOff` recognition without touching Ch 13's diagnostic workflow, exactly as the outline's scope guard required.
```

**Two findings need an author decision before this chapter is signed off:**

1. **Bearings #2 Q4's grouped why-wrong is the only hard FAIL** — one edit, and option D (the near-miss) is the one that needs its own line.
2. **`pluggable-interfaces` is planted five times and tested zero times.** Chapter 17's secondary Zenith is designed to land as recognition; nothing in Chapter 2 gives the reader something to recognise. A proposed item is in the report, and adding it also closes the integrative shortfall (5 delivered against the outline's floor of 6).

The Soundings binary-question calibration issue is not on either list but is the finding with the widest blast radius — a zero-knowledge reader currently scores ~3.5/8 by guessing and is told to "read at normal pace."