I have everything I need. Three things materially change what this stage should write, and one of them overturns a premise the chapter and integration report both carry.

# Knowledge-Base Manifest — KCNA Chapter 2

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 2 — Cargo in Standard Crates
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24
**Competency:** D1.4 (Containerization) · **Chapter type:** content · **Authored weight:** ~9%

**Inputs consulted:** finalized `chapter-02-cargo-in-standard-crates.md`, `ch-02/integration.md` (Stage 13), `ch-02/outline.md` frontmatter, `ch-01/kb-manifest.md`, `ch-03/kb-manifest.md` (the Tier 4 handoff), `ch-04` / `ch-05` / `ch-06` / `ch-07/kb-manifest.md`, and **11 snapshots in `../Book-KCNA/sources/` dated 2026-08-24** — see Finding 0.

---

## ⚑ FINDING 0 — The "missing" snapshots are on disk. Five blocking AUTHOR-REVIEWs are stale.

This is the most consequential thing this stage found, and it inverts a premise the chapter states five times and the integration report repeats as pipeline finding #12.

Chapter 2's §1 pipeline note says: *"`../Book-KCNA/sources/` contains only the 87 snapshots dated 2026-08-23; nothing dated 2026-08-24 exists."* **That was true when Stage 2 ran (2026-08-24 01:07). It is not true now.** `sources/` holds **137** files, and the Appendix A items landed at **04:48–04:49 on 2026-08-24** — after Chapter 2's research stage, but *before* its Stage 12 revision (11:09) and Stage 13 integration (15:10). They were almost certainly harvested by Chapter 3's research pass, which fetched the same URL set.

Verified present, read, and content-confirmed against what each AUTHOR-REVIEW asks for:

| Manifest item | File on disk | Closes |
|---|---|---|
| A13 | `docker-docs-what-is-a-container-2026-08-24.md` | §1 kernel register — *"they all share the same kernel"*; *"A VM is an entire operating system with its own kernel"*. The file's own header says it **"RESOLVES CHAPTER 2 OPEN QUESTION #1 and the live AUTHOR-REVIEW at chapter-01 line 140."** |
| A14 | `cncf-glossary-container-2026-08-24.md` | §1 OS register — *"Containers share the same operating system and its machine resources"*; plus the exam authority stating §1's tradeoff and §7's motivation in one sentence: *"Since containers share the same operating system, processes can be considered less secure than alternatives."* |
| A4/A5/A6 | `oci-image-spec-layers-2026-08-24.md` | §2 layer mechanics — *"One or more layers are applied on top of each other to create a complete filesystem."* |
| A9 | `docker-docs-image-layers-2026-08-24.md` | §2 layer sharing **and** Soundings Q4 / Practice Q6 — *"it allows layers to be reused between images"*, which *"reduce[s] the amount of storage and bandwidth required"* |
| A7 | `oci-distribution-spec-2026-08-24.md` | §3 registry + the digest Fixed Point's second authority — Registry, Push, Pull, and *"Digest: a unique identifier created from a cryptographic hash of a Blob's content."* |
| A8 | `oci-runtime-spec-bundle-2026-08-24.md` | §5 filesystem bundle — the spec's own definition, plus `config.json` REQUIRED at bundle root |
| A1 | `k8s-docs-cri-2026-08-24.md` | §4 CRI thesis sentence, verbatim. Carries its own **SCOPE WARNING** matching the chapter's scope guard exactly |
| A17 | `containerd-cri-o-runc-2026-08-24.md` | §4 containerd→runC hop (*"Most interactions… are handled via runc"*) **and** §5's hazard anchor (*"CRI-O is an implementation of the Kubernetes CRI… to enable using OCI… compatible runtimes"*) |
| A3 | `k8s-blog-dockershim-faq-2026-08-24.md` | §4 Snag / Ch 3 §1 gap (integration finding **C4**) |
| A11 / A12 | `docker-docs-multi-stage-…`, `docker-docs-build-best-practices-…` | §2 ⚓ attack-surface sentence and Practice Q26's hinge |

**Also present and unclaimed:** `cncf-glossary-container-image-2026-08-24.md`, `cncf-glossary-containerization-2026-08-24.md`, `k8s-docs-container-runtimes-setup-2026-08-24.md`, `oci-image-spec-manifest-2026-08-24.md`, `oci-image-spec-overview-2026-08-24.md`, `docker-docs-build-cache-2026-08-24.md`.

**What this means practically.** Every "harvest and tag" instruction in the chapter is now a *tagging* job, not a research job. No re-fetch, no extraction from the manifest appendix, no browser session. Nine of the chapter's eleven AUTHOR-REVIEW comments can be discharged against files already on disk. The two that genuinely remain open are the **ISO 668 / ISO 1161 containerization history** (§8 + epigraph — iso.org 403s) and the **gVisor Sentry mechanism** (§7 🔭 — Appendix A never covered it, and the chapter's own defensible fallback is to leave it trimmed).

The shards below are written to the depth the *on-disk cache* supports, and each records which snapshot upgrades which claim. Where the chapter hedges a claim that a now-present snapshot would let it state outright, the shard says so rather than silently promoting it — promotion is a chapter edit, not a Stage 14 write.

---

## ⚑ FINDING 1 — `Book-KCNA/knowledge-base/` does not exist. Six manifests are unapplied. Replay order matters.

```
$ ls C:/dev/lodestar/Book-KCNA/knowledge-base/
ls: cannot access '...': No such file or directory
```

Chapters 1, 3, 4, 5, 6, and 7 all produced `kb-manifest.md` files with `=== WRITE ===` / `=== APPEND ===` blocks. **None reached disk.** Chapter 3's ledger already diagnosed this ("Chapter 1's Stage 14 composed this ledger and nine other KB files, and none of them reached disk — the same executor write failure"). It is now seven stage-runs deep.

This changes the safe shape of my output. **My blocks below are `APPEND`, and an append to a nonexistent file will produce a glossary containing only Chapter 2** — no header, no conventions, no Chapters 1/3–7. Do not replay this manifest in isolation.

**Correct replay order:**

1. `ch-01/kb-manifest.md` — its 7 concept shards **only**. Skip its `glossary.md` / `objective-coverage.md` / `retrieval-log.md` WRITEs; Chapter 3 supersedes all three.
2. `ch-03/kb-manifest.md` — full replay. Its `glossary.md` WRITE is the reconstructed base carrying Chapter 1's tiers verbatim.
3. `ch-04` → `ch-05` → `ch-06` → `ch-07` — appends, in order.
4. **`ch-02` (this manifest) last.** Chapter 2 drafted second but reached Stage 14 seventh; appending in chapter order would misfile it. Its append is written to slot in at the end and is explicit about discharging Chapter 3's Tier 4.

The common factor is write permission on `../Book-KCNA/`. Same fault, same directory, three stages (2, 13, 14). Worth fixing above the per-chapter level — this is the third manifest in a row to say so.

---

## ⚑ FINDING 2 — Chapter 1's `container` entry was held open *for this stage*, and the blocker is now cleared

Chapter 1's ledger carries an explicit instruction addressed to me:

> ⚑ PROVISIONAL WORDING. […] The chapter's "operating system kernel" is a sharpening — more precise and more standard, but not verbatim from the source. **Chapter 2's Stage 14 must NOT lock the sharpened form until this is resolved.**

It is resolved, and not by choosing a winner. A13 and A14 together establish that **both registers are authoritative and they differ by speaker, not by fact** — CNCF (the exam authority) and kubernetes.io say *operating system*; Docker's runtime documentation says *kernel*. Chapter 2 §1 already carries both, names which is which, and says which the exam is likelier to use. That is the correct resolution, and it is now directly citable rather than entailed.

**Action taken:** the `container` entry is promoted from provisional to **canonical, dual-register**, sourced to both snapshots. **Action NOT taken:** I did not edit Chapter 1's shard or draft. The glossary entry records that Chapter 1's provisional flag can be cleared and by which snapshots — clearing it is an author edit.

One residual, and it is small: Chapter 3 line 271 calls the kernel sharpening *"this book's, not the documentation's… our gloss."* With A13 on disk that framing is now wrong — it is Docker's wording, quoted. Recorded under Canon Conflicts.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

**Chapter 2 contributes 63 rows: 44 defined (Tier 1) · 2 convention locks (Tier 2) · 17 reserved (Tier 3).** All eleven of Chapter 3's Tier 4 gap terms are discharged.

### On the rule collision the integration report referred here

Stage 13 asked which rule governs — the stage rule ("defined-in-chapter needs no entry," giving 17) or skill Part 16 ("all technical terms introduced in the book," giving ~57) — and correctly noted Chapter 2 is the book's largest single vocabulary contributor, so the difference is ~40 terms.

**Chapter 1's ledger design already resolves this, and the resolution is not a compromise.** This file is the *working ledger*, not the shipped artifact; the published `glossary.md` at the book root is generated from it at assembly. So the ledger tracks **both**: defined terms get Tier 1 rows with inherited prose, undefined-here terms get Tier 3 rows with a defining chapter and no prose. Part 16's 100-term floor is met from Tier 1 across all chapters; the stage rule's concern — not inventing definitions — is met by Tier 3 carrying none.

Under that design Chapter 2 contributes **44 defined + 17 reserved**, and no author decision is needed. Recording it here because Stage 13 asked, and because Chapters 8–20 will hit the same question.

### Tier 1 — Defined (prose inherited verbatim; **no paraphrase**, per Rule 5)

Full text is in the write block. Summary of what lands, grouped by section:

| § | Terms defined |
|---|---|
| §1 | container *(canonical, dual-register)* · virtual machine *(promoted from Ch 1 partial)* · relaxed isolation · kernel sharing |
| §2 | container image · image layer · base image · layer stacking · immutability (stateless & immutable) · filesystem-layer serialization · buildpack · builder · stack (build/run image pair) · platform (Buildpacks) · lifecycle: detect / build / export · reproducible layers · Cloud Native Buildpacks |
| §3 | image reference · registry hostname default · tag default (`latest`) · tag · digest · `:latest` · registry · `imagePullSecrets` *(partial)* · kubelet credential provider *(partial)* · pre-pulled images |
| §4 | container runtime · CRI (Container Runtime Interface) · containerd · CRI-O · runC · the kubelet→CRI→runtime→runC chain |
| §5 | OCI (Open Container Initiative) · `image-spec` · `distribution-spec` · `runtime-spec` · filesystem bundle · the OCI/CRI boundary |
| §6 | `imagePullPolicy` · `Always` · `IfNotPresent` · `Never` · the four conditional defaults · `ImagePullBackOff` |
| §7 | RuntimeClass · `runtimeClassName` · runtime handler · Kata Containers · gVisor · user-space kernel · Pod overhead *(partial — Ch 7 completes)* |
| §4/§8 | **"Kubernetes defines an interface and lets the ecosystem implement it"** — named pattern *(see Canon Conflict CC-1)* |

**Terms Chapter 2 uses but does NOT re-define** (already canonical in the ledger from a chapter that ran earlier; no duplicate row written):
`kubelet` (Ch 3) · `PodSpec` (Ch 5 full / Ch 3 partial) · `Pod` (Ch 5) · `Secret` / `kubernetes.io/dockerconfigjson` (Ch 4) · `namespace` — Kubernetes sense (Ch 4) · `Deployment` (Ch 6) · `Waiting` container state (Ch 5) · `custom resource` / CRD (Ch 6) · control-plane components (Ch 3).

This corrects the integration report's reserved list, which was compiled against an empty KB and therefore reserved eight terms that six later-running chapters have since defined. Only genuinely-undrafted targets remain reserved.

### Tier 3 — Reserved (surfaced in Ch 2, defined later — **no prose written**)

| Term | Defining chapter | Surfaced at |
|---|---|---|
| `crictl` | Ch 13 §5 | §4 closing pointer |
| CNI (Container Network Interface) | Ch 9 §1 | §4 ⚓ |
| CSI (Container Storage Interface) | Ch 11 | §4 ⚓ |
| device plugin | Ch 17 | §4 ⚓ |
| API extensions | Ch 6 §8 | §4 ⚓ |
| NetworkPolicy | Ch 10 | Bearings #3 Q4 distractor D |
| SBOM / bill of materials | Ch 12 | §2 closing |
| attestation | Ch 12 | §2 🔭 |
| image signing | Ch 12 | §2 🔭 |
| vulnerability scanning | Ch 12 | Practice Q7 rebuttal D |
| supply-chain security | Ch 12 §1 | §2 |
| `nodeSelector` | Ch 7 §3 | §7 |
| toleration | Ch 7 §4 | §7 |
| Pod overhead *(completion)* | Ch 7 §2 | §7 |
| node | Ch 3 §3 | §4 |
| kube-proxy | Ch 3 §3 | §4 |
| union filesystem | *unassigned* — see note | not in chapter |

**Note on `union filesystem`:** not in Chapter 2 and not reserved by any chapter, but `docker-docs-image-layers-2026-08-24` carries it, and it is the mechanism that makes §2's "layers stack into a single filesystem view" true. Flagged as an *available* depth item, not an obligation. A 🔭 Closer Look in §2 is where it would go if wanted.

### Tier 2 — Convention locks proposed at Chapter 2

| Term | Convention | Why |
|---|---|---|
| **`manifest`** | Qualify at every use outside its home chapter: **"image manifest"** (OCI, Ch 2 §2/§5) vs **"Kubernetes manifest"** (Ch 4 §2). Bare `manifest` reserved for the Kubernetes sense from Ch 4 onward. | Chapter 2 is the first chapter to use *both* senses, and uses both unqualified — OCI sense in §2/§5, Kubernetes sense in Bearings #1 Q3 and the §3 Logbook Entry. Integration flagged it; Ch 12 and Ch 15 will use both again. |
| **`namespace`** | Three senses, always qualified except the Kubernetes one: **"Linux namespace"** (§1) · **"registry namespace"** (§3, Practice Q10) · bare **`namespace`** = Kubernetes (Ch 4 §3, canonical). | See **CC-2** — this is a Rule 6 flag, not a free lock. |

---

## Concept shards added at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/`

**15 created, 0 updated, 0 overwritten.** All 15 slugs are unclaimed by Chapters 1, 3, 4, 5, 6, or 7 — verified against every prior manifest's write blocks.

| Shard | Basis | Status |
|---|---|---|
| `container.md` | §1 | created — **closes Ch 1's provisional entry** |
| `container-image.md` | §2 | created |
| `image-layer.md` | §2 | created |
| `image-immutability.md` | §2 | created — Ch 3 Q24 + Ch 5 Q20 retrieval target |
| `tag-vs-digest.md` | §3 | created — chapter's sharpest fact |
| `image-reference.md` | §3 | created |
| `registry.md` | §3 | created — **Ch 4 Bearings Q4 depends on the five-path count** |
| `container-runtime.md` | §4 | created |
| `cri.md` | §4 | created |
| `oci.md` | §5 | created (absorbs `filesystem-bundle`) |
| `imagepullpolicy.md` | §6 | created |
| `imagepullbackoff.md` | §6 | created — Ch 5 + Ch 13 depend |
| `runtimeclass.md` | §7 | created |
| `pluggable-interface-pattern.md` | §4 ⚓ + §8 Zenith | created — **see CC-1** |
| `buildpacks.md` | §2 | created |

---

## ⚑ Canon conflicts (Rule 6) — flagged, not resolved

### CC-1 — Chapter 3 broadens Chapter 2's named pattern past its sourced enumeration

Chapter 3's ledger raised this against a chapter it could not read the Stage 14 output of. Now that both sides exist, I am recording it in `pluggable-interface-pattern.md` **with both readings intact and neither adopted.**

- **Chapter 2 §4 (⚓, the coining site):** *"Kubernetes defines an interface and lets the **ecosystem** implement it."* Sourced enumeration: CRI, CSI, CNI, device plugins, API extensions `[k8s-docs-extending-kubernetes-2026-08-23]`.
- **Chapter 3 §3 (~line 325):** *"Where a good general-purpose component already exists, Kubernetes defines an interface and **uses it** rather than reimplementing it"* — said of etcd **and** the container runtime.

etcd is not in Chapter 2's enumeration, and Kubernetes does not define an etcd interface; it consumes a general-purpose datastore. The claim is true of the runtime and true-but-different of etcd. **Do not merge these two sentences into one shard definition.** The shard records Chapter 2's wording as canonical (it is the coining site, it is sourced, and B3 schedules the pattern for retrieval *by name*) and records Chapter 3's as an adjacent-but-distinct instinct needing a chapter-level fix.

**Compounding, and worth the author's attention:** Chapter 2 §4 tells the reader *"you are about to see it three more times."* Chapter 3 hits the first recurrence, re-derives it in fresh words, and never uses the name or bears back to Ch 2 §4. That is a missed spaced-retrieval event on a theme Ch 17's secondary Zenith depends on.

### CC-2 — `namespace`: three senses, one canonical shard, do not touch it

`concepts/namespace.md` (Ch 4) is canonical for the Kubernetes sense and is **not modified by this stage**. Chapter 2's two other senses get qualified glossary rows only.

Minor adjacent observation, recorded not acted on: Ch 4's namespace shard uses a *registry* analogy — *"Two ships on two different registries can carry the same name."* Chapter 2 establishes `registry` as a container-image term four sections deep. The analogy is fine in isolation and I am not proposing a change; noting it because a reader arriving at Ch 4 straight from Ch 2 has a freshly loaded meaning for that word.

### CC-3 — Chapter 3's "our gloss" framing is now inaccurate

Ch 3 line 271 describes the kernel sharpening as *"this book's, not the documentation's."* With A13 on disk it is Docker's documentation, quotable. One-clause fix in Ch 3; recorded in `container.md` so it isn't lost.

### CC-4 — Objective-registry mismatch in Chapter 7's ledger

Ch 7's book-level allocation table lists **Ch 2 — Containerization | ~9% | D1.1**. Chapter 2's outline frontmatter tags every section `objectives: ["D1.4"]`, and Chapter 1's competency registry assigns **D1.4 Containerization → Ch 2**. D1.4 is correct; Ch 7's row is a transcription slip. Corrected in the objective-coverage append, flagged rather than silently rewritten since it lives in Ch 7's block.

### No conflict found

Chapter 2's `container runtime`, `kubelet`, and `PodSpec` usages match Chapter 3's canonical entries verbatim in substance — same snapshots, same wording. Chapter 5's `container-state.md` (`Waiting`) and Chapter 2 §6's `ImagePullBackOff` agree exactly: Ch 2 supplies the reason, Ch 5 supplies the state. That handoff worked.

---

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`.** Rule 1 — the author promotes candidates to LOCKED. Function tags match the existing file's taxonomy; three proposed *new* tags are marked.

| Function | Excerpt (opening; full passage cited by location) | Recommendation |
|---|---|---|
| **chapter opening (rule-first)** | *"Here is a sentence that should stop you: **Kubernetes cannot run a container.** Not one, not ever, on any cluster you will ever touch. […] That is not a limitation someone forgot to fix. It is the design, it is deliberate, and by the time you finish §4 you will be able to draw it."* (§Why This Chapter Matters) | **Strong.** The current rule-first opening exemplar is CAPM-sourced; this is the first KCNA passage that does the same job with a counterintuitive assertion plus a discharge promise, and the promise is kept in-chapter. |
| **Fixed Point callout** | *"A tag identifies a series and can be moved to point at a different image. A digest is a hash of the image's content and is immutable. Two pulls of `myapp:v2` a week apart are not guaranteed to be the same bytes. Two pulls of an image by digest are."* (§3) | **Strong.** Four sentences, no hedge, the last two convert the distinction into a consequence the reader can test. Best Fixed Point in the drafted book. |
| **Dead Reckoning block** | *"Three pull policies. **IfNotPresent:** the image is pulled only if it is not already present locally. **Always:** every time the kubelet launches a container, it queries the container image registry to resolve the name to an image digest…"* (§6) | **Strong.** Textbook execution of Part 11's facts-only register: whole exam surface stated flat, *then* interpreted. The "now the two things worth saying about it" hinge afterward is the part worth preserving as a pattern. |
| **Navigational Hazards warning** | *"**CRI and OCI are different layers, and conflating them is the hardest discrimination in this chapter.** […] The discipline is to ask which *direction* you're looking. Up toward Kubernetes, that's CRI. Sideways toward the rest of the industry, that's OCI."* (§5) | **Strong.** Names the confusion, refuses to blame the reader for it, then supplies a one-move test rather than a mnemonic. |
| **Extended Analogy** | *"Consider what the world looks like before the standard, because that is the part usually skipped. A ship arrives. In the hold are barrels, sacks, crates of a dozen different sizes… Unloading is slow in a way that has nothing to do with how fast anyone is working."* (§8) | **Strong.** Runs the analogy through the failure mode of the *pre*-standard world, which is what makes the mapping land instead of decorate. Caveat: its historical specifics are the chapter's one open sourcing gap (ISO 668). |
| **wry humor beat** | *"A bare name is not a bare name. `busybox` is three defaults stacked in a trench coat: a registry you didn't name, a namespace you didn't name, and a tag you didn't name."* (§3 🪝) | **Moderate–strong.** Clean subject-dignity compliance — aimed at the abstraction, not at anyone. Slightly more casual than the locked register; include only if the author wants the band widened. |
| **Where-People-Get-Confused** | *"This is the habit that readers with virtual-machine or bare-metal backgrounds find hardest to break, and the reason deserves naming, because the reason is honorable. […] That skill is genuinely valuable and it is genuinely the wrong instinct here."* (§2) | **Strong.** Respects the reader's prior expertise before correcting it. This is the "respect their intelligence" guardrail rendered as prose rather than asserted. |
| **NEW TAG: Logbook Entry (failure narrative)** | *"There is a particular quality of silence in a room where four competent people have just realized that the thing they were treating as an identity was a label the whole time."* (§3) | **Strong, and the file has no exemplar for this function.** Skill §18.15 defines Logbook Entry loosely; six chapters have shipped them with no anchor. **One caveat the author should rule on first:** it is written in first-person plural and reads as lived experience. If house style requires composite anecdotes to be signalled as composite, settle that before locking this as the anchor. |
| **NEW TAG: Zenith synthesis** | *"You have spent this chapter looking at that same move from five angles without necessarily seeing that it was one move. […] Which is why Kubernetes never needed to know what is in the crate."* (§8 ☀️) | **Strong.** Every content chapter requires exactly one Zenith (skill §18.10) and none is anchored. This one re-reads five earlier sections as one decision, which is the function. |
| **NEW TAG: uncertainty signal / derived-not-quoted** | *"**An image contains no kernel.** That is not a separate fact to memorize, and it is deliberately not presented here as a quotation, because no authority states it as a negative. It is §1 read in reverse."* (§2) | **Strong, and unusual enough to be worth a tag.** Part 11's order/truth balance usually shows up as "the simple version / the full picture." This is rarer: the prose tells the reader *why a claim carries no citation* and derives it in the open. Given how much of this pipeline turns on source discipline, having an anchor for it would pay. |

**Not nominated, deliberately:** §1's kernel/OS dual-register passage. It is the best *pedagogy* in the chapter but its shape is dictated by a sourcing accident, so it would anchor a technique rather than a voice.

---

## Objective coverage log

**D1.4 (Containerization) opens and closes in Chapter 2.** Like D1.3, there is no later chapter to absorb a gap. Full detail in the append block; headline:

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.4** | **Chapter 2** | **deep** | **2026-08-24** |

Registry row: `D1.4 | Containerization | Ch 2` → **complete — Ch 2 covered 2026-08-24**, with one recorded scope decision (gVisor mechanism deliberately left at recognition depth) and no coverage shortfall.

**Question-budget correction recorded.** Frontmatter declares `practice_questions: 25` / `total_this_chapter: 45`. Body has **27** practice questions (Q27 present; exactly seven `[integrative:]` tags at Q9/14/20/22/24/26/27, matching the stated claim) and **47** total. Stage 14 and the book-level 300-question floor both read frontmatter, so the book is currently under-counted by two. The coverage log records **actual**, and flags the frontmatter as needing the edit.

---

## Retrieval-practice ledger

**Outbound: 0 items — correct.** B3 excludes Ch 1 and starts the ramp at Ch 3 (10%, drawing from Ch 2). Chapter 2 is the first content chapter; there is nothing earlier to retrieve.

**Inbound: 12 items across Ch 3, 4, 5, 7 — all verified supported by the final draft.** This mattered: Stage 12 revised the chapter *after* those items were written, and a cut passage would have orphaned them. None was cut. The append records each with its anchor.

**Three binding dependencies now recorded so a later edit can't quietly break them:**

1. **§3 must keep listing exactly five private-registry credential paths.** Ch 4 Bearings Q4 says *"one of the **five** mechanisms Chapter 2 listed"* and asks the reader to name two of the other four. Dropping one from §3 breaks a shipped question in a shipped chapter.
2. **§6 must keep "reported as a container in the Waiting state."** Ch 5 Soundings Q8's answer attributes that phrasing to Chapter 2 by name.
3. **§1 must keep "containers are not the unit Kubernetes schedules; something wraps them."** Ch 5 line 307 back-references it in substance.

**Two forward commitments, one already unmet:**

| # | Commitment | Status |
|---|---|---|
| 1 | **Ch 17 §4 collects the four pluggable interfaces.** §8's Zenith stakes the book's closing argument on it and pins it twice (lines 600, 914) | **OPEN + COLLIDING** — Ch 1 line 182 pins the same section for the certification landscape. Ch 17's lineup puts extension-points synthesis fifth and the certification ladder last, which favors Ch 2's claim. Resolve before Ch 17 outlines |
| 2 | **Ch 3 §1 explains the Docker-era shorthand.** §4's 🪝 Snag defers it there | **UNMET — Ch 3 is drafted and does not deliver it.** Three Docker mentions, none explaining why "Kubernetes runs Docker containers" was ever accurate. A3 is now on disk and closes it in one or two sentences; the alternative is softening Ch 2's Snag |

---

## Recommended actions (ranked; none performed by this stage)

1. **Replay the six unapplied manifests in the order given in Finding 1, then this one.** Everything else in the KB is downstream of this.
2. **Fix the executor write permission on `../Book-KCNA/`.** Three stages, three chapters, same directory.
3. **Discharge nine AUTHOR-REVIEWs by tagging, not researching** (Finding 0). This is the cheapest large win available on the chapter — it converts the chapter's most-hedged passages into sourced ones without re-fetching anything.
4. **`Ch 6 §3` → `Ch 6 §8`** (line 600). One token, requested by Chapter 6, not yet made. Note Ch 6's stated reason for not renumbering is based on a Ch 4 pin that does not exist; the real second claimant is Ch 1 line 436, which is also wrong (StatefulSets are §6).
5. **Resolve the Ch 17 §4 collision** before Ch 17 outlines.
6. **Fix the frontmatter question count** 25→27 / 45→47.
7. **Reconcile Ch 1's "The Voyage Ahead" with Ch 2's actual opening** — Ch 1 promises the crate as premise; Ch 2 delivers it as §8 payoff. Both chapters are shipped, so the contradiction is reader-visible.
8. **Decide CC-1** (the named-pattern broadening) before Ch 9, 11, and 17 add three more recurrences to an already-drifting name.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# ═══ CHAPTER 2 — Cargo in Standard Crates (Containerization, D1.4) ═══

Appended 2026-08-24, Stage 14. Chapter 2 drafted second but reached Stage 14 seventh;
this block belongs at the END of the ledger regardless of chapter order.

**⚑ This block discharges "Tier 4 — Chapter 2 gap" above.** All eleven terms Chapter 3
reserved there are now defined below. The Tier 4 table is superseded — keep it for
provenance if you like, but it is no longer a live gap.

Terms added: 63 — 44 defined · 2 conventions · 17 reserved.

**Rule collision resolved (Stage 13 referred it here).** The stage rule says
defined-in-chapter needs no entry (17 terms); skill Part 16 says the book glossary
carries all terms introduced (~57). Chapter 1's ledger design already answers this:
this file is the working ledger, the shipped glossary is generated from it. So the
ledger tracks BOTH — Tier 1 with inherited prose, Tier 3 with a defining chapter and
no prose. Part 16's floor is met from Tier 1; the stage rule's concern (no invented
definitions) is met by Tier 3 carrying none. No author decision needed.

---

## Tier 1 — Defined (prose inherited verbatim from Chapter 2)

### A

**`Always` (imagePullPolicy value)** — "every time the kubelet launches a container, it
queries the container image registry to resolve the name to an image digest; if the
kubelet has a container image with that exact digest cached locally, it uses its cached
image, otherwise it pulls the image with the resolved digest."
[source: k8s-docs-images-2026-08-23] (Ch 2 §6)
> **The name oversells it.** Chapter 2: "`Always` does not mean 'always download.' It
> means always *check*." Always re-resolve; download only on a miss. Chapter 2 calls
> this "a favorite distractor," and Practice Q2/Q22 both exploit it.

### B

**base image** — the layer at the bottom of an image's stack; "the parts that change
least" belong there. Two images built from the same base "name that same base layer,"
so it is "stored once and transferred once, rather than duplicated per image."
(Ch 2 §2)
> Now directly sourceable: `docker-docs-image-layers-2026-08-24` — the format "allows
> layers to be reused between images," which "reduce[s] the amount of storage and
> bandwidth required to distribute the images."

**builder (Buildpacks)** — "an OCI image containing an ordered combination of buildpacks
and a build-time base image, a lifecycle binary, and a reference to a runtime base
image." [source: buildpacks-concepts-2026-08-23] (Ch 2 §2)

**buildpack** — "software that transforms application source code into runnable
artifacts by analyzing the code and determining the best way to build it."
[source: buildpacks-concepts-2026-08-23] (Ch 2 §2)

### C

**Cloud Native Buildpacks** — a CNCF **graduated** project implementing the buildpack
model. [source: buildpacks-concepts-2026-08-23] (Ch 2 §2)

**container** — a repeatable, isolated unit of execution: "Each container that you run
is repeatable; the standardization that comes from having dependencies included means
that you get the same behavior wherever you run it." Containers "decouple applications
from the underlying host infrastructure." Like a VM, "a container has its own
filesystem, share of CPU, memory, process space, and more."
[source: k8s-docs-containers-2026-08-23] [source: k8s-docs-overview-2026-08-23]
(Ch 2 §1 — canonical)

> **★ DUAL REGISTER — both are authoritative; they differ by SPEAKER, not by fact.**
> Chapter 2 §1 carries both and names which is which:
>
> - **"shares the operating system"** — the CNCF glossary (THE EXAM AUTHORITY) and
>   kubernetes.io. "Containers share the same operating system and its machine
>   resources" [source: cncf-glossary-container-2026-08-24]. This is "the phrasing the
>   exam is likeliest to use, and the one to recognize on an answer sheet."
> - **"shares the host's kernel"** — Docker's runtime documentation. "If you run
>   multiple containers, they all share the same kernel"
>   [source: docker-docs-what-is-a-container-2026-08-24]. This is the mechanism.
>
> **Teach the mechanism; ensure the reader recognizes the OS phrasing on the exam.**
>
> ✅ **CLOSES Chapter 1's provisional flag.** Ch 1's entry carried "⚑ PROVISIONAL
> WORDING… Chapter 2's Stage 14 must NOT lock the sharpened form until this is
> resolved." It is resolved — not by picking a winner, but because both snapshots are
> now on disk and establish that the two registers are two speakers, not a conflict.
> **Chapter 1's provisional flag can be cleared by the author.** This stage does not
> edit Chapter 1.
>
> ⚑ **Chapter 3 line 271 needs a one-clause fix.** It calls the kernel sharpening
> "this book's, not the documentation's… our gloss." With A13 on disk it is Docker's
> documentation, quotable. Not a factual conflict — a stale provenance claim.

**container image** — "a ready-to-run software package containing everything needed to
run an application: the code and any runtime it requires, application **and** system
libraries, and default values for any essential settings."
[source: k8s-docs-containers-2026-08-23]
Also: "binary data that encapsulates an application and all its software dependencies;
images are executable software bundles that can run standalone and that make very
well-defined assumptions about their runtime environment."
[source: k8s-docs-images-2026-08-23] (Ch 2 §2)
> **An image contains no kernel.** Chapter 2 marks this as DERIVED, not quoted — "no
> authority states it as a negative. It is §1 read in reverse." Preserve that framing;
> do not attach a source tag to the negative claim.
> **System libraries ARE included** — they belong to the OS *userspace*, which is what
> the image supplies. This is where readers tangle.

**container runtime** — "a fundamental component that empowers Kubernetes to run
containers effectively. It is responsible for managing the execution and lifecycle of
containers within the Kubernetes environment." Kubernetes supports "containerd, CRI-O,
and **any other implementation of the Kubernetes CRI**."
[source: k8s-docs-containers-2026-08-23]
[source: k8s-docs-cluster-architecture-2026-08-23]
A node component: one "must be installed on every node."
[source: k8s-docs-setup-tooling-2026-08-23] (Ch 2 §4)
> The third list item is not padding. The supported set is **open**; the qualifying
> condition is CRI conformance, not membership in a list.
> Agrees verbatim with Ch 3's `node-components.md`. No conflict.

**containerd** — one of the two CRI implementations the Kubernetes documentation names;
a CNCF **graduated** project. [source: k8s-docs-containers-2026-08-23]
[source: cncf-project-maturity-levels-2026-08-23] (Ch 2 §4)
> Upgradeable to a primary-source definition: "containerd is an industry-standard
> container runtime with an emphasis on simplicity, robustness, and portability," and
> "Most interactions with the Linux and Windows container feature sets are handled via
> runc" [source: containerd-cri-o-runc-2026-08-24] — which is the containerd→runC hop
> the chapter's Fixed Point currently asserts without a tag.

**CRI (Container Runtime Interface)** — the interface Kubernetes publishes so that
alternative runtimes can be used. Listed among Kubernetes' infrastructure extension
points as "container runtime (CRI, the Container Runtime Interface, **to support
alternative container runtimes**)." [source: k8s-docs-extending-kubernetes-2026-08-23]
(Ch 2 §4)
> **★ Fixed Point (verbatim — do not reword):**
> "kubelet → CRI → containerd or CRI-O → runC → a running process.
> Kubernetes defines the CRI. It does not implement it. Kubernetes never starts a
> container itself."
> Chapter 2's most-reused item — Ch 3, Ch 8, Ch 13, and Ch 17's secondary Zenith all
> retrieve this chain as written. **Do not soften to a generic "CRI runtime → OCI
> runtime."**
> Thesis sentence now available on disk: "The CRI is a plugin interface which enables
> the kubelet to use a wide variety of container runtimes, without having a need to
> recompile the cluster components" [source: k8s-docs-cri-2026-08-24].

**CRI-O** — the other CRI implementation the documentation names; a CNCF **graduated**
project. [source: k8s-docs-containers-2026-08-23]
[source: cncf-project-maturity-levels-2026-08-23] (Ch 2 §4)
> Primary source states the OCI/CRI boundary in one sentence, both acronyms in their
> correct planes: "CRI-O is an implementation of the Kubernetes CRI (Container Runtime
> Interface) to enable using OCI (Open Container Initiative) compatible runtimes."
> [source: containerd-cri-o-runc-2026-08-24] — the anchor §5's ⚠ callout and Practice
> Q20 both want.

### D

**digest** — "a unique identifier for a specific version of an image, **a hash of the
image's content**," and **immutable**. [source: k8s-docs-images-2026-08-23] (Ch 2 §3)
> Second independent authority now on disk: "Digest: a unique identifier created from a
> cryptographic hash of a Blob's content" [source: oci-distribution-spec-2026-08-24].
> A digest cannot be re-pointed **by anyone, including the registry operator** —
> mutability here is not a permissions question (Practice Q11 D turns on this).

**`distribution-spec` (OCI Distribution Specification)** — reached **v1.0 in May 2020**;
"introduced to standardize the API to distribute container images."
[source: oci-overview-2026-08-23] (Ch 2 §5)
> This is why any registry can serve an image built by any tool.

### F

**filesystem bundle** — "the unpacked, on-disk form of an image: the container's
filesystem contents plus the configuration a runtime needs in order to start it."
*Chapter 2 marks this as a plain-language gloss on `oci-overview`'s "filesystem bundle
that is unpacked on disk," not a quotation.* (Ch 2 §5)
> Specification's own definition now on disk: "a set of files organized in a certain
> way, and containing all the necessary data and metadata for any compliant runtime to
> perform all standard operations against it," with `config.json` REQUIRED at the
> bundle root [source: oci-runtime-spec-bundle-2026-08-24]. Replacing the gloss with
> this is a chapter edit, flagged not made.

### G

**gVisor** — an alternative runtime supplying "a user-space kernel," reachable via
RuntimeClass. [source: k8s-docs-runtime-class-2026-08-23] (Ch 2 §7)
> Depth deliberately capped at recognition. The Sentry / syscall-interception mechanism
> is NOT in the cache and NOT in the research manifest; it needs gvisor.dev. Chapter 2's
> own position: an exam item is likelier to ask *why RuntimeClass exists* than which
> sandbox uses which technique. Leaving it trimmed is defensible for associate tier.

### I

**`IfNotPresent`** — "the image is pulled only if it is not already present locally."
[source: k8s-docs-images-2026-08-23] (Ch 2 §6)

**image layer** — an image arrives as "a set of filesystem layers, described by a
manifest that names them, plus a configuration that says how to start the thing."
The OCI Image Format "encompasses the image manifest, **filesystem layer
serialization**, and image configuration." [source: oci-overview-2026-08-23] (Ch 2 §2)
> Three consequences, all load-bearing downstream:
> 1. **Layers stack in order** — base at the bottom, each applied on top.
> 2. **A shared base is a shared layer** — one identity, one object, stored once.
> 3. **Position determines rebuild cost** — changing a lower layer invalidates
>    everything above it.
> All three now sourceable: "One or more layers are applied on top of each other to
> create a complete filesystem" [source: oci-image-spec-layers-2026-08-24]; "it allows
> layers to be reused between images" [source: docker-docs-image-layers-2026-08-24].

**image reference** — `[registry[:port]/]name[:tag | @digest]`. **Three defaults hide in
a bare name:** omit the registry → "Kubernetes assumes that you mean the Docker public
registry"; omit the tag → "Kubernetes assumes you mean the tag `latest`"; and the
`library` namespace. The documentation's own equivalence: **`busybox` ≡
`docker.io/library/busybox:latest`.** [source: k8s-docs-images-2026-08-23] (Ch 2 §3)

**`imagePullPolicy`** — the field selecting when the kubelet fetches an image. Three
values (`Always`, `IfNotPresent`, `Never`) and **four conditional defaults**, applied
when the field is omitted:
> | Reference form | Default |
> |---|---|
> | `@digest` | IfNotPresent |
> | `:latest` | **Always** |
> | no tag | **Always** |
> | any other tag | IfNotPresent |
>
> "Once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest
> changes later." [source: k8s-docs-images-2026-08-23] (Ch 2 §6)
> **There is no single global default.** Practice Q1 C and Q23 C both trade on the
> assumption that there is.

**`imagePullSecrets`** — one of five documented paths for private-registry credentials;
specified on a Pod, referencing a Secret of type `kubernetes.io/dockerconfigjson`.
*Partial — Chapter 2 names it; the Secret type is defined at Ch 4 §4.*
[source: k8s-docs-images-2026-08-23] (Surfaced Ch 2 §3 · Secret defined Ch 4 §4)

**`ImagePullBackOff`** — "the container could not start because Kubernetes could not
pull the image," from causes "such as an invalid image name or pulling from a private
registry without credentials." **BackOff** = "Kubernetes will keep trying, with an
increasing back-off delay, up to a compiled-in limit of **300 seconds (5 minutes)**."
Reported as a container in the **Waiting** state.
[source: k8s-docs-images-2026-08-23] (Ch 2 §6)
> Agrees exactly with Ch 5's `container-state.md`: Ch 2 owns the reason, Ch 5 owns the
> state. **Ch 5 Soundings Q8 attributes the Waiting-state phrasing to Chapter 2 by
> name — do not drop it from §6.**

**`image-spec` (OCI Image Specification)** — defines the OCI Image Format, "which
encompasses the image manifest, filesystem layer serialization, and image configuration
needed to launch applications on target platforms."
[source: oci-overview-2026-08-23] (Ch 2 §5)

**immutability (stateless and immutable)** — "Containers are intended to be stateless
and immutable: you should not change the code of a container that is already running.
If you have a containerized application and want to make changes, the **correct
process** is to build a new image that includes the change, then recreate the container
to start from the updated image." [source: k8s-docs-containers-2026-08-23] (Ch 2 §2)
> Not "discouraged" — **different in kind.** Build, then recreate. Neither step is edit.
> Payoff: "Image immutability is exactly what makes quick and efficient rollbacks
> possible" [source: k8s-docs-overview-2026-08-23]. Edit in place and there is nothing
> to go back to.
> Retrieval target for Ch 3 Practice Q24 and Ch 5 Practice Q20.

### K

**Kata Containers** — an alternative runtime using **hardware virtualization**,
reachable via RuntimeClass. [source: k8s-docs-runtime-class-2026-08-23] (Ch 2 §7)
> CRI-O "supports runc and Kata Containers as the container runtimes"
> [source: containerd-cri-o-runc-2026-08-24] — a sourced §5→§7 bridge showing Kata
> slots into the SAME socket from §4, not a new mechanism.

**kubelet credential provider** — one of five documented private-registry credential
paths; "fetches credentials dynamically." *Partial — named, not developed.*
[source: k8s-docs-images-2026-08-23] (Ch 2 §3)

### L

**`:latest`** — an ordinary tag with a conventional name. "You should avoid using the
`:latest` tag when deploying containers in production, as it is harder to track which
version of the image is running and more difficult to roll back properly."
[source: k8s-docs-images-2026-08-23] (Ch 2 §3)
> **★ Two problems, one field.** The documented caution names only the first. The second
> is that `:latest` also flips the default `imagePullPolicy` to **Always** (§6). So the
> tag that made you unsure which version is running is also the tag that maximizes the
> number of opportunities for the answer to change.
> It does NOT mean "most recently pushed." It points wherever it was last moved.

**lifecycle (Buildpacks)** — three phases: **detect** (which buildpacks apply),
**build** (compile and assemble), **export** (create the final OCI image with
reproducible layers). [source: buildpacks-concepts-2026-08-23] (Ch 2 §2)

### N

**`Never`** — "the kubelet does not try fetching the image; if the image is somehow
already present locally, the kubelet attempts to start the container, otherwise startup
fails." [source: k8s-docs-images-2026-08-23] (Ch 2 §6)
> **Never a default.** Only ever set explicitly. Practice Q21 C and Q22 C both offer it
> as one.

### O

**OCI (Open Container Initiative)** — "an **open governance structure** for the express
purpose of creating open industry standards around container formats and runtimes,"
established **June 2015** by Docker and other container-industry leaders, operating
under the Linux Foundation. [source: oci-overview-2026-08-23] (Ch 2 §5)
> **★ Fixed Point (verbatim):** "The OCI is a governance body that publishes three
> specifications: the image specification, the distribution specification, and the
> runtime specification. It is not a runtime, not a company, and not a product you
> install."
> Practice Q19 D carries the *correct founding date* with the wrong kind of body —
> which is exactly why the Fixed Point leads with "governance body," not with "2015."

**OCI vs CRI** — the chapter's hardest discrimination. **CRI** is how *Kubernetes* talks
to a runtime; endpoints kubelet↔runtime; a Kubernetes concern. **OCI** is how *images*
are formatted and distributed and how *bundles* are executed; endpoints build tools,
registries, runtimes; an industry concern that "would exist, unchanged, in a world where
Kubernetes was never written." (Ch 2 §5 ⚠)
> The test: "ask which *direction* you're looking. Up toward Kubernetes, that's CRI.
> Sideways toward the rest of the industry, that's OCI."

### P

**platform (Buildpacks)** — "either the `pack` CLI or a CI system," which "orchestrates
the process by invoking the lifecycle binary together with the buildpacks and the
application source to produce a runnable OCI image."
[source: buildpacks-concepts-2026-08-23] (Ch 2 §2)

**pre-pulled images** — one of five private-registry credential paths.
**Per-node**: an image cached on one node does nothing for a Pod scheduled onto another.
[source: k8s-docs-images-2026-08-23] (Ch 2 §3, Practice Q13 D)

### R

**registry** — "where images live between being built and being run. You push there and
nodes pull from there." A distribution layer speaking a standardized API.
[source: k8s-docs-images-2026-08-23] (Ch 2 §3)
> Chapter 2 marks this as paraphrase. Spec-level definitions now on disk:
> Registry = "a service that handles the required APIs defined in this specification";
> Push = "the act of uploading blobs and manifests to a registry"; Pull = "the act of
> downloading blobs and manifests from a registry"
> [source: oci-distribution-spec-2026-08-24].
>
> **★ FIVE credential paths — the count is load-bearing.** (1) configuring nodes to
> authenticate; (2) a kubelet credential provider; (3) pre-pulled images; (4)
> `imagePullSecrets` on a Pod; (5) vendor-specific and local extensions.
> **Ch 4 Bearings Q4 says "one of the FIVE mechanisms Chapter 2 listed" and asks the
> reader to name two of the other four. Do not drop one from §3.**

**relaxed isolation** — containers "have relaxed isolation properties in order to share
the operating system among the applications, and *therefore* containers are considered
lightweight." [source: k8s-docs-overview-2026-08-23] (Ch 2 §1)
> **A tradeoff, not a deficiency** — the docs use exactly the word *relaxed*. Because it
> was a trade, it can be renegotiated per workload (§7). This is the §1→§7 spine.
> The exam authority states the tradeoff and §7's motivation in one sentence: "Since
> containers share the same operating system, processes can be considered less secure
> than alternatives" [source: cncf-glossary-container-2026-08-24].

**reproducible layers** — the export phase produces layers where "the same input
reliably produces the same layer bytes rather than layers that differ run to run
because of timestamps or file ordering." *Chapter 2 marks the gloss on "reproducible" as
the author's, not the specification's.* [source: buildpacks-concepts-2026-08-23]
(Ch 2 §2 🔭)
> The hinge for supply-chain verification: you cannot attest to an artifact whose bytes
> change when nothing changed. → Ch 12 §2.

**runC** — the low-level runtime "Docker donated… to the Open Container Initiative to
serve as the cornerstone of that effort." An OCI runtime "runs a filesystem bundle that
has been unpacked on disk." [source: oci-overview-2026-08-23] (Ch 2 §4, §5)
> Donated TO the OCI — a different relationship from the OCI shipping one (Practice
> Q18 C, Q19 A both turn on this).
> Primary source: runc is "a CLI tool for spawning and running containers on Linux
> according to the OCI specification" [source: containerd-cri-o-runc-2026-08-24].

**runtime handler** — the name of a CRI-implementation configuration on the nodes; a
RuntimeClass names one via its `handler` field.
[source: k8s-docs-runtime-class-2026-08-23] (Ch 2 §7)

**RuntimeClass** — "a feature for selecting the container runtime **configuration** used
to run a Pod's containers." `apiVersion: node.k8s.io/v1`, `kind: RuntimeClass`, with a
`handler` field. Selected per Pod via `runtimeClassName`; "if no `runtimeClassName` is
specified, the default runtime handler is used."
[source: k8s-docs-runtime-class-2026-08-23] (Ch 2 §7)
> **Two levels of indirection:** the Pod names a RuntimeClass; the RuntimeClass names a
> handler an administrator configured. The Pod author never names a runtime. That is
> what makes it self-service rather than arbitrary-runtime-request.
> Motivation before mechanism: "a balance of performance versus security" — hardware
> virtualization (Kata) or a user-space kernel (gVisor), "at the expense of some
> additional overhead."
> Also carries `nodeSelector`, `tolerations`, and **Pod overhead** — all Ch 7 concepts;
> register that they exist.

**`runtime-spec` (OCI Runtime Specification)** — "outlines how to run a 'filesystem
bundle' that is unpacked on disk." [source: oci-overview-2026-08-23] (Ch 2 §5)

### S

**stack (Buildpacks)** — the pairing of the **build image** (the environment in which
buildpacks run) and the **run image** (the base for the final application image).
[source: buildpacks-concepts-2026-08-23] (Ch 2 §2)
> ⚓ The idea worth taking even if you never use Buildpacks: **the environment that
> compiles your application and the environment that runs it do not have to be the
> same, and usually shouldn't be.** Compilers, headers, and build tooling are attack
> surface production has no use for.
> Now sourceable: "None of the build tools required to build the application are
> included in the resulting image" [source: docker-docs-multi-stage-2026-08-24];
> "A small image with minimal dependencies can considerably lower the attack surface"
> [source: docker-docs-build-best-practices-2026-08-24] — which also supplies "you can
> pin the image version to a specific digest," Practice Q26's hinge.

### T

**tag** — "Tags let you identify different versions of the same **series** of images."
**Tags can be moved to point to different images.**
[source: k8s-docs-images-2026-08-23] (Ch 2 §3)

> ### ★★ THE CHAPTER'S SHARPEST FACT — Fixed Point, verbatim, do not reword
>
> **A tag identifies a series and can be moved to point at a different image. A digest
> is a hash of the image's content and is immutable. Two pulls of `myapp:v2` a week
> apart are not guaranteed to be the same bytes. Two pulls of an image by digest are.**
>
> The asymmetry to hold: a digest is *derived from* the image — "you cannot move a
> digest to point at different content, in the same way that you cannot move the number
> 4 to mean 5." A tag is *attached to* the image, and labels come off.

### V

**virtual machine** — "a full machine running all the components, **including its own
operating system**, on top of virtualized hardware."
[source: k8s-docs-overview-2026-08-23] (Ch 2 §1 — promotes Ch 1's partial to full)
> **Derive, don't memorize.** Every container-vs-VM difference follows from that one
> row: booting a guest OS takes time → containers start faster; a guest OS occupies
> disk and memory → container images are smaller; three guest kernels cost three
> baselines → container density is higher. "You do not need three facts. You need one
> fact and the willingness to follow it."
> Also on disk: "A VM is an entire operating system with its own kernel, hardware
> drivers, programs, and applications"
> [source: docker-docs-what-is-a-container-2026-08-24].

### The named pattern

**"Kubernetes defines an interface and lets the ecosystem implement it"** — Chapter 2
§4's ⚓, coined and named deliberately. Sourced enumeration: **CRI** (runtimes), **CNI**
(pod networking), **CSI** (storage types), **device plugins**, **API extensions**.
[source: k8s-docs-extending-kubernetes-2026-08-23] (Ch 2 §4, §8)

> **⚑ CANON CONFLICT — CC-1. Do not merge with Chapter 3's variant. See
> `concepts/pluggable-interface-pattern.md` for both readings.**
>
> Chapter 3 §3 (~line 325) writes, of etcd *and* the runtime: "Where a good
> general-purpose component already exists, Kubernetes defines an interface and **uses
> it** rather than reimplementing it." etcd is not in Chapter 2's enumeration, and
> Kubernetes does not define an etcd interface — it consumes a general-purpose
> datastore. True of the runtime, true-but-different of etcd.
>
> **Chapter 2's wording is canonical**: it is the coining site, it is sourced, and B3
> schedules the pattern for retrieval BY NAME. Chapters 9, 11, and 17 must use this
> exact phrase.
>
> ⚑ **Internal count discrepancy in Chapter 2 itself.** §4's ⚓ says "Four sockets"
> immediately after naming five things. The book's canon is four everywhere else
> (Exam Alert item 5; §8's "Storage does it. Networking does it. The API itself does
> it"; the Chapter Summary's last row). Ch 17's lineup collects **seven** extension
> points. Author decision: drop device plugins from the ⚓, or change "Four sockets" to
> "One design instinct, applied in several places."

---

## Tier 2 — Convention locks proposed at Chapter 2

| Term | Convention | Status |
|---|---|---|
| **`manifest`** | Qualify outside the home chapter: **"image manifest"** (OCI — Ch 2 §2/§5) vs **"Kubernetes manifest"** (Ch 4 §2). Bare `manifest` = the Kubernetes sense from Ch 4 onward. | Proposed — Ch 2 is the first chapter using both, and uses both unqualified (§2/§5 vs Bearings #1 Q3 and the §3 Logbook Entry). Ch 12 and Ch 15 use both again. Recommended chapter fix: one clause in §2. |
| **`namespace`** | Three senses. Always qualify **"Linux namespace"** (Ch 2 §1) and **"registry namespace"** (Ch 2 §3, Practice Q10). Bare `namespace` = Kubernetes, canonical at Ch 4 §3. | Proposed — **see CC-2. `concepts/namespace.md` is Chapter 4's and is NOT modified by this stage.** |

---

## Tier 3 — Reserved (surfaced in Ch 2, defined later — NO definition written)

| Term | Defining chapter | Surfaced at |
|---|---|---|
| `crictl` | Ch 13 §5 | §4 closing pointer |
| CNI (Container Network Interface) | Ch 9 §1 | §4 ⚓ |
| CSI (Container Storage Interface) | Ch 11 | §4 ⚓ |
| device plugin | Ch 17 | §4 ⚓ |
| API extensions | Ch 6 §8 | §4 ⚓ |
| NetworkPolicy | Ch 10 | Bearings #3 Q4 distractor D |
| SBOM / bill of materials | Ch 12 | §2 closing |
| attestation | Ch 12 | §2 🔭 |
| image signing | Ch 12 | §2 🔭 |
| vulnerability scanning | Ch 12 | Practice Q7 rebuttal D |
| supply-chain security | Ch 12 §1 | §2 |
| `nodeSelector` | Ch 7 §3 | §7 |
| toleration | Ch 7 §4 | §7 |
| Pod overhead *(completion)* | Ch 7 §2 | §7 |
| node | Ch 3 §3 | §4 |
| kube-proxy | Ch 3 §3 | §4 (Practice Q15 B) |
| union filesystem | *unassigned* | not in chapter — available depth, see note |

**Note on `union filesystem`:** not used by Chapter 2 and reserved by no chapter, but
`docker-docs-image-layers-2026-08-24` carries it and it is the mechanism making §2's
"layers stack into a single filesystem view" true: "a union filesystem is created where
layers are stacked on top of each other, creating a new and unified view," plus a
per-container directory that "allows the container to make filesystem changes while
allowing the original image layers to remain untouched" — a strong sourced support for
§2's immutability argument. Recorded as available, not owed.

**Already defined elsewhere — Chapter 2 uses these and does NOT re-define them.**
No duplicate rows written. This corrects the Stage 13 reserved list, which was compiled
against an empty KB before six later chapters ran:
`kubelet` (Ch 3) · `PodSpec` (Ch 5 full / Ch 3 partial) · `Pod` (Ch 5) · `Secret` and
`kubernetes.io/dockerconfigjson` (Ch 4) · `namespace` Kubernetes sense (Ch 4) ·
`Deployment` (Ch 6) · `Waiting` container state (Ch 5) · custom resource / CRD (Ch 6) ·
kube-apiserver, kube-scheduler, kube-controller-manager (Ch 3) · `kubeconfig` (Ch 8
reserved; Ch 2 Practice Q4 B glosses it in a distractor rebuttal only).

**Deliberately excluded:** Docker (the company / CLI / build format / historical
runtime) — Chapter 2 §4's "four things wearing one name" is authored framing, explicitly
untagged, and the taxonomy is not a documented one. If the author wants it in the
glossary it needs a source; `k8s-blog-dockershim-faq-2026-08-24` documents the
misconception ("Early versions of Kubernetes only worked with a specific container
runtime: Docker Engine") but that page is dated 2022-02-17 and must not be presented as
current, and the dockershim narrative belongs to Chapter 3.
=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/container.md ===
# Concept: The container

**Home:** Chapter 2 §1 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 1's partial entry AND its ⚑ PROVISIONAL wording flag

## Definition (verbatim)

> Each container that you run is **repeatable**; the standardization that comes from
> having dependencies included means that you get the same behavior wherever you run it.
> [source: k8s-docs-containers-2026-08-23]

> Similar to a VM, a container has **its own filesystem, share of CPU, memory, process
> space, and more**; because containers are decoupled from the underlying
> infrastructure, they are portable across clouds and OS distributions.
> [source: k8s-docs-overview-2026-08-23]

## The proposition is SAMENESS, not speed

Chapter 2 is explicit that the usual selling points are downstream: "It is not
'containers are fast.' It is not 'containers are small.' Speed and size are
consequences. The proposition is *sameness*: the thing that ran on your laptop is the
thing that runs on the node, because the dependencies are not assumptions about the
host. They're contents."

## ★ The dual register — both authoritative, differing by speaker

| Register | Who says it | Wording |
|---|---|---|
| **operating system** | CNCF glossary (**the exam authority**), kubernetes.io | "Containers share the same operating system and its machine resources" [source: cncf-glossary-container-2026-08-24] |
| **kernel** | Docker runtime documentation | "they all share the same kernel" [source: docker-docs-what-is-a-container-2026-08-24] |

**Teach the mechanism (kernel); ensure the reader recognizes the OS phrasing on an
answer sheet.** Everything above the kernel that the application needs — libraries,
files, its view of the process table — comes from the container itself. That is why a
container has its own filesystem and process space while running on somebody else's
kernel.

In-cache entailment Chapter 2 uses where a direct citation was unavailable: Kubernetes
describes a sandboxed runtime as supplying "a user-space kernel (such as gVisor)"
[source: k8s-docs-runtime-class-2026-08-23] — meaningful only if the ordinary case is
the *host's* kernel.

## ✅ Chapter 1's provisional flag is discharged

Chapter 1's ledger held this entry open with an instruction addressed to Chapter 2's
Stage 14: do not lock the sharpened form until resolved. **Resolved** — not by choosing
a register, but because both snapshots are on disk and establish that the difference is
one of speaker, not of fact. Chapter 2 §1 already carries both. The author may clear
Chapter 1's ⚑.

⚑ **Chapter 3 line 271 is now stale.** It calls the kernel sharpening "this book's, not
the documentation's… our gloss." It is Docker's documentation, quotable. One-clause fix.

## Derive the comparison table; don't memorize it

The single most useful move in §1. One architectural choice produces every cited
difference:

| Follows from | Difference |
|---|---|
| Booting a guest OS takes time | VMs start slowly, containers quickly |
| A guest OS occupies disk and memory | VM images large, container images small |
| Three guest kernels = three baselines | Container density is higher |

"You do not need three facts. You need one fact and the willingness to follow it."

## Relaxed isolation is a TRADE

The docs use exactly the word *relaxed* [source: k8s-docs-overview-2026-08-23]. Chapter
2's ⚓ insists this is a tradeoff, not a deficiency — "because it was a trade, it can be
renegotiated per workload." That sentence is the entire §1 → §7 spine.

The exam authority states the tradeoff and §7's motivation together: "Since containers
share the same operating system, processes can be considered less secure than
alternatives" [source: cncf-glossary-container-2026-08-24].

## The misconception this shard exists to kill

**"A container can supply its own kernel."** Bearings #1 Q1 and Practice Q2 both target
it, and distractor D is the tempting form: base images genuinely carry a distribution's
*userspace* — the libraries and files that make an image "look like" Debian or Alpine.
They do not carry that distribution's kernel. **Choosing a base image changes what is
above the kernel, never the kernel itself.**

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 2 §2** | "An image contains no kernel" is this shard read in reverse — keep it marked as DERIVED, not quoted |
| **Ch 2 §7** | RuntimeClass is the renegotiation of the trade named here |
| **Ch 3** | Deployment eras + Practice Q2 retrieve the shared-OS fact |
| **Ch 5** | "Containers are not the unit Kubernetes schedules; something wraps them" — §1's forward plant, back-referenced at Ch 5 line 307 |

## Related

[[container-image]] · [[image-immutability]] · [[runtimeclass]] · [[container-runtime]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/container-image.md ===
# Concept: The container image

**Home:** Chapter 2 §2 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "container image"

## Definition (verbatim)

> A container image is a **ready-to-run software package containing everything needed to
> run an application**: the code and any runtime it requires, application **and system**
> libraries, and default values for any essential settings.
> [source: k8s-docs-containers-2026-08-23]

> A container image represents binary data that encapsulates an application and all its
> software dependencies; images are executable software bundles that can run standalone
> and that make **very well-defined assumptions about their runtime environment**.
> [source: k8s-docs-images-2026-08-23]

## The negative space is the teaching

**An image contains no kernel.**

⚑ **Chapter 2 deliberately does NOT source this, and the framing must be preserved.**
Its exact words: "That is not a separate fact to memorize, and it is deliberately not
presented here as a quotation, because no authority states it as a negative. It is §1
read in reverse." A shipped kernel would have to be booted, and booting is precisely
what a VM does and a container does not.

**Do not attach a source tag to the negative claim.** It is a rare, clean instance of
skill Part 11's order/truth balance, and it is nominated as a voice exemplar for exactly
that reason.

## Where readers tangle: system libraries

System libraries **are** included [source: k8s-docs-containers-2026-08-23], which feels
like a contradiction because they feel like part of the OS. They belong to the operating
system's **userspace**, and userspace is exactly what the image supplies. Kernel below,
everything above it in the crate.

## "Very well-defined assumptions" is doing quiet work

An image is not self-sufficient. It is *explicit* about what it expects from underneath.
The largest thing it expects is the one thing it does not carry.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 3** | Practice Q25 is a `[retrieval: ch2]` item testing image contents — verified supported |
| **Ch 12** | Supply chain attaches to everything here; §2 defers it explicitly |
| **Ch 13** | Failed-image-pull diagnosis assumes the reader knows what an image is |

## Related

[[container]] · [[image-layer]] · [[image-immutability]] · [[image-reference]] ·
[[buildpacks]] · [[oci]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/image-layer.md ===
# Concept: Image layers

**Home:** Chapter 2 §2 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "image layer"

## Definition (verbatim, as the chapter has it)

> The OCI Image Format encompasses the image manifest, **filesystem layer
> serialization**, and image configuration needed to launch applications on target
> platforms. [source: oci-overview-2026-08-23]

Chapter 2's rendering: the contents arrive as a set of filesystem layers, described by a
manifest that names them, plus a configuration that says how to start the thing.

## Three consequences, all load-bearing

**1. The layers stack, in order.** The manifest lists them as an ordered set — a base at
the bottom, each subsequent layer applied on top. The image you run is that stack
resolved into a single filesystem view.

**2. A shared base is a shared layer.** Two images built from the same base name the
same base layer in both manifests. One identity → one object: **stored once and
transferred once**, not duplicated per image.

**3. Position determines rebuild cost.** Changing a lower layer invalidates everything
above it. Hence the convention: least-changing parts at the bottom.

## ⚑ Sourcing status — the closing snapshots ARE on disk

Chapter 2 §2 carries an AUTHOR-REVIEW saying these three claims rest on snapshots Stage
2 could not write, leaving only `oci-overview`'s phrase "filesystem layer serialization"
on disk. **That is no longer true.** Both files landed 2026-08-24 04:49:

- Ordering: "One or more layers are applied on top of each other to create a complete
  filesystem" [source: oci-image-spec-layers-2026-08-24]. Same page also defines a layer
  as a serialized set of filesystem changes — "Additions, Modifications, Removals."
- Sharing: the format "allows layers to be reused between images," which "reduce[s] the
  amount of storage and bandwidth required to distribute the images"
  [source: docker-docs-image-layers-2026-08-24]. **This snapshot's own header marks it
  as the Soundings Q4 answer key**, and it also closes Practice Q6's rebuttal of
  distractor A.
- Immutability of layers themselves: "each of these layers, once created, are immutable"
  [source: docker-docs-image-layers-2026-08-24].

⚑ **Rebuild cost is the one claim still unsourced.** The Docker page demonstrates
ordering with a five-layer example but the extractor marked its ordering paragraph
"EXTRACTOR SUMMARY — NOT VERBATIM. Re-verify before quoting." Do not quote it. The claim
follows from the ordering citation as an entailment, which is how §2 should carry it.

## Scope guard — do NOT narrow this subsection

The research manifest resolved Open Question #2 to option (a): **keep the
`ch02-fig02-image-layers-and-digests` anchor and keep both halves of the figure.**
Layers are load-bearing for §3's digest concept and for Chapter 12's supply-chain
material.

## Available depth, not owed

`union filesystem` — "a union filesystem is created where layers are stacked on top of
each other, creating a new and unified view," plus a per-container directory that
"allows the container to make filesystem changes while allowing the original image
layers to remain untouched" [source: docker-docs-image-layers-2026-08-24]. That second
sentence is a strong sourced support for §2's immutability argument. 🔭 material at most.
`whiteout files` (`.wh.` prefix) are below KCNA's waterline — cut without regret.

## Related

[[container-image]] · [[tag-vs-digest]] · [[oci]] · [[image-immutability]] ·
[[buildpacks]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/image-immutability.md ===
# Concept: Immutability — build a new image, recreate the container

**Home:** Chapter 2 §2 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "immutability (stateless & immutable)"
**Retrieval target:** Ch 3 Practice Q24 · Ch 5 Practice Q20

## Definition (verbatim)

> Containers are intended to be **stateless and immutable**: you should not change the
> code of a container that is already running. If you have a containerized application
> and want to make changes, the **correct process** is to build a new image that
> includes the change, then recreate the container to start from the updated image.
> [source: k8s-docs-containers-2026-08-23]

## Read the SHAPE of that instruction

Chapter 2's key observation: "It does not say 'editing a running container is
discouraged.' It says the *correct process* is different in kind: build, then recreate.
Two steps, neither of which is 'edit.'"

This is a rule, not a preference. Answer keys should reject "edit then snapshot" and
"edit then commit" on mechanism, not on style.

## Why the wrong instinct is honorable

The passage worth preserving intact (and nominated as a voice exemplar):

> If you have spent years administering long-lived servers, the skill you built was
> *repair*: log in, diagnose, fix in place, verify. That skill is genuinely valuable and
> it is genuinely the wrong instinct here. […] Repair-in-place produces a running thing
> that no image can reproduce, which forfeits the one property you adopted containers to
> get: sameness.

## The payoff is concrete

> Image immutability is exactly what makes quick and efficient **rollbacks** possible.
> [source: k8s-docs-overview-2026-08-23]

"You can go back to the previous version because the previous version still exists,
unchanged, as a distinct artifact. Edit containers in place and there is nothing to go
back to."

## Sourced support now available

"When the union filesystem is created, in addition to the image layers, a directory is
created specifically for the running container. This allows the container to make
filesystem changes **while allowing the original image layers to remain untouched**"
[source: docker-docs-image-layers-2026-08-24]. This closes the mechanism half of
Bearings #1 Q2 distractor A ("changes are written to the image's top layer" — they are
not; the image layers are never mutated).

## Where else it surfaces

- **§6, unexpectedly:** "Once a Pod is created, `imagePullPolicy` is not updated if the
  image's tag or digest changes later" — Chapter 2 calls this "§2's immutability
  principle showing up in an unexpected place." If you need new behavior, you need a new
  Pod.
- **Ch 4 Practice Q13** invokes it analogically to rebut a ConfigMap-immutability
  distractor. Tagged `[retrieval: ch2]`; defensible as interleaving, not accurate as
  retrieval. Ch 4's issue, noted here for provenance.

## Related

[[container-image]] · [[image-layer]] · [[tag-vs-digest]] · [[imagepullpolicy]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/tag-vs-digest.md ===
# Concept: Tag versus digest — the chapter's sharpest fact

**Home:** Chapter 2 §3 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "image layer / tag vs digest"

## Definition (verbatim)

> Tags let you identify different versions of the **same series** of images. Digests are
> a unique identifier for a specific version of an image, **a hash of the image's
> content**, and are **immutable**; **tags can be moved to point to different images.**
> [source: k8s-docs-images-2026-08-23]

## ★ Fixed Point — verbatim, do not reword

> **A tag identifies a series and can be moved to point at a different image. A digest
> is a hash of the image's content and is immutable. Two pulls of `myapp:v2` a week
> apart are not guaranteed to be the same bytes. Two pulls of an image by digest are.**

Chapter 2: "If you recite one sentence from §1 through §3 cold, recite that one."

## The asymmetry to hold

A digest is **derived from** the image. Change one byte and you get a different digest,
necessarily. "You cannot move a digest to point at different content, in the same way
that you cannot move the number 4 to mean 5."

A tag is **attached to** the image. It is a label, and labels come off.

**Mutability here is not a permissions question.** A digest cannot be re-pointed by
anyone, *including the registry operator*, because it is derived from the content
(Practice Q11 distractor D exists to catch exactly this).

## Second authority now on disk

> Digest: "a unique identifier created from a cryptographic hash of a Blob's content."
> [source: oci-distribution-spec-2026-08-24]

The standards body stating the identity half independently of Kubernetes. Chapter 2's
§3 AUTHOR-REVIEW rates this "recommended, not blocking" — it is available now.

## The failure mode, preserved

§3's Logbook Entry is the chapter's best narrative and its mechanism is entirely
sourced: a deployment misbehaves, the manifest is verified unchanged twice, and the
rollback produces "the *same reference*, which produces the *same bytes*, which produces
the same bad behavior."

The tell, in the chapter's own words: "we spent an hour proving the manifest hadn't
changed instead of one minute asking whether an unchanged manifest guarantees unchanged
bytes."

Nobody moved the tag maliciously — "somebody upstream rebuilt `:v2` with a dependency
bump, which is a completely reasonable thing to do to a tag, because a tag identifies a
series."

⚑ Nominated as a voice exemplar under a **new** function tag (Logbook Entry). One author
question first: it is written in first-person plural and reads as lived experience. If
house style requires composite anecdotes to be signalled, settle that before locking.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 2 §6** | Practice Q26's strongest distractor (D) turns on this: a Pod is pinned to the **reference**, not to a resolved digest |
| **Ch 3** | Bearings #1 Q4 distractor D ("cached container image layers") assumes it |
| **Ch 12** | Signing and attestation are meaningless without content-addressed identity |
| **Ch 15** | Any claim about reproducible deployment rests here |

## Related

[[image-reference]] · [[registry]] · [[imagepullpolicy]] · [[image-layer]] ·
[[image-immutability]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/image-reference.md ===
# Concept: The image reference and its three defaults

**Home:** Chapter 2 §3 · **Competency:** D1.4 · **Status:** canonical

## Shape

`[registry[:port]/]name[:tag | @digest]`

## The defaults (verbatim)

> **If you don't specify a registry hostname, Kubernetes assumes that you mean the
> Docker public registry.** […] **If you don't specify a tag, Kubernetes assumes you
> mean the tag `latest`.** So `busybox` is equivalent to
> `docker.io/library/busybox:latest`. [source: k8s-docs-images-2026-08-23]

| What you write | Resolves to | Default(s) applied |
|---|---|---|
| `busybox` | `docker.io/library/busybox:latest` | registry **and** tag |
| `busybox:<version>` | `docker.io/library/busybox:<version>` | registry |
| `registry.k8s.io/pause` | `registry.k8s.io/pause:latest` | tag |
| `registry.k8s.io/pause:3.5` | exactly that | none |
| `registry.k8s.io/pause@sha256:1ff6…` | exactly those bytes | none |

The `busybox` equivalence and both `registry.k8s.io/pause` forms are the documentation's
own examples; `<version>` is a placeholder, not a published tag.

## Three defaults, not two

Chapter 2's 🪝: "`busybox` is three defaults stacked in a trench coat: a registry you
didn't name, a **namespace** you didn't name, and a tag you didn't name."

The `library` namespace is the third and the one most often dropped — Practice Q10
distractor C is `docker.io/busybox:latest`, correct except for it.

⚑ **Terminology:** this is the *registry-path* sense of `namespace`, not the Kubernetes
sense (Ch 4 §3) or the Linux sense (Ch 2 §1). See the glossary's Tier 2 convention lock.

## Two facts, one field

The default is **not** cluster-configurable. Bearings #1 Q4 distractor A ("whichever
registry the node is configured to prefer") exists to catch that; the assumption is
specific.

`registry.k8s.io` hosts Kubernetes project images and appears throughout the docs'
examples, but **it is not the assumed default.**

## The hidden second effect

The reference form you choose for *identity* reasons silently chooses your *pull
behavior* — see [[imagepullpolicy]]. §3's ⚠ names only the first effect; §6 completes it.

## Related

[[tag-vs-digest]] · [[registry]] · [[imagepullpolicy]] · [[container-image]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/registry.md ===
# Concept: The registry

**Home:** Chapter 2 §3 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "registry"

## Definition (chapter's paraphrase — flagged as such)

> A registry is where images live between being built and being run. You push there and
> nodes pull from there. [source: k8s-docs-images-2026-08-23]

Chapter 2 marks this as paraphrase, and it is: a distribution layer speaking a
standardized API.

## Spec-level definitions now on disk

`oci-distribution-spec-2026-08-24` supplies all three verbatim, upgrading this shard
from paraphrase to citation:

- **Registry** — "a service that handles the required APIs defined in this
  specification"
- **Push** — "the act of uploading blobs and manifests to a registry"
- **Pull** — "the act of downloading blobs and manifests from a registry"
- **Repository** — "a scope for API calls on a registry for a collection of content
  (including manifests, blobs, and tags)"
- **Blob** — "the binary form of content that is stored by a registry, addressable by a
  digest"

## ★★ FIVE credential paths — the count is BINDING

Private registries may require credentials. The documented paths
[source: k8s-docs-images-2026-08-23]:

1. Configuring **nodes** to authenticate to the private registry
2. A **kubelet credential provider** that fetches credentials dynamically
3. **Pre-pulled images**
4. **`imagePullSecrets`** on a Pod, referencing a Secret of type
   `kubernetes.io/dockerconfigjson`
5. Vendor-specific and local extensions

> ⚑ **DO NOT DROP ONE.** Chapter 4's Bearings Q4 reads "one of the **five** mechanisms
> Chapter 2 listed" and asks the reader to name two of the other four. Chapter 4 is
> shipped. Editing §3's list breaks a published question in a published chapter.

Two traps the answer keys build on:

- **The API server is not on the image-pull path at all.** Configuring *nodes* to
  authenticate is the documented path, because the kubelet is what pulls (Practice Q13
  distractor C).
- **Pre-pulling is per-node.** An image cached on one node does nothing for a Pod
  scheduled onto another (Practice Q13 distractor D).

## Adjacent-terminology note (not a conflict)

Chapter 4's `namespace.md` uses a *registry* analogy — "Two ships on two different
registries can carry the same name." Fine in isolation; recorded because a reader
arriving at Ch 4 straight from Ch 2 has a freshly loaded meaning for that word. **No
change proposed to Chapter 4's shard.**

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 4 §4** | Secrets and the `dockerconfigjson` type — pinned by name and line, honored |
| **Ch 12 §3** | "Restricting who can pull what" — ⚑ this topic does **not** appear in Ch 12's lineup at all. May be a content gap, not just a numbering one |
| **Ch 13** | Registry auth failure is a leading `ImagePullBackOff` cause |

## Related

[[image-reference]] · [[tag-vs-digest]] · [[oci]] · [[imagepullbackoff]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/container-runtime.md ===
# Concept: The container runtime

**Home:** Chapter 2 §4 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap rows "containerd", "CRI-O", "runC"

## Definition (verbatim)

> The container runtime is a fundamental component that empowers Kubernetes to run
> containers effectively. It is **responsible for managing the execution and lifecycle
> of containers** within the Kubernetes environment. Kubernetes supports container
> runtimes such as **containerd**, **CRI-O**, and **any other implementation of the
> Kubernetes CRI**. [source: k8s-docs-containers-2026-08-23]
> [source: k8s-docs-cluster-architecture-2026-08-23]

## The third list item is the design

Chapter 2: "Read the third item in that list carefully, because it is not padding. It is
a promise about the shape of the system: the list of supported runtimes is *open*. Two
are named because two are widely deployed; the qualifying condition is **conformance to
an interface**, not membership in a list."

Practice Q27 distractor C exists for this: CNCF graduation is a project-maturity status,
**not** a certification that makes a runtime usable by Kubernetes.

## A NODE component

Runs on every machine that runs workloads, alongside the kubelet and (optionally)
kube-proxy [source: k8s-docs-components-2026-08-23]. "A container runtime, containerd or
CRI-O, must be installed on **every node**"
[source: k8s-docs-setup-tooling-2026-08-23]. Not centrally, not on the control plane's
behalf — on each node, because that is where containers run.

Agrees verbatim in substance with Chapter 3's `node-components.md`. **No conflict.**

## Runtime vs kubelet — the distinction the exam probes

- The **kubelet** is the component that *wants* containers to exist. It "takes a set of
  PodSpecs […] and ensures that the containers described in those PodSpecs are running
  and healthy" [source: k8s-docs-cluster-architecture-2026-08-23].
- The **runtime** is the component that *makes* them exist.
- Between them is the CRI.

Bearings #2 Q1 distractor B is the most tempting in the chapter for exactly this reason.
"It drives; it does not execute."

## The three named implementations

| Name | Plane | Status |
|---|---|---|
| **containerd** | CRI implementation | CNCF **graduated** [source: cncf-project-maturity-levels-2026-08-23] |
| **CRI-O** | CRI implementation | CNCF **graduated** |
| **runC** | OCI runtime, below the CRI runtime | Donated by Docker to the OCI "to serve as the cornerstone" [source: oci-overview-2026-08-23] |

**These three are not a list of alternatives.** Chapter 2's Why-This-Chapter-Matters
makes the point explicitly: telling them apart is the discrimination the whole chapter
installs.

## Primary sources now on disk

- containerd: "an industry-standard container runtime with an emphasis on simplicity,
  robustness, and portability"; "a member of CNCF with 'graduated' status"; and the
  previously-unsourced hop — **"Most interactions with the Linux and Windows container
  feature sets are handled via runc"** [source: containerd-cri-o-runc-2026-08-24].
- CRI-O: "an implementation of the Kubernetes CRI […] to enable using OCI […] compatible
  runtimes"; "supports runc and Kata Containers as the container runtimes but any
  OCI-conformant runtime can be plugged in principle" — a sourced §4 → §7 bridge.
- runC: "a CLI tool for spawning and running containers on Linux according to the OCI
  specification." *Only this fragment returned as a quotation; attribute no more without
  re-fetching.*

## Related

[[cri]] · [[oci]] · [[pluggable-interface-pattern]] · [[runtimeclass]] · [[container]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cri.md ===
# Concept: CRI — the Container Runtime Interface

**Home:** Chapter 2 §4 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "CRI" (its Bearings #1 Q5 retrieval item)

## Definition (verbatim, as the chapter has it)

Kubernetes' infrastructure extension points include the "container runtime (**CRI**, the
Container Runtime Interface, **to support alternative container runtimes**)."
[source: k8s-docs-extending-kubernetes-2026-08-23]

Chapter 2: "That single parenthetical is the whole design in one line. CRI exists *in
order to* support alternatives. It is a socket, and the socket is the product."

## ★★ Fixed Point — verbatim, DO NOT REWORD

> **kubelet → CRI → containerd or CRI-O → runC → a running process.**
>
> **Kubernetes defines the CRI. It does not implement it. Kubernetes never starts a
> container itself.**

⚑ **Chapter 2's most-reused item.** Ch 3, Ch 8, Ch 13, and Ch 17's secondary Zenith all
retrieve this chain **as written**. An earlier revision proposal to soften it to a
generic "CRI runtime → OCI runtime" was correctly rejected and must stay rejected.

## The thesis sentence is now on disk

Chapter 2's AUTHOR-REVIEW asks for it by name; `k8s-docs-cri-2026-08-24` supplies it:

> The CRI is a **plugin interface** which enables the kubelet to use a wide variety of
> container runtimes, **without having a need to recompile the cluster components.**

Plus: "The kubelet acts as a **client** when connecting to the container runtime via
gRPC," and "You need a working container runtime on each Node in your cluster, so that
the kubelet can launch Pods and their containers."

## ⚠ SCOPE GUARD — take only those sentences

The same snapshot carries material that is **above associate tier and must not reach
this chapter.** The snapshot states this warning itself:

- `--container-runtime-endpoint`
- the v1 CRI API requirement / version skew
- gRPC message size limits
- the `CRIListStreaming` feature gate

## The middle hop, previously unsourced

Nothing on disk at draft time stated that the CRI runtime *invokes* the OCI runtime.
`containerd-cri-o-runc-2026-08-24` closes it: "Most interactions with the Linux and
Windows container feature sets are handled via runc." **The Fixed Point's chain is now
sourced end to end.**

## The Docker confusion

§4's 🪝: "'Docker' is four things wearing one name: a company, a command-line tool, a
build format, and, historically, a runtime." ⚑ **Authored framing, not a documented
taxonomy — deliberately left untagged.** Do not dress it as sourced.

The misconception itself *is* documented: "Early versions of Kubernetes only worked with
a specific container runtime: Docker Engine"
[source: k8s-blog-dockershim-faq-2026-08-24]. **Two cautions:** that FAQ is dated
2022-02-17 and must not be presented as current, and the dockershim narrative belongs to
Chapter 3.

⚑ **UNMET PROMISE.** §4's Snag defers "the era that produced the shorthand" to Ch 3 §1.
**Chapter 3 is drafted and does not deliver it** — three Docker mentions, none
explaining why the shorthand was ever accurate. Fix in Ch 3 §1 using A3, or soften Ch 2's
Snag. See `retrieval-log.md`.

## Related

[[container-runtime]] · [[oci]] · [[pluggable-interface-pattern]] · [[runtimeclass]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oci.md ===
# Concept: The OCI and its three specifications

**Home:** Chapter 2 §5 · **Competency:** D1.4 · **Status:** canonical
**Absorbs:** `filesystem-bundle` (too short for its own shard)

## Definition (verbatim)

> The Open Container Initiative is an **open governance structure** for the express
> purpose of creating open industry standards around container formats and runtimes. It
> was established in **June 2015** by Docker and other leaders in the container
> industry, and it operates under the **Linux Foundation**.
> [source: oci-overview-2026-08-23]

**Governance structure. Not software. It publishes documents.**

## ★ Fixed Point — verbatim

> **The OCI is a governance body that publishes three specifications: the image
> specification, the distribution specification, and the runtime specification. It is
> not a runtime, not a company, and not a product you install.**

Practice Q19 distractor D carries the **correct founding date** with the wrong kind of
body. That is deliberate: "Getting the date right will not save you if you have the kind
of body wrong, which is exactly why the Fixed Point in §5 leads with 'governance body,'
not with '2015.'"

## Each specification retroactively explains an earlier section

| Spec | Governs | Explains |
|---|---|---|
| **`image-spec`** | "the image manifest, filesystem layer serialization, and image configuration needed to launch applications on target platforms" | §2's layers — a published format, not a widely-followed convention |
| **`distribution-spec`** | "the API to distribute container images" — **v1.0, May 2020** | §3's registries — why any registry serves any image |
| **`runtime-spec`** | "how to run a 'filesystem bundle' that is unpacked on disk" | §4's bottom hop — runC's job description is a document |

[source: oci-overview-2026-08-23]

> 🪢 **Build it, ship it, run it** — `image-spec`, `distribution-spec`, `runtime-spec`.

## Filesystem bundle

Chapter 2's gloss (**marked as a gloss, not a quotation**): "the unpacked, on-disk form
of an image: the container's filesystem contents plus the configuration a runtime needs
in order to start it."

The specification's own definition is now on disk: "a set of files organized in a certain
way, and containing all the necessary data and metadata for any compliant runtime to
perform all standard operations against it," with `config.json` **REQUIRED** at the
bundle root [source: oci-runtime-spec-bundle-2026-08-24]. Replacing the gloss with this
is a chapter edit.

The flow, in three beats: download an OCI Image → unpack into a filesystem bundle → the
bundle is run by an OCI Runtime [source: oci-overview-2026-08-23].

## ⚠ OCI vs CRI — the hardest discrimination in the chapter

| | CRI | OCI |
|---|---|---|
| **What** | How *Kubernetes* talks to a runtime | How *images* are formatted/distributed, how *bundles* execute |
| **Endpoints** | kubelet ↔ runtime | build tools, registries, runtimes |
| **Whose concern** | Kubernetes | The industry — "would exist, unchanged, in a world where Kubernetes was never written" |

**The test:** "ask which *direction* you're looking. Up toward Kubernetes, that's CRI.
Sideways toward the rest of the industry, that's OCI."

A single component can genuinely participate in both planes. Chapter 2 generalized this
sentence because the specific claim was unsourced; **it is sourced now** — "CRI-O is an
implementation of the Kubernetes CRI (Container Runtime Interface) to enable using OCI
(Open Container Initiative) compatible runtimes"
[source: containerd-cri-o-runc-2026-08-24]. One sentence, both acronyms, correct planes,
from the project. Anchor both the §5 ⚠ and Practice Q20 on it.

## Chronology — what the chapter may and may not claim

On disk: OCI "Established in June 2015"; "currently contains three specifications";
`distribution-spec` v1.0 May 2020. **Not on disk:** v1.0 dates for `image-spec` and
`runtime-spec`. An earlier draft asserted "two of the three were part of the effort from
its 2015 founding" and did five-year arithmetic; both were correctly cut. To restore,
source from opencontainers.org.

## Related

[[cri]] · [[container-runtime]] · [[image-layer]] · [[registry]] ·
[[pluggable-interface-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/imagepullpolicy.md ===
# Concept: `imagePullPolicy` and its four conditional defaults

**Home:** Chapter 2 §6 · **Competency:** D1.4 · **Status:** canonical
**Chapter 2's own assessment:** "the fiddliest material in the chapter, and in the
author's judgment the highest value per minute of anything in it."

## The three policies (verbatim, Dead Reckoning)

> **IfNotPresent:** the image is pulled only if it is not already present locally.
> **Always:** every time the kubelet launches a container, it queries the container
> image registry to resolve the name to an image digest; if the kubelet has a container
> image with that exact digest cached locally, it uses its cached image, otherwise it
> pulls the image with the resolved digest.
> **Never:** the kubelet does not try fetching the image; if the image is somehow
> already present locally, the kubelet attempts to start the container, otherwise
> startup fails. [source: k8s-docs-images-2026-08-23]

## ★ The four defaults, applied when the field is omitted

| Reference form | Default |
|---|---|
| `@digest` | IfNotPresent |
| `:latest` | **Always** |
| no tag | **Always** |
| any other tag | IfNotPresent |

**There is no single global default** — Bearings #3 Q1 distractor C and Practice Q23 C
both offer one. **`Never` is never a default**; it is only ever set explicitly.

## Two things worth saying about it

**1. The right-hand branch is reached by NOT making a decision.** Figure 2-5's caption
carries the insight: "the reference form you chose for identity reasons quietly chose
your pull behavior too." This completes §3's `:latest` hazard — the documented caution
names only the naming problem; the tag *also* flips the default to `Always`, maximizing
the number of opportunities for the answer to change. **Two problems, one field.**

**2. `Always` does not mean "always download."** It means always **check**: re-resolve
the name to a digest at the registry, and use the cached copy on a digest match. Chapter
2 calls this "a favorite distractor" — Bearings #3 Q2 A and Practice Q22 D both work it.

Note for answer keys: **caching is keyed on digest, not on tag**, and there is no
tag-cache expiry mechanism (Practice Q26 C).

## Resolved at creation, not re-evaluated

> Once a Pod is created, `imagePullPolicy` is not updated if the image's tag or digest
> changes later. [source: k8s-docs-images-2026-08-23]

Chapter 2 frames this as "§2's immutability principle showing up in an unexpected
place." If you need new behavior, you need a new Pod. Practice Q26 composes this with
the IfNotPresent default to explain the "we pushed a fix and nothing happened" scenario
— its distractor D is the strongest in the chapter because the rebuild *does* produce a
new digest; the Pod is simply pinned to the **reference**, not to a resolved digest.

## Related

[[image-reference]] · [[tag-vs-digest]] · [[imagepullbackoff]] · [[image-immutability]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/imagepullbackoff.md ===
# Concept: `ImagePullBackOff`

**Home:** Chapter 2 §6 · **Competency:** D1.4 · **Status:** canonical
**Retrieval target:** Ch 5 Soundings Q8, Ch 5 Bearings #2 Q4, Ch 5 Practice Q22

## Definition (verbatim)

> A container could not start because Kubernetes could not pull the image, for reasons
> such as an invalid image name or pulling from a private registry without credentials.
> The **BackOff** part indicates that Kubernetes will keep trying, with an **increasing
> back-off delay**, up to a compiled-in limit of **300 seconds (5 minutes)**.
> [source: k8s-docs-images-2026-08-23]

Reported as a container in the **Waiting** state
[source: k8s-docs-images-2026-08-23].

## ★ Scope boundary — what Chapter 2 owes and what it doesn't

Chapter 2 owes exactly three things: **the name, the cause, and the retry behavior.**
It has all three and stops there, deliberately.

| Deferred | To |
|---|---|
| Container states and Pod phases | Ch 5 §5 |
| Diagnosis — reading events, checking the name, confirming the push | Ch 13 §2 |

## ⚑ Binding cross-chapter dependency

**Ch 5 Soundings Q8's answer attributes "reported as a container in the Waiting state"
to Chapter 2 by name.** That clause must stay in §6. Chapter 5's `container-state.md`
and this shard agree exactly — Ch 2 owns the reason, Ch 5 owns the state. This handoff
worked and should not be disturbed.

## Answer-key discriminations

- **Not** an integrity-check failure, and **not** given up on — retrying is what BackOff
  describes (Bearings #3 Q3 A).
- **Not** a crash after a successful pull (Q3 C) — the image never arrived.
- **Not** disk pressure, which is a distinct node condition (Q3 D).

## Related

[[imagepullpolicy]] · [[registry]] · [[image-reference]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/runtimeclass.md ===
# Concept: RuntimeClass — isolation strength as a per-workload decision

**Home:** Chapter 2 §7 · **Competency:** D1.4 · **Status:** canonical
**Closes:** Chapter 3's Tier 4 gap row "RuntimeClass"

## Definition (verbatim)

> **RuntimeClass is a feature for selecting the container runtime configuration** used
> to run a Pod's containers. [source: k8s-docs-runtime-class-2026-08-23]

## Motivation before mechanism

> You can set a different RuntimeClass between different Pods to provide a **balance of
> performance versus security**. For example, if part of your workload deserves a high
> level of information-security assurance, you might choose to schedule those Pods so
> that they run in a container runtime that uses **hardware virtualization** (such as
> Kata Containers) or a **user-space kernel** (such as gVisor). You'd then benefit from
> the extra isolation of the alternative runtime, **at the expense of some additional
> overhead.** [source: k8s-docs-runtime-class-2026-08-23]

Chapter 2 insists on this ordering: "the mechanism without the motivation is
unmemorable trivia."

## ⚓ The sentence that makes the section stick

> **"Container" names an interface, not an isolation level.**

Everything from §1–§6 — the image format, the pull behavior, the CRI socket — is
unchanged whether the thing on the other end shares the host kernel directly, interposes
a user-space kernel, or boots a lightweight VM. **The contract is stable; the strength
of the walls is a parameter.**

This is the renegotiation of the trade named in §1's ⚓. The two callouts are one
argument split across six sections.

## Two levels of indirection

1. The **Pod** names a RuntimeClass via `runtimeClassName`.
2. The **RuntimeClass** (`node.k8s.io/v1`, `handler` field) names a **handler** that an
   administrator configured on the nodes.

"The Pod author does not name a runtime. They name a *class of runtime configuration*
that a cluster administrator has already established" — which is why this is
self-service rather than arbitrary-runtime-request.

**If no `runtimeClassName` is specified, the default runtime handler is used**
[source: k8s-docs-runtime-class-2026-08-23]. Practice Q25 distractor C inverts the
tradeoff: defaulting to the strongest runtime would make every workload pay for a
boundary most don't need. **Selectivity is the feature.**

## Also carries (register, don't develop)

`nodeSelector` and `tolerations`, so Pods land on nodes supporting the handler, and
**Pod overhead**, so the scheduler accounts for the runtime's resource cost
[source: k8s-docs-runtime-class-2026-08-23]. All three are Chapter 7's. Ch 7 line 576
discharges the pointer by name — verified.

## Kata vs gVisor — depth deliberately capped

Kata uses **hardware virtualization** (roughly, borrowing back the boundary §1 traded
away); gVisor interposes a **user-space kernel**. Different techniques, same goal,
different overheads.

⚑ **The gVisor mechanism is the chapter's one genuinely open research item.** The Sentry
/ syscall-interception description is not in the cache and **not in the research
manifest's Appendix A** — it needs gvisor.dev/docs/. The chapter's own position is the
defensible one: "an exam item is far likelier to ask *why RuntimeClass exists* than to
ask which sandbox uses which technique."

Sourced bridge available: CRI-O "supports runc and Kata Containers as the container
runtimes" [source: containerd-cri-o-runc-2026-08-24] — showing Kata slots into the
**same socket** from §4, not a new mechanism.

## The misconception this shard exists to kill

**"Container isolation strength is fixed."** Practice Q24 A is the belief; Bearings #3
Q4 D is the subtler error — namespaces and NetworkPolicy segment *network* reachability,
while the requirement is a stronger boundary between workload and **host**. Right
control, wrong axis.

## Related

[[container]] · [[container-runtime]] · [[cri]] · [[pluggable-interface-pattern]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interface-pattern.md ===
# Concept: "Kubernetes defines an interface and lets the ecosystem implement it"

**Home:** Chapter 2 §4 (⚓, coining site) and §8 (Zenith) · **Competency:** D1.4
**Status:** canonical **with an open cross-chapter conflict — read CC-1 before using**
**Closes:** Chapter 3's Tier 4 gap row for the named pattern
**B3 status:** one of nine cross-cutting themes, scheduled for retrieval **BY NAME**

## Canonical wording (Chapter 2 §4 ⚓ — the coining site)

> **Kubernetes defines an interface and lets the ecosystem implement it.**

## Sourced enumeration

CRI (runtimes), **CNI** (pod networking), **CSI** (storage types), **device plugins**,
**API extensions** [source: k8s-docs-extending-kubernetes-2026-08-23].

## The Zenith reading (§8)

> The OCI standardized the image format […] the distribution API […] bundle execution.
> And Kubernetes, for its part, standardized nothing about containers at all. It
> published an *interface*, the CRI, and let the ecosystem supply the implementations.

"Which is why Kubernetes never needed to know what is in the crate. […] It knows the
shape of the fitting."

## ⚑⚑ CC-1 — CANON CONFLICT. Do not merge. Neither reading adopted.

**Chapter 2 §4** (`ch02:598`), of the runtime:
> Kubernetes defines an interface and lets the **ecosystem implement** it.

**Chapter 3 §3** (`ch03:~325`), of etcd **and** the runtime:
> Where a good general-purpose component already exists, Kubernetes defines an interface
> and **uses it** rather than reimplementing it.

**Why this is not a paraphrase difference.** etcd is not in Chapter 2's sourced
enumeration, and Kubernetes does not define an etcd interface — it consumes a
general-purpose datastore. The claim is true of the *runtime* and true-but-different of
*etcd*, and calling them "the same" broadens a sourced list past what it says.

**Compounding it.** Chapter 2 §4 is a section titled "The pattern to name now" whose ⚓
tells the reader *"Give this move a name in your head, because you are about to see it
three more times."* Chapter 3 hits the first recurrence, re-derives it in fresh words,
**and never uses the name or bears back to Ch 2 §4.** That is a missed spaced-retrieval
event on a theme B3 tracks by name and Ch 17's secondary Zenith depends on.

**Chapter 2's wording is canonical** — coining site, sourced, scheduled for retrieval by
name. Chapters 9, 11, and 17 must use this exact phrase.

**Recommended chapter fix** (Chapter 3's own, endorsed): separate the two instincts.
Keep the named pattern for the container runtime, cross-beared to Ch 2 §4; describe etcd
as the adjacent-but-distinct instinct of reusing an existing general-purpose component.

## ⚑ Internal count discrepancy in Chapter 2

§4's ⚓ says **"Four sockets"** immediately after naming **five** things (CRI, CSI, CNI,
device plugins, API extensions). Book canon is four everywhere else:

- Exam Alert item 5 — "CRI, CNI, CSI, and API extensions"
- §8 — "Storage does it. Networking does it. The API itself does it."
- Chapter Summary, last row — "CRI is the first of four"
- Ch 2 pins `Ch 17 §4 — the four pluggable interfaces, collected` (twice)

**Author decision:** drop device plugins from the ⚓, or change "Four sockets" to "One
design instinct, applied in several places." ⚑ Ch 17's lineup collects **seven**
extension points — if four is a deliberate simplification, Ch 17 should say so.

## ⚑ Ch 17 §4 is DOUBLE-PINNED

| Claimant | Line | Topic |
|---|---|---|
| Chapter 1 | 182 | "the cloud native certification landscape" |
| **Chapter 2** | **600 and 914** | **"the four pluggable interfaces, collected"** |

Ch 17 cannot be both, and both chapters are shipped. Chapter 2's claim is load-bearing —
it is the Zenith's payoff pointer, pinned twice, and §8 stakes the book's closing
argument on it ("the collecting is meant to feel like recognition"). Ch 1's is a single
navigational aside. Ch 17's lineup places extension-points synthesis **fifth** and the
certification ladder **last**, favoring Chapter 2.

**Recommendation: Ch 2 keeps §4; retarget Ch 1 line 182. Resolve before Ch 17 outlines.**
This is the `Ch 6 §3` failure with the fuse still burning.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 9 §1** | CNI — second recurrence. **Use the name.** |
| **Ch 11** | CSI — third recurrence. **Use the name.** ⚑ Ch 2 pins §2; Ch 11's lineup orders CSI *ninth* |
| **Ch 6 §8** | API extensions — fourth. ⚑ Ch 2 line 600 says §3; **CRDs are §8** |
| **Ch 17 §4** | The collection. Must "feel like recognition rather than a fourth list" |

## Related

[[cri]] · [[oci]] · [[container-runtime]] · [[runtimeclass]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/buildpacks.md ===
# Concept: Cloud Native Buildpacks

**Home:** Chapter 2 §2 · **Competency:** D1.4 · **Status:** canonical
**Scope:** ecosystem awareness — the exam asks *that the alternative exists*, not how to
operate it.

## The five terms (verbatim)

[source: buildpacks-concepts-2026-08-23]

| Term | Definition |
|---|---|
| **buildpack** | "software that transforms application source code into runnable artifacts by analyzing the code and determining the best way to build it" |
| **builder** | "an OCI image containing an ordered combination of buildpacks and a build-time base image, a lifecycle binary, and a reference to a runtime base image" |
| **stack** | the pairing of the **build image** (where buildpacks run) and the **run image** (base for the final application image) |
| **platform** | "either the `pack` CLI or a CI system," which orchestrates by invoking the lifecycle binary with the buildpacks and the source |
| **lifecycle** | three phases — **detect** (which buildpacks apply) → **build** (compile and assemble) → **export** (final OCI image with reproducible layers) |

Cloud Native Buildpacks is a CNCF **graduated** project.

## ⚓ The idea worth keeping even if you never use them

**The environment that *compiles* your application and the environment that *runs* it do
not have to be the same environment, and they usually shouldn't be.** Compilers, headers,
and build tooling are attack surface that a production image has no use for. Buildpacks
make that separation structural rather than a discipline you have to remember.

Now sourceable (the chapter flags this sentence as unsourced; both files are on disk):

- "None of the build tools required to build the application are included in the
  resulting image" [source: docker-docs-multi-stage-2026-08-24]
- "A small image with minimal dependencies can considerably lower the attack surface"
  [source: docker-docs-build-best-practices-2026-08-24]

The second snapshot also supplies **"you can pin the image version to a specific
digest,"** which the chapter identifies as the hinge sentence for Practice Q26.

## 🔭 Reproducible layers

The export phase produces *reproducible* layers — "the same input reliably produces the
same layer bytes rather than layers that differ run to run because of timestamps or file
ordering." ⚑ **That gloss on "reproducible" is the author's, not the specification's**,
and the chapter says so. Preserve the attribution.

Why it matters beyond exam scope: "you cannot meaningfully attest to an artifact whose
bytes change when nothing changed." → Ch 12 §2.

## What Buildpacks do NOT claim

Answer-key discriminations from Practice Q7:
- **Not** a build-speed claim; nothing promises parallel layer creation.
- **Not** a runtime change — the output is an ordinary OCI image, which is the point.
- **Not** a vulnerability guarantee. Scanning is a separate supply-chain concern
  [source: k8s-docs-cloud-native-security-2026-08-23]; no build system can guarantee a
  clean image.

## Related

[[container-image]] · [[image-layer]] · [[oci]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 2 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.4** | **Chapter 2** *(Containerization)* | **deep** | **2026-08-24** |

**Registry row change:** `D1.4 | Containerization | Ch 2` → **"complete — Ch 2 covered
2026-08-24."**

**D1.4 opens and closes in one chapter.** Like D1.3, there is no later chapter to absorb
a gap. Unlike D1.3, **no coverage shortfall is recorded** — see the scope decisions
below, all three of which are deliberate and defensible at associate tier.

**Sequencing note:** Chapter 2 drafted second but reached Stage 14 seventh. Its coverage
was therefore missing from the registry while Chapters 3–7 were logged. Nothing needs
re-auditing; the row simply lands late.

### Chapter 2 — D1.4 coverage detail

`kb_tags.objectives: ["D1.4"]`; all eight sections carry `objectives: ["D1.4"]`.

| Sub-topic | Depth |
|---|---|
| Container vs VM; what is shared | **deep — derived rather than tabulated, which is the chapter's method claim** |
| Kernel/OS dual register | **deep — both registers carried, exam-authority wording named** |
| Relaxed isolation as a tradeoff | deep — and load-bearing for §7 |
| Container image contents | deep |
| "No kernel" | **deep — correctly marked DERIVED, not quoted** |
| Immutability; build-then-recreate | **deep — Ch 3 Q24 and Ch 5 Q20 both retrieve it** |
| Image layers: stacking, sharing, rebuild cost | moderate–deep — ⚑ sourcing now closable, see below |
| Buildpacks | moderate — correctly scoped to ecosystem awareness |
| Image reference and its three defaults | deep |
| Tag vs digest | **deep — the chapter's sharpest single fact, ★ Fixed Point** |
| `:latest`, both effects | **deep — the second effect (§6) is the chapter's best integrative move** |
| Registry; five credential paths | moderate — **the count is binding on Ch 4** |
| Container runtime as a node component | deep |
| CRI as interface, not implementation | **deep — ★ Fixed Point, the chapter's most-reused item** |
| containerd / CRI-O / runC and their planes | deep |
| OCI as governance body; three specs | **deep — ★ Fixed Point** |
| Filesystem bundle | moderate — gloss, upgradeable to spec definition |
| OCI vs CRI discrimination | **deep — ⚠ callout plus Practice Q9/Q16/Q20** |
| `imagePullPolicy`: 3 values, 4 defaults | **deep — chapter's own "highest value per minute"** |
| `ImagePullBackOff` | moderate — **correctly capped**; states and diagnosis deferred to Ch 5 / Ch 13 |
| RuntimeClass; per-workload isolation | deep |
| Kata vs gVisor mechanisms | recognition — **deliberate; see scope decision 2** |
| The pluggable-interface pattern | **deep — named, sourced, and Zenith-carried** |

### Three scope decisions, all deliberate

1. **Supply-chain security named and deferred to Ch 12.** Correct — Ch 12 owns D2.2.
2. **gVisor's Sentry/syscall mechanism left at recognition depth.** The only genuinely
   open research item in the chapter (not in cache, not in the research manifest's
   Appendix A; needs gvisor.dev). The chapter's own justification holds: an item is
   likelier to ask *why RuntimeClass exists* than which sandbox uses which technique.
3. **CRI operational detail excluded** — `--container-runtime-endpoint`, v1 CRI API
   version skew, gRPC limits, `CRIListStreaming`. All above associate tier. The
   `k8s-docs-cri-2026-08-24` snapshot carries its own matching scope warning; the
   chapter's guard and the snapshot's agree exactly.

### ⚑ Question-budget correction — frontmatter under-counts by two

| | Frontmatter declares | Body actually has |
|---|---|---|
| Soundings | 8 | 8 ✅ |
| Taking Your Bearings | 12 | 12 ✅ |
| Practice questions | **25** | **27** |
| **Chapter total** | **45** | **47** |

Verified: Q27 is present, and the body's "seven require combining two sections" claim
matches exactly seven `[integrative:]` tags (Q9, 14, 20, 22, 24, 26, 27). The Bearings
count was updated 10 → 12 during revision but the practice count was not, even though an
AUTHOR-REVIEW documents adding "the new integrative Practice Q26."

**Stage 14 and the book-level 300-question floor both read frontmatter, so the book is
currently under-counted by two.** This log records **actual**. Frontmatter fix is a
chapter edit.

### ⚑ Registry correction — Chapter 7's ledger lists Chapter 2 under the wrong objective

Chapter 7's book-level allocation table records **Ch 2 — Containerization | ~9% | D1.1**.

**D1.4 is correct.** Chapter 2's outline frontmatter tags every section `["D1.4"]`, and
Chapter 1's competency registry assigns D1.4 Containerization → Ch 2. A transcription
slip, not a coverage question. Flagged rather than silently rewritten, since it lives in
Chapter 7's appended block. The domain-allocation arithmetic is unaffected — the ~9% is
counted once either way.

### ⚑ Sourcing status — nine gaps are closable by tagging, not research

`sources/` holds **137** files, including **11 dated 2026-08-24** that landed at
04:48–04:49 — after Chapter 2's Stage 2 (01:07) but before its Stage 12 revision (11:09)
and Stage 13 integration (15:10). They were almost certainly harvested by Chapter 3's
research pass.

**Chapter 2's AUTHOR-REVIEWs, and integration finding #12, state these files do not
exist. That is stale.** Nine of eleven AUTHOR-REVIEWs are now discharged by tagging
against files on disk: A1, A3, A4/A5/A6, A7, A8, A9, A11, A12, A13, A14, A17. No
re-fetch, no manifest extraction, no browser session.

**Two remain genuinely open:** ISO 668 / ISO 1161 (§8 and the epigraph — iso.org 403s to
WebFetch) and the gVisor mechanism (scope decision 2 above, defensibly left as is).

⚑ **The §1 AUTHOR-REVIEW carries one stale instruction to delete.** It directs deleting
"Chapter 1's parallel AUTHOR-REVIEW at its line ~140." No such comment exists — Ch 1's
remaining comments are at 248, 280, 442, 584, none about the kernel/OS registers, and
Chapter 3 line 273 records the question as resolved book-wide. Delete that sentence;
keep the A13/A14 harvest request, which is now trivially satisfiable.

### Ethical-guardrails carry-forward (skill Part 14)

Chapter 2 passes with **one qualification worth tracking at book level.** The Exam Alert
closes with an unusually strong disclaimer — "they are conceptually slippery, not because
this book has data on how often they show up. The book does not make frequency claims it
cannot support" — and the trap table honors it.

But four body-prose predictions are stated as fact rather than judgment:
§1 *"the phrasing the exam is likeliest to use"* · §5 🔭 *"What the exam is more likely to
ask…"* · §6 *"This is a favorite distractor"* · §7 🔭 *"an exam item is far likelier to
ask…"*

None is fabricated and none is harmful, but they sit alongside a paragraph promising the
book doesn't make them. **Four words each** ("in the author's judgment") makes the
disclaimer true chapter-wide — and the chapter already models the fix twice, in the
Attention Budget and in §6's opening. Recorded here because Chapters 8–20 will face the
identical temptation and this is the cheapest place to set the precedent.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 2 update (2026-08-24)

### Outbound: 0 retrieval items — correct

B3 excludes Chapter 1 entirely (orientation, 0% weight) and begins the ramp at **Ch 3
(10%, drawing from Ch 2)**. Chapter 2 is the **first content chapter** and has nothing
earlier to retrieve. The question-quality audit confirms 0/0. No finding.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| *(none — Chapter 2 is the first content chapter)* | — | — |

### Inbound: 12 `[retrieval: ch2]` items — ALL VERIFIED SUPPORTED

This mattered. Stage 12 revised Chapter 2 *after* these items were written in Chapters
3–7, and a cut passage would have orphaned a shipped question. **Nothing was cut.**

| Source | Item | Anchor in Ch 2 | ✓ |
|---|---|---|---|
| Ch 3 Soundings Q4 + answer | kubelet ensures containers run | §4 | ✅ |
| Ch 3 Bearings #1 Q5 | kubelet reaches the runtime through CRI | §4 ★ Fixed Point | ✅ |
| Ch 3 Practice Q2 | what containers share that VMs don't | §1 | ✅ |
| Ch 3 Practice Q24 | correct process for changing a running container | §2 immutability | ✅ |
| Ch 3 Practice Q25 | what a container image contains | §2 | ✅ |
| Ch 4 Bearings Q4 | "one of the **five** mechanisms Ch 2 listed" — name two of the other four | §3, exactly five | ✅ |
| Ch 5 Soundings Q8 + answer | `ImagePullBackOff`, **reported as a container in the Waiting state** | §6, that exact phrasing | ✅ |
| Ch 5 Bearings #2 Q4 | phase / state / reason for a Pod that can't pull | §6 (name + state); Ch 5 (phase) | ✅ |
| Ch 5 Practice Q20 | "Chapter 2 established that containers are immutable" | §2 | ✅ |
| Ch 5 Practice Q22 | init container that can't pull its image | §6 | ✅ |
| Ch 5 line 307 | "containers are not the unit Kubernetes schedules; something wraps them" | §1 (verbatim in substance) | ✅ |
| Ch 7 line 576 | RuntimeClass carries `nodeSelector` and tolerations | §7 | ✅ |

**One loose item, not Chapter 2's defect.** Ch 4 Practice Q13 is tagged
`[retrieval: ch2]` but tests ConfigMap immutability in v1.19 — Ch 4's own material. The
Ch 2 link is analogical (its answer key rebuts distractor A by invoking Ch 2's
build-a-new-image rule). Defensible as interleaving; not accurate as retrieval. Belongs
to Chapter 4's ledger.

### ⚑ THREE BINDING DEPENDENCIES — editing Chapter 2 breaks shipped chapters

| # | Chapter 2 must keep | Because |
|---|---|---|
| 1 | **§3's list of exactly FIVE private-registry credential paths** | Ch 4 Bearings Q4 says "one of the **five** mechanisms Chapter 2 listed" and asks the reader to name two of the other four. Dropping one breaks a published question in a published chapter |
| 2 | **§6's "reported as a container in the Waiting state"** | Ch 5 Soundings Q8's answer attributes that phrasing to Chapter 2 **by name** |
| 3 | **§1's "containers are not the unit Kubernetes schedules; something wraps them"** | Ch 5 line 307 back-references it in substance as the Pod chapter's opening move |

These are contracts, not preferences. Record them in Chapter 2's chapter-state so a
future sweep doesn't trim them as redundant.

### ⚑ Forward commitments — binding

| # | Commitment | Where stated | Status |
|---|---|---|---|
| 2 | **Ch 17 §4 collects the four pluggable interfaces** | Ch 2 §4 (line 600) and §8 Zenith (line 914); §8's closing argument depends on it landing as "recognition rather than a fourth list" | **OPEN — AND COLLIDING.** Ch 1 line 182 pins the same section for "the cloud native certification landscape." Ch 17's lineup places extension-points synthesis **fifth** and the certification ladder **last**, favoring Ch 2. **Recommend Ch 2 keeps §4; retarget Ch 1 line 182. Resolve before Ch 17 outlines** |
| 3 | **Ch 3 §1 explains why "Kubernetes runs Docker containers" was ever accurate** | Ch 2 §4's 🪝 Snag defers "the era that produced the shorthand" there | **UNMET.** Ch 3 is drafted and does not deliver it — three Docker mentions, none explaining the shorthand. `k8s-blog-dockershim-faq-2026-08-24` is now on disk and closes it in one or two sentences (**caution:** dated 2022-02-17; do not present as current). Alternative: soften Ch 2's Snag |
| 4 | **Ch 2 §4's ⚓ promises the pattern "three more times"** | §4, then §8's "This is the **first** of four times" | **AT RISK.** Ch 3 hits the first recurrence, re-derives it in fresh words, and never uses the name — a missed retrieval event on a B3-tracked theme. See `concepts/pluggable-interface-pattern.md` CC-1 |

Commitment #1 (Ch 13 must carry a Ch 8 retrieval item) is Chapter 1's and remains open.

### ⚑ Section-number pins — five are at risk, and the mechanism to fix them already exists

Chapter 2 publishes 15 forward cross-bearings. Seven verified correct against drafted
chapters; one is **broken**; five name sections in **undrafted** chapters whose lineup
ordering contradicts the number.

**Broken (fix now, one token):** `Ch 6 §3 — CRDs and extending the API` at line 600.
**CRDs are Ch 6 §8.** Chapter 6 caught this itself and left a standing request at its
line 973; the revision stage did not make the edit.

> ⚑ **Correction to Chapter 6's reasoning, which matters for how the fix is argued.**
> Ch 6 states "§3 is pinned by chapter-04 line 688 and cannot move." **That premise is
> false** — Chapter 4 contains no §-numbered cross-bearing to Chapter 6 at all (all four
> of its Ch 6 pointers are chapter-level; line 688 is a ConfigMap/Secret table). The
> actual second claimant is **Chapter 1 line 436**, which pins Ch 6 §3 for StatefulSets
> — and StatefulSets are Ch 6 §6. So Ch 6 §3 is mis-pinned by two shipped chapters for
> two different topics, and neither is the one Ch 6 blames. The Ch 2 edit is still the
> right fix; **Ch 1 line 436 needs the same treatment.**

**At risk — pin these numbers in Ch 11's and Ch 12's frontmatter NOW:**

| Cross-bearing | Lineup says |
|---|---|
| `Ch 11 §2 — CSI and storage drivers` | CSI is ordered **ninth** (volume types → PV → PVC → StorageClass → provisioning → binding → reclaim → access modes → CSI) |
| `Ch 12 §1 — securing the image supply chain` | Ch 12 opens with lifecycle phases and the 4Cs; supply chain is second-from-last |
| `Ch 12 §2 — signing, attestation, supply chain` | Same. §1 and §2 would both have to be supply-chain sections |
| `Ch 12 §3 — restricting who can pull what` | ⚑ **Registry-side pull authorization does not appear in Ch 12's lineup at all.** Possibly a content gap, not a numbering one |
| `Ch 12 §4 — runtime protection for compute` | Sandboxed runtimes are **last** in Ch 12's lineup |

These are recoverable — the chapters aren't written — **but only if the numbers are
pinned now**, the way Ch 3 and Ch 4 pinned Ch 1's and Ch 2's with
`WARNING SECTION NUMBERING IS LOAD-BEARING` frontmatter blocks. Ch 11 and Ch 12 have no
such blocks. **Ch 6 §3 is what happens when nobody adds one.**

### Verified-correct pins (no action)

`Ch 3 §1` · `Ch 3 §3` · `Ch 4 §4` · `Ch 5 §1` · `Ch 5 §5` · `Ch 7` (chapter-level) ·
`Ch 10` (chapter-level). Also consistent by contrast: `Ch 17 §2` is pinned identically
by Ch 1 line 144 and Ch 2 line 671; `Ch 13 §5` identically by Ch 2 line 602 and Ch 3
line 451; `Ch 9 §1` has no competing claim and is plausible against the lineup.

### ⚑ Chapter 1 ↔ Chapter 2 contradiction across a page turn

Chapter 1's "The Voyage Ahead" (lines 580–586) tells the reader:

> *"Chapter 2 opens with a shipping container. An actual one: corrugated steel,
> standardized corner fittings… it's why Chapter 2 starts there rather than with a
> definition. You'll get the definition too. But you'll get it after you can already see
> why it had to be that way."*

Chapter 2 opens with "Kubernetes cannot run a container," defines the container in §1,
and delivers the crate in **§8**. **The promised order is inverted**, and both chapters
are shipped, so a reader meets the contradiction across a page turn.

**Recommend revising Chapter 1's handoff** rather than restructuring Chapter 2 — far
cheaper, and arguably better: §8's Zenith earns considerably more as a synthesis than it
would as an opening.

### Unresolved convention, carried forward

The `[retrieval: chN]` tag's rendered form (reader-visible or draft-only) is **still
undecided**. Chapter 1 flagged Chapter 3 as the first chapter needing it settled;
Chapters 3–7 have shipped without a decision. Chapter 2 correctly carries none. Now five
chapters overdue.
=== END APPEND ===
```

---

## Summary of what this stage did and didn't do

**Wrote (as write intentions):** 63 glossary rows discharging Chapter 3's Tier 4 gap in full · 15 concept shards · objective-coverage row closing D1.4 · retrieval-log entry with 12 verified inbound items, 3 binding dependencies, and 3 forward commitments.

**Did not touch:** `voice-exemplars.md` (10 candidates nominated only) · `style-decisions.md` · `structural-contract.yaml` · the skill · `concepts/namespace.md` (Chapter 4's, and Chapter 2 conflicts with it — flagged under CC-2, not overwritten) · any chapter draft.

**Three things the author should see before anything else:**

1. **The snapshots exist.** Eleven files dated 2026-08-24 are on disk, and they close nine of Chapter 2's eleven AUTHOR-REVIEWs by *tagging* — no re-fetching. The chapter, the integration report, and Chapter 3's ledger all say otherwise; they were written before the files landed. This is the cheapest large improvement available on the chapter.

2. **Nothing has ever been written to `Book-KCNA/knowledge-base/`.** Seven manifests, zero applied. Replay order is in Finding 1 — Chapter 2 goes **last**, not second.

3. **`Ch 17 §4` is claimed by two shipped chapters**, and Chapter 2's claim is the one its Zenith depends on. Ch 6 §3 already shows what happens when this goes unresolved; this one is still fixable.