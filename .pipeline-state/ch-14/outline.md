I have both binding contracts, the arc-outline block, B1's D3.1 concept and trap tables, B4's budget, and every published cross-bearing into Ch 14 verified by line number against chapters 01–13. Two findings shape this outline: **no section number in Ch 14 is pinned by shipped text** (all three inbound pointers are chapter-level), and **the cached research is 33 lines total for the entire chapter** — the thinnest source base of any chapter in the book.

```
---
chapter: 14
chapter_type: "content"
title: "Packing for the Voyage"
subtitle: "A chart is not a release, and templates are not the point"
exam_domain: "Cloud Native Application Delivery (competency: Application Delivery)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- SUBTITLE NOTE. Ten words, from the arc outline and the chapter lineup,
#-- carried forward unmodified. It states TWO Fixed Points on the chapter's
#-- second line — that is the subtitle's job and is NOT a licence for the
#-- Soundings. See the FIXED-POINT SPOILER CHECK below. Its second clause is
#-- also the §7 Zenith claim, so subtitle and synthesis agree by construction
#-- (the Ch 12 / Ch 13 pattern).

#-- EXAM_DOMAIN NOTE. D3.1 Application Delivery, in the house form shipped by
#-- ch-04/-09/-10/-11/-12/-13. The published domain weight is 16%
#-- [source: cncf-kcna-curriculum-pdf-2026-08-23]; the metadata line states
#-- that figure with its tag, followed by the house disclaimer that the split
#-- across Ch 14-16 is an authored allocation (B1 gap G33, B2 disclosure #1).
#-- Do NOT present 5% as published.
#--
#-- ⚠ SECOND, SHARPER HONESTY CONSTRAINT — unique to this chapter.
#-- CNCF publishes the competency NAME "Application Delivery" and nothing
#-- else. Verified against lf-kcna-exam-page-2026-08-23 (line 43) and
#-- cncf-kcna-curriculum-pdf-2026-08-23 (line 15): neither snapshot contains
#-- the word "Helm" or "Kustomize" anywhere. This chapter's entire topic list
#-- is authored inference from the bundled LFS250 module name plus the CNCF
#-- project landscape. Consequence for drafting, and it is binding:
#--   * The chapter must SAY this once, plainly, in Why This Chapter Matters.
#--   * No Helm or Kustomize fact may be framed as "frequently tested,"
#--     "commonly appears," or any frequency claim. Skill Part 14, Ethical
#--     Guardrail #8 — distinguish "frequently tested" from "might be tested."
#--   * B1 traps 79/80/81 are [source]-tagged and are real confusions, so they
#--     may be called "easy to confuse." They may NOT be called common exam
#--     material. The tag licenses the confusion, not the frequency.
#-- See Open Question 2.

#-- PREREQ NOTE. `standard`. Two prerequisites, both far back and both
#-- foundational, which is why the Soundings leans on them hard:
#--   Ch 4 §1 (declarative object config, `kubectl apply -f <dir>/`) -> §1
#--   Ch 4 §2 (object anatomy)                                       -> §2, §5
#--   Ch 4 §4 (ConfigMap/Secret as externalized config)              -> §2, §5
#--   Ch 4 §5 (labels and selectors)                                 -> §5
#--   Ch 6 §5 (revisions, `kubectl rollout undo`)                    -> §3  ** the big one **
#--   Ch 6 §8 (custom resources and CRDs)                            -> §2, §6
#--   Ch 2 §3 (registries, tags, digests)                            -> §4
#--   Ch 13 §7 ("somebody has to install that")                      -> §1
#-- Ch 6 §5 is the load-bearing one. §3 exists to separate `helm rollback`
#-- from `kubectl rollout undo`, and a reader who has lost what a Deployment
#-- revision IS cannot receive that separation — they will read §3 as one
#-- mechanism described twice.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard" — 5 points.
#-- Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING — the inverse of Ch 13's situation, and worth stating
#-- plainly so no downstream stage misreads the freedom as licence.
#-- THREE published cross-bearings point into this chapter. NONE names a
#-- section number:
#--   chapter-01:274  -> "see Ch 14-16 - the Application Delivery domain in full"
#--   chapter-06:372  -> "see Ch 14 - a Helm chart's job is to template this object"
#--   chapter-06:720  -> "see Ch 14 - Helm rollback and Deployment rollback are
#--                       different mechanisms wearing the same word"
#--   chapter-06:1036 -> "see Ch 14 - why Helm charts have a `crds/` directory"
#-- (Four pointers, three distinct promises; 01:274 is a range pointer.)
#-- Verified 2026-08-31 against chapters 01-13. No `Ch 14 §N` form exists
#-- anywhere in shipped text.
#--
#-- BUT the numbering is still fixed, from the other direction. B6 records two
#-- DOWNSTREAM sections that will point back here by number:
#--   Ch 15 §4 -> "charts as a manifest source refers to Ch 14 §2"
#--   Ch 17 §4 -> "CRDs shipped as chart content refers to Ch 14 §6"
#-- §2 and §6 are therefore FIXED at those numbers. The skeleton's seven
#-- sections are adopted unchanged, in order, with no renumbering.
#--
#-- ⚠ DECAY RISK — the arc outline flags this chapter explicitly: "thin
#-- downstream presence." Only two downstream anchors exist and B3 marks both
#-- MANDATORY. Neither may be dropped:
#--   Ch 15 §4 (charts as the delivery agent's manifest source)
#--   Ch 17 §4 (CRDs shipped as chart content)
#-- §2 and §6 must each emit the forward cross-bearing that sets its anchor
#-- up. This is not decorative; it is the only thing standing between this
#-- chapter and being read once and never retrieved.
sections:
  - name: "Why a Folder of YAML Stops Working"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-fig01-manifest-to-package-progression"
    checkpoint_after: false

  - name: "What a Chart Contains"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-fig02-helm-chart-anatomy"
    checkpoint_after: false

  - name: "Chart, Release, Revision"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-fig03-release-vs-chart-vs-revision"
    checkpoint_after: false

  - name: "Where Charts Come From"
    objectives: ["D3.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

  - name: "Patching Instead of Templating"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-fig04-kustomize-base-overlay"
    checkpoint_after: false

  - name: "Which One, When"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-fig05-templating-vs-overlay-decision"
    checkpoint_after: true

  - name: "A Package, Not a Template"
    objectives: ["D3.1"]
    requires_figure: true
    figure_anchor: "ch14-zenith-package-not-template"
    checkpoint_after: false

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
soundings_planned:
  question_count: 8
  topics:
    - "What `kubectl apply -f <directory>/` does, and what it does not promise about ordering (Ch 4 §1)"
    - "What 'installing metrics-server' actually consists of in a declarative system (Ch 13 §7 + Ch 4 §1)"
    - "What `kubectl rollout undo` changes, and what it does to revision history (Ch 6 §5)"
    - "A manifest names a `kind` the API server does not recognize — what has to happen first (Ch 6 §8)"
    - "Where environment-specific configuration belongs, and why not baked into the image (Ch 4 §4, Ch 2 §2)"
    - "Image tag versus digest, and what a registry actually is (Ch 2 §3)"
    - "General professional knowledge: what a package manager gives you that a directory of files does not"
    - "Generation-effect prompt: two clusters, same application, different replica counts and hostnames — what are your options with only the tools taught so far?"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 17 = 35, and unlike Ch 12 and Ch 13 this chapter
#-- needs NO override. Reason: Ch 14's arc-outline retrieval target is 20%,
#-- not the 25% ceiling, and 20% divides evenly into 10 — two retrieval items
#-- across two checkpoints of five lands at EXACTLY 20.0%. The Ch 12/13
#-- precedent for raising B4's Bearings figure existed only to make a 25%
#-- ceiling reachable cleanly; that pressure is absent here. B4's numbers
#-- stand unmodified.
question_budget:
  soundings: 8
  taking_your_bearings: 10             # across 2 checkpoints (5 + 5)
  practice_questions: 17
  total_this_chapter: 35

#-- Concept / objective / command tagging -------------------------------
kb_tags:
  objectives: ["D3.1"]
  concepts:
    - "manifest-sprawl"
    - "environment-variation"
    - "apply-ordering"
    - "helm"
    - "chart"
    - "chart-yaml"
    - "values-yaml"
    - "chart-templates-directory"
    - "chart-dependencies-directory"
    - "chart-crds-directory"
    - "subchart"
    - "notes-txt"
    - "chart-helpers"
    - "go-template-in-helm"
    - "helm-release"
    - "helm-release-revision"
    - "helm-rollback-versus-rollout-undo"
    - "chart-repository"
    - "oci-registry-as-chart-store"
    - "chart-version-versus-appversion"
    - "kustomize"
    - "kustomization-yaml"
    - "base-and-overlay"
    - "strategic-merge-patch"
    - "json-patch"
    - "configmap-generator"
    - "secret-generator"
    - "templating-versus-overlay"
    - "crd-ordering-problem"
  commands:
    - "helm-install"
    - "helm-upgrade"
    - "helm-rollback"
    - "helm-list"
    - "helm-repo-add"
    - "kubectl-apply-k"

#-- COMMANDS NOTE. Deliberately short. Ch 13's materialisation raised an
#-- AUTHOR-REVIEW because its outline listed two `crictl` subcommands the
#-- draft correctly declined to teach. Same discipline here: this list names
#-- only commands the chapter will actually demonstrate. `helm template`,
#-- `helm pull`, `helm dependency update`, `helm status`, `helm get`, and
#-- `kubectl kustomize` are all deliberately ABSENT. If drafting demonstrates
#-- one of them, add it here rather than letting the concept index under-claim
#-- — but the associate-tier default is not to.

figures_planned:
  - "ch14-fig01-manifest-to-package-progression"
  - "ch14-fig02-helm-chart-anatomy"
  - "ch14-fig03-release-vs-chart-vs-revision"
  - "ch14-fig04-kustomize-base-overlay"
  - "ch14-fig05-templating-vs-overlay-decision"
  - "ch14-zenith-package-not-template"
---
```

# Chapter 14 Outline — Packing for the Voyage

## Chapter-type note (read first)

`content`. Full structural contract applies: witty subtitle, Attention Budget, epigraph, 🧭 Soundings, Why This Chapter Matters, What You'll Learn, ≥2 ☆ Taking Your Bearings, Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead.

**Heading form:** `## <difficulty> §N — Title`, the Ch 5–8 majority form that B6 recommends for Ch 9–19 and that shipped Ch 9–13 use. **Closing section takes `☀️` in place of a difficulty glyph**, per B6 recommendation #4.

**Part boundary.** This is the first chapter of **Part IV — Dispatches** (Ch 1:399). Ch 13 closed Part III. The chapter opens a new Part and should carry the small extra orientation beat that implies: the reader has finished learning how the cluster works and how to tell when it isn't, and is now learning how software gets onto one.

---

## 1. Why This Chapter Matters

Ch 13's Voyage Ahead already wrote this chapter's opening for us, and the draft should take the handoff rather than invent a new one. Line 1830: *"This chapter kept saying 'somebody has to install that': metrics-server, a logging backend, an Ingress controller. The next chapters are about how anything gets installed on a cluster at all, and about the moment a folder full of YAML stops being a workable answer."* That promise is due immediately, in the first paragraph, in those terms.

The curiosity gap is the gap between what the reader has been told and what they have never been shown. Thirteen chapters have said "install a CNI plugin," "install an Ingress controller," "install metrics-server," "install a CSI driver" — and not one of them said *how*. The reader has been quietly accumulating an unpaid debt. The question the chapter opens on: when the answer to "how do I install this" is "apply about forty YAML files, in roughly this order, with six values changed for your cluster" — what is the thing you are actually being handed, and why does it not have a name yet?

The identity frame is a shift in what the reader is holding. Up to now every artifact in this book has been a single object: a Pod, a Deployment, a Service. Practitioners do not hand each other objects. They hand each other *units* — a named, versioned thing that installs as one act and uninstalls as one act, that somebody else can take and run without reading it, and that can be undone when it turns out to be wrong. This chapter is where the reader stops writing manifests and starts shipping software.

The stakes are honest and stated once: this is the domain whose weight doubled. Ch 1:274 already told the reader that Cloud Native Application Delivery went from 8% to 16% and that material built for the old blueprint under-serves it by half. This is the first chapter to actually cash that.

**Mandatory honesty beat — do not omit.** Somewhere in this section, in one short paragraph, the chapter states that CNCF publishes the competency name "Application Delivery" and no sub-topic list; that Helm and Kustomize appear nowhere in the published curriculum; and that their presence here is derived from the bundled LFS250 module and from what the ecosystem actually uses. Then it says why that is still the right call. This is the same move Ch 1 made about the 60-question figure, and the book's credibility on the unpublished numbers depends on making it consistently. See Open Question 2.

**Voice guardrail.** The wry beats belong to the practitioner's own filing habits — the directory containing `deployment-prod-final-v2-USE-THIS-ONE.yaml`, the `sed` command in a runbook, the environment that drifted because somebody fixed staging and forgot production. Never at anyone harmed by a bad deploy. Skill Part 14, subject dignity.

**Register guardrail.** The chapter title and Part name are already doing the cargo work. Resist a second layer. `structural-contract.yaml` forbids `batten down the hatches`, `chart a course`, `set sail`, `smooth sailing`; note that **"chart" is a technical term throughout this chapter**, which makes `chart a course` an unusually easy accident here. US spelling throughout.

---

## 2. What You'll Learn

- **Name** the four things a folder of manifests cannot do, and recognize each one when you hit it
- **Read** a Helm chart's directory layout and say what each entry is *for*
- **Separate** package from installation from installed-state — chart, Helm release, release revision — and stop collapsing them into one word
- **Distinguish** `helm rollback` from `kubectl rollout undo`: different unit, different mechanism, same word
- **Explain** what Kustomize does instead of templating, and why it needs no engine you have to install
- **Choose** between the two for a given situation, and say what the choice actually turns on

*You'll also stop thinking of this as a chapter about YAML syntax, which is the misreading it exists to prevent.*

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Every question is answerable from Chapters 1–13 or from general professional knowledge. Two carry extra load: **Q3 is the chapter's most important pre-test** (it sets the Ch 6 §5 baseline that §3 needs in order to separate the two rollbacks), and **Q8 is a generation-effect prompt** (skill Part 10) that states the chapter's problem without hinting at its answer.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | What `kubectl apply -f <directory>/` does across a whole directory, and what it does not promise about the order files are applied in | Ch 4 §1 | §1's entire argument is "this technique has limits." A reader who never held the technique clearly cannot feel the limits. Ch 4 line 310 stated the directory form explicitly; this measures whether it survived nine chapters. |
| 2 | You need metrics-server on a cluster that does not have one. In a declarative system, what does "install it" concretely consist of? | Ch 13 §7 + Ch 4 §1 | The bridge question, and the discharge of Ch 13's own handoff. The right answer — "a set of objects somebody wrote, that you apply" — *is* §1's starting position, arrived at by the reader rather than announced. |
| 3 | `kubectl rollout undo` on a Deployment: what does it change, and what does it do to the revision history? | Ch 6 §5 | **The load-bearing one.** §3 exists to separate two mechanisms that share a word; that separation is unreadable if one half is missing. A wrong answer here must send the reader back to Ch 6 §5 *before* §3, not alongside it. |
| 4 | A manifest names a `kind` the API server does not recognize. What has to happen first, and who does it? | Ch 6 §8 | Pre-tests the ordering intuition that §6's `crds/` explanation depends on, using only Ch 6 vocabulary. **Does not mention charts, directories, or Helm.** |
| 5 | Where does environment-specific configuration belong, and why is baking it into the image the wrong answer? | Ch 4 §4 + Ch 2 §2 | `values.yaml` is this idea one level up. Testing the idea at the object level first means §2 can present values as a familiar move rather than a new one. |
| 6 | Image tag versus digest, and what a registry actually is | Ch 2 §3 | §4 claims a registry can hold things that are not images. That claim only lands for a reader who still has a clear model of what a registry is. |
| 7 | From your own professional experience with any package manager — apt, npm, pip, NuGet, Homebrew — what does it give you that a folder of files does not? | General professional knowledge | The transferable intuition, and the chapter's best arousal move. Adult professionals already own this answer; the chapter's job is to show them they were holding it. Answerable with zero Kubernetes. |
| 8 | Two clusters need the same application with different replica counts and hostnames. Using only what this book has taught so far, what are your options — and what is wrong with each? | Ch 4 + Ch 6 | **Generation effect.** The reader constructs the problem statement themselves. Every honest answer (copy the directory; `sed` it; hand-edit) is a trade-off §1 then names. Nothing here reveals that a solution exists. |

### FIXED-POINT SPOILER CHECK

The chapter's candidate Fixed Points, and the confirmation that no Soundings question states one:

| Candidate ★ Fixed Point | Spoiled by any Soundings question? |
|---|---|
| A chart is a package. A Helm release is an installed instance of it. One chart, many releases. | **No.** Q7 asks what package managers give you generally; it never reaches the chart/release split, and the words "chart" and "release" appear in no stem. |
| `charts/` is a directory of dependency charts *inside* a chart. A chart repository is an HTTP server. Different things. | **No.** No stem mentions either. |
| `helm rollback` and `kubectl rollout undo` are different mechanisms wearing the same word — different unit, different scope. | **No.** Q3 asks only what `kubectl rollout undo` does. It does not hint that anything else claims the word. |
| Kustomize does not template. It patches a base it never modifies. | **No.** Kustomize is named in no stem, and Q8's honest answers are all copy-or-edit, not patch-without-modifying. |
| Templating is a means. The unit is the point. | **No** — and this is the one to watch. Q7 approaches it from outside, via package managers generally, which is the motivation rather than the claim. If drafting sharpens Q7 toward "what does a package give you that a template does not," it becomes a spoiler. Keep Q7 tool-agnostic. |
| `crds/` exists because a CustomResourceDefinition must be registered before any custom resource that uses it can be created. | **No.** Q4 tests the ordering rule in Ch 6's own terms and never mentions packaging. |

Clean, with one watch item recorded. The subtitle states Fixed Points #1 and #5 on the chapter's second line — that is the subtitle's job and is not a licence to relax the above.

**Rubric branches (all three mandatory):**
- **6+** → skim, but read §3 and §6 properly. Those two are what the chapter is actually about; the rest is vocabulary you can move through fast.
- **3–5** → normal pace.
- **0–2** → **re-read Ch 4 §1 before starting**, not alongside. Name the section, not the chapter. If Q3 specifically was missed, add Ch 6 §5.

---

## 4. Section plan

### `## ⚪ §1 — Why a Folder of YAML Stops Working`

Owns the **problem statement**, and owns it as an argument rather than a preamble. Four named failures of `kubectl apply -f <dir>/`, each demonstrated rather than asserted: **environment variation** (the same application, three clusters, six values different); **apply ordering** (nothing guarantees the namespace exists before the object that lives in it, or the CRD before the custom resource); **versioning** (a directory has no version, so "which one is running" has no answer); and **distribution** (there is no way to hand somebody a directory that they can install without reading it). Takes the Ch 13 handoff explicitly in the opening paragraph. Names Helm and Kustomize once each, as the two answers the chapter will examine, and stops — the reader should leave §1 knowing the shape of the problem and nothing about the solutions.

- **Objectives:** D3.1 (Application Delivery — from raw manifests to packages)
- **Introduces:** manifest-sprawl; environment-variation; apply-ordering
- **Figure:** `ch14-fig01-manifest-to-package-progression`
- **Cross-bearings out:** `Ch 4 §1 — declarative object configuration and kubectl apply`; `Ch 13 §7 — metrics-server, and what "somebody has to install that" costs`; `Ch 6 §8 — custom resources and CRDs` (for the ordering example)
- **Guardrail:** do not solve anything here. §1's job is to make the reader *want* §2. If drafting finds itself explaining what a chart is, it has run past the section boundary.
- **Ledger note:** **Kustomize's first appearance in the book is here** (ledger: "first appears Ch 14 §1†"). Name only — the definition is §5, and the mention carries a pointer.
- **Checkpoint:** none

### `## ⚪ §2 — What a Chart Contains`

Owns **Helm** and **chart** as definitions, and the chart's anatomy. `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/`, plus `NOTES.txt` and `_helpers.tpl` at lower resolution. Every entry is explained by *what it is for*, not by what it is — a directory listing is not teaching. Owns **subchart** and the one-sentence statement of Go templating as Helm's rendering mechanism. The section's thesis, and the reason it is not merely a file tour: **the chart is the unit; templating is how the unit absorbs variation, not what the unit is.**

Trap 81 is pre-empted here rather than in §4: `charts/` gets an explicit "this is not a repository" clause at the moment it is introduced, because that is where the confusion forms.

- **Objectives:** D3.1 (Helm — chart structure)
- **Introduces:** helm; chart; chart-yaml; values-yaml; chart-templates-directory; chart-dependencies-directory; chart-crds-directory; subchart; notes-txt; chart-helpers; go-template-in-helm
- **Figure:** `ch14-fig02-helm-chart-anatomy`
- **Cross-bearings out:** `Ch 4 §2 — the anatomy of a record`; `Ch 4 §4 — configuration kept outside the image`; `Ch 6 §8 — custom resources and CRDs`; **`Ch 15 §4 — an agent that watches a repository`** ← **MANDATORY B3 ANCHOR**, and the reason §2 is a pinned number
- **Depth ruling — templating.** Show **one** templated line beside its rendered output and stop. Do not teach the template language: not pipelines, not `range`, not `with`, not the sprig functions. This is an associate exam and the ledger gives §2 "Go template (in the Helm sense)," which is the concept, not the syntax. See Open Question 8.
- **Discharges:** chapter-06:372 — "a Helm chart's job is to template this object." The Deployment from Ch 6 §1 is the natural worked example, and using it makes the discharge visible to the reader who remembers the promise.
- **Checkpoint:** none

### `## 🔵 §3 — Chart, Release, Revision`

**The chapter's core section**, and the one the subtitle names. Owns the **four words readers collapse**: *package* (what a chart is), *manifest* (what it renders to — already the reader's from Ch 4 §2), **Helm release** (an installed instance, named, living in a namespace), and **release revision** (a numbered state of that release). One chart installs many times; each install is a separately named release, independently upgradable and independently undoable.

Then the payoff: **`helm rollback` and `kubectl rollout undo` are different mechanisms wearing the same word.** Different unit — a release versus a single Deployment. Different scope — everything the chart installed versus one workload's Pod template. Different bookkeeping — Helm's release history versus the Deployment's ReplicaSet-backed revision history. This discharges chapter-06:720, which is the most specific promise made to this chapter.

- **Objectives:** D3.1 (Helm — releases, upgrade and rollback)
- **Introduces:** helm-release; helm-release-revision; helm-rollback-versus-rollout-undo; `helm install`; `helm upgrade`; `helm rollback`; `helm list`
- **Figure:** `ch14-fig03-release-vs-chart-vs-revision`
- **Cross-bearings out:** `Ch 6 §5 — every rollout is a revision`; `Ch 6 §1 — the Deployment → ReplicaSet → Pod ownership chain`; `Ch 4 §3 — where a name lives`; `Ch 15 §4 — rollback by revert`
- **⚑ CANONICAL-FORM guardrails — hard, three of them.** (1) **"Helm release" on first use in this section**, never bare "release" where a Kubernetes minor version could be meant. (2) **"release revision" or "Helm revision", never bare "revision"** — Ch 6 §5 owns the unqualified word. (3) **Never write bare "rollback"** anywhere a reader could take it either way; the ledger assigns this section the explicit statement that the two are different, and a bare noun undoes the section's own work.
- **⛑ SANCTIONED ORDINAL — read before drafting.** The book-level convention bars running ordinals *unless the count is fixed by a closed set the reader can see*. Shipped Ch 6:719 published exactly such a set: *"you are going to meet the word 'rollback' twice more in this book attached to entirely different mechanisms,"* followed by pointers to Ch 14 and Ch 15. §3 may therefore say it is discharging one of those two, and may name the third as still owed to Ch 15 §4. It may **not** invent any other count — no control-loop tally, no "the fourth time you've seen this."
- **Checkpoint:** none

### `## ⚪ §4 — Where Charts Come From`

Owns **distribution**. A **chart repository** is an HTTP server housing packaged charts, managed with `helm repo` — the second half of trap 81, and the point at which the reader who did not catch §2's clause gets caught properly. Owns **OCI registries as chart stores**, which is where Ch 2 §3 pays off in a way the reader will not expect: the registry they learned about for images also holds charts, because the OCI distribution spec was never about images specifically. Owns **chart version versus `appVersion`** — the chart is versioned separately from the software it installs, and conflating them is the quiet error in this section.

- **Objectives:** D3.1 (Helm — chart repositories)
- **Introduces:** chart-repository; oci-registry-as-chart-store; chart-version-versus-appversion; `helm repo add`
- **Figure:** none, deliberately. This is a vocabulary section, and its one genuinely visual distinction — `charts/` versus a repository — is better carried by `ch14-fig02`'s explicit label than by a second figure competing with it. See Required figures.
- **Cross-bearings out:** `Ch 2 §3 — registries, tags, and digests`; `Ch 2 §5 — the Open Container Initiative`
- **Guardrail:** the OCI-holds-charts fact is a genuine ☀️-adjacent moment and should be written as a small one, but the chapter's Zenith is §7 and this is not it. One paragraph, one back-bearing, move on.
- **Checkpoint:** **☆ TYB 1** — closes the Helm arc (§1–§4)

### `## 🔵 §5 — Patching Instead of Templating`

Owns **Kustomize**, which is **blocking gap G19** and has ten lines of cached source. The thesis in one line: Kustomize introduces a template-free way to customize configuration — it does not render, it patches, and it never modifies or copies the base. Owns **base and overlay**, `kustomization.yaml`, **strategic-merge and JSON patches**, **generators** (`configMapGenerator`, `secretGenerator`), and **`kubectl apply -k`** — including the fact that carries real exam value: it is built into kubectl, so there is no engine to install.

The section's structural job is contrast, not neutrality. The reader has just spent three sections inside a system that renders text; this one has to make "patch a thing you never edit" feel like a different idea rather than a different syntax.

- **Objectives:** D3.1 (Kustomize — base and overlay)
- **Introduces:** kustomize; kustomization-yaml; base-and-overlay; strategic-merge-patch; json-patch; configmap-generator; secret-generator; `kubectl apply -k`
- **Figure:** `ch14-fig04-kustomize-base-overlay`
- **Cross-bearings out:** `Ch 4 §5 — labels and selectors` (common labels); `Ch 4 §4 — ConfigMaps and Secrets` (generators); `Ch 4 §2 — apiVersion, kind, metadata` (what a patch targets)
- **⚠ RESEARCH-BLOCKED.** This section cannot be drafted from the cached corpus. `kustomize-overview-2026-08-23.md` is a 10-line marketing-page summary with no field reference, no patch syntax, and no generator detail. See Open Question 1 — two fetches are mandatory before drafting.
- **Ledger note:** if the draft says Kustomize is a Kubernetes **SIG CLI** project, "SIG" is owned by Ch 17 §8 and earlier chapters must use it **name-only with a pointer**. Recommendation: say "maintained by the Kubernetes project itself" and avoid the acronym entirely — it buys nothing here.
- **Checkpoint:** none

### `## 🔵 §6 — Which One, When`

Owns the **decision**, and owns the `crds/` explanation. The decision is not a preference poll: it turns on whether you are *distributing* software to people who will not read it (Helm, because a package needs a version, a repository, and a lifecycle) or *adapting* software you already have for environments you control (Kustomize, because there is nothing to distribute and a template engine is overhead). Owns **using both together** at name-only depth.

Then the `crds/` payoff, which discharges chapter-06:1036. A CustomResourceDefinition must be registered before any custom resource using it can be created, and a single rendered stream of manifests gives no ordering guarantee — this is precisely failure #2 from §1, returning at the end of the chapter as something the reader can now diagnose. `crds/` exists to solve it: those definitions install first, before the templates render.

- **Objectives:** D3.1 (when each fits; CRDs shipped as chart content)
- **Introduces:** templating-versus-overlay; crd-ordering-problem
- **Figure:** `ch14-fig05-templating-vs-overlay-decision` — **new; not in the arc stub list.** See Required figures.
- **Cross-bearings out:** `Ch 6 §8 — the control loop, extended` (CRDs); **`Ch 17 §4 — the four pluggable interfaces, collected`** ← **MANDATORY B3 ANCHOR**, and the reason §6 is a pinned number
- **⚑ Ledger guardrail:** the CRD **definition** belongs to Ch 6 §8. §6 owns only the *ordering problem* and the directory that solves it. If drafting starts explaining what a CustomResourceDefinition is, it has taken Ch 6's material.
- **Structural note:** §1's four failures should be visibly answered by the end of §6 — variation by values and overlays, ordering by `crds/`, versioning by chart version, distribution by repositories. Making that closure explicit is what earns §7.
- **Checkpoint:** **☆ TYB 2** — closes the Kustomize-and-decision arc (§5–§6)

### `## ☀️ §7 — A Package, Not a Template`

Zenith. The recognition is that the reader has been comparing the wrong things. Helm and Kustomize disagree completely about mechanism — one renders text from values, the other patches YAML it refuses to modify — and agree completely about the goal: turn a directory of files into **one named, versioned, addressable unit that installs as a single act and can be undone as a single act.** The templating argument that the ecosystem spends so much energy on is an argument about *how*, conducted by two tools that already agreed on *what*. That is the subtitle's second clause, arriving as a conclusion rather than a claim.

Closes by pointing at the question that is now unavoidable and that this chapter cannot answer: you have a unit. Who applies it, and when, and from where? That is Ch 15.

- **Figure:** `ch14-zenith-package-not-template`
- **Cross-bearings out:** `Ch 15 §3 — push, or pull`; `Ch 4 §6 — a declaration, not an order`
- **⛑ CONVENTION guardrail — read before drafting.** §7 may observe that a package is a declaration with a version on it and may back-bear to Ch 4 §6. It **must not** reach for the control loop, and it must not assert any running ordinal. Ch 15 §7 is the book's **primary Zenith** and it is the control-loop payoff; shipped Ch 6 already told the reader "the third time is the one that matters." This chapter's Zenith is its own — mechanism versus unit — and borrowing Ch 15's would spend a recognition the book has been saving for nine chapters.

---

## 5. ☆ Taking Your Bearings checkpoints

Two checkpoints, 10 questions, **2 retrieval questions = exactly 20.0%**, the arc outline's target for this chapter (not the 25% ceiling — that applies to Ch 13, 15, 16, 17, 18).

**Retrieval is defined narrowly**, per the Ch 13 precedent, and drafting must hold the line: a retrieval question is one whose *answer* lives in an earlier chapter. A question about `helm rollback` that merely leans on the reader knowing what a Deployment is remains a chapter question.

| # | Falls after | Topic | Qs | Retrieval | Drawn from |
|---|---|---|---|---|---|
| TYB 1 | §4 | The package and the thing you installed | 5 | 1 | **Ch 6 §5** — what `kubectl rollout undo` changes and what it leaves in the history (≥4-back floor; sets the §3 contrast in tension rather than restating it) |
| TYB 2 | §6 | Patching, and choosing | 5 | 1 | **Ch 13 §7** — the component that has to be installed before anything works (the Ch 9–13 draw the arc outline requires; the item asks what "install metrics-server" means now that the reader has a word for it) |

Both draws are specified by the arc outline: 20%, from Ch 9–13, with the ≥4-back floor satisfied by Ch 4 and Ch 6. TYB 1 satisfies the floor; TYB 2 satisfies the Ch 9–13 window.

Every checkpoint carries trap answers targeting the misconceptions in the Exam Alert below, why-wrong explanations for **all** options, and a revision prompt naming a **section** for 0–2 scorers.

**TYB 1 must include the chart/release item and the `charts/`-versus-repository item.** Those are B1 traps 80 and 81 and they are the two things a reader most reliably gets wrong; a checkpoint that omits them is not doing its job.

---

## 6. Exam Alert plan

**High-priority topics.** Four, and the chapter is these four:

1. **Chart, Helm release, release revision — three words, three things.** A chart is the package. A release is one installation of it. A revision is one numbered state of that release. One chart, many releases; one release, many revisions.
2. **`charts/` is not a chart repository.** `charts/` is a directory *inside* a chart holding the charts it depends on. A chart repository is an HTTP server housing packaged charts.
3. **Helm is a package manager, not a template engine.** Templating is one mechanism inside it. Kustomize solves the same problem with no templating at all, which is the clearest possible proof that templating was never the definition.
4. **Kustomize is built into kubectl** (`apply -k`) and is template-free. Nothing to install; nothing rendered.

**Common traps** — ⚠ Navigational Hazards, loss-aversion framing. Sources noted, because three of these are B1 `[source]` traps and the rest are derived:

| Trap | The correct understanding | Origin |
|---|---|---|
| "Helm is a templating engine" | It is a packaging system: chart → values → templates → **Helm release**. Templating is a means. | B1 #79 |
| Using "chart" and "release" interchangeably | One chart installs many times; each install is a separately named Helm release, independently upgradable and independently rolled back. | B1 #80 |
| Reading `charts/` as a chart repository | `charts/` holds **dependency** charts inside a chart. A repository is an HTTP server, managed with `helm repo`. | B1 #81 |
| Assuming `helm rollback` runs `kubectl rollout undo` underneath | Different unit and different scope. A Helm rollback returns the whole release to a previous revision; `rollout undo` changes one Deployment's Pod template. | Derived from Ch 6 §5 + §3 |
| Reading chart version as the version of the software | The chart has its own version. `appVersion` is the application's. They move independently. | Derived, §4 |
| Assuming Kustomize needs an engine installed | It is in kubectl. `kubectl apply -k` works on a stock installation. | Derived, §5 |
| Assuming an overlay edits or copies the base | It does neither. The base is untouched and unduplicated; the overlay declares only its deltas. | Derived, §5 |
| **"You have to run Tiller"** | Helm 3 removed Tiller. Material that mentions it predates 2019 and is describing a Helm that no longer exists. | **Derived — REQUIRES A SOURCE, see Open Question 5** |

**Blueprint-transition beat.** The Tiller trap belongs in the same family as B2 disclosure #3: this domain doubled in weight and much of the available prep material predates the change. One sentence connecting them is worth writing.

**Framing constraint, restated because it is easy to lose in an Exam Alert:** none of these may be described as "frequently tested" or "commonly appears." CNCF publishes no sub-topic list for this competency. "Easy to confuse" and "the distinction the material rewards" are the available registers. See Open Question 2.

---

## 7. Practice Questions plan

**Target: 17**, per `question_budget.practice_questions` and B4, unmodified.

| Section | Items | Rationale |
|---|---|---|
| §1 the problem | 1 | Method, not recall; better carried by scenario stems elsewhere |
| §2 chart anatomy | 4 | The largest single vocabulary load, and trap 81 forms here |
| §3 chart / release / revision | 5 | The chapter's core, traps 79 and 80, and the Ch 6 rollback contrast |
| §4 repositories and versions | 3 | Trap 81's second half plus chart-version-vs-appVersion |
| §5 Kustomize | 3 | Blocking gap G19; the reader has one section of exposure and needs the reps |
| §6 the decision | 1 | Judgment, and one well-built scenario beats three recall items |

**Interleaving strategy.** At least five stems present a *situation* and ask what the reader would reach for, rather than asking for a definition — the shape a glossary cannot answer. Three stems cross domains deliberately: one pairs a chart with a Deployment rollback (D1.1 workloads), one pairs an OCI registry with image identity (D1.4 containerization), one pairs a chart that installs a CRD with the ordering problem (D1.1 extensibility). Per skill Part 10, wrong options are built to catch the specific misconceptions tabulated in the Exam Alert, and every option gets a why-wrong explanation.

**Barred from all graded text in this chapter:**

- **Argo CD, Flux, GitOps sync states, and the deployment-strategy vocabulary** (blue/green, canary, A/B). All are Ch 15's, and B1 traps 73–78 belong to that chapter. A Ch 14 item testing them would strip Ch 15 of its own material.
- **Knative, serverless, and the twelve-factor app** (Ch 15 §1, Ch 17 §6). B1 traps 82–86.
- **PodDisruptionBudget** — unowned book-wide (⚑3), barred everywhere including here.
- **ABAC, SRE, descheduler, eBPF** — glossary-only with graded-use restrictions.
- **Any item hinging on the absence of a Kubernetes LTS** (unresolved; see Ch 13 outline Open Question 3).
- **Any item requiring Helm template-language syntax.** The §2 depth ruling authorizes one templated line as illustration; a question that needs the reader to write or read a template exceeds what the chapter taught and what the exam is.

---

## 8. Required figures

Six anchors: five concept diagrams plus one Zenith, inside skill Part 18.10's 2–8 band.

| Anchor | § | Type | Purpose and content |
|---|---|---|---|
| `ch14-fig01-manifest-to-package-progression` | §1 | Progression, three panels | Left: one directory of loose YAML, one cluster. Middle: the same directory copied three times for three environments, with the drifted values highlighted — the failure made visible. Right: one versioned package plus three small values files. The middle panel is the emphasized element; it is the state the reader is probably in. ≤7 labels. **Glyph-free** — progression family, not stack or pipeline. |
| `ch14-fig02-helm-chart-anatomy` | §2 | Annotated hierarchy | A chart directory tree with **exactly five** annotated entries — `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/` — each annotated with what it is *for*, not what it is. `README`, `LICENSE`, `NOTES.txt` appear greyed and unannotated so the tree is honest without spending labels. **`charts/` carries the load-bearing annotation: "charts this chart depends on — NOT a repository."** That single label is trap 81's pre-emption and the reason this figure exists rather than a plain listing. **Glyph-free** — hierarchy family. |
| `ch14-fig03-release-vs-chart-vs-revision` | §3 | Containment, three levels | One chart box at the top. Two arrows down to two named Helm releases in two namespaces — same chart, different names, different values. One of those releases expands downward into an ordered revision strip: rev 1 → rev 2 → rev 3. The chapter's central distinction rendered spatially, which is the only way it stops being three words. ≤7 labels. **Glyph-free** — containment family. **This is the chapter's most important figure**; if only one gets illustrator attention, it is this one. |
| `ch14-fig04-kustomize-base-overlay` | §5 | Layering | A base directory drawn once, in the center, visibly unmodified. Two overlays flanking it, each containing only its own deltas (replica count, image tag, name prefix) and a reference back to the base. Arrows from base + overlay converge on a rendered result per environment. The visual claim: **the base is neither edited nor copied.** ≤7 labels. **Glyph policy provisional — glyph-free recommended.** This layers, but it is not the architectural stack family; Stage 10 confirms against `glyph-ledger.yaml` (Ch 13's precedent distinguished "staged-flow" from "pipeline" the same way). |
| `ch14-fig05-templating-vs-overlay-decision` | §6 | Comparative, two columns | **New — not in the arc stub list.** Helm and Kustomize side by side across five rows: what varies (values vs patches), the unit (versioned chart vs directory), distribution (repository/OCI vs none), lifecycle (releases and revisions vs none), where the engine lives (installed CLI vs built into kubectl). A closing full-width row states what the choice actually turns on: distributing to strangers, or adapting for yourself. **Added because §6 is the chapter's decision point and Part 18.9's strongest case is "requires distinguishing similar-sounding alternatives"** — the one criterion this chapter meets more clearly than any other. ≤7 rows. **Glyph-free** — comparison family. |
| `ch14-zenith-package-not-template` | §7 | Dramatic synthesis | Two divergent paths — **RENDER** on the left, **PATCH** on the right — converging on a single labeled object: *one named, versioned, installable unit.* The mechanisms are drawn as visibly different; the destination is drawn as visibly identical. The whole argument in one image. Exactly one Zenith per content chapter, per Part 18.10. |

**Deviations from the arc-outline stub list, recorded so no downstream stage reads them as drift.** One figure added (`ch14-fig05`) with the rationale above. All five original stubs are retained at their original anchor IDs and land in the sections their names imply, so numbering is in document order and no renumbering note is required — unlike Ch 13. **§4 is deliberately figure-free**; its one visual distinction is carried by `ch14-fig02`'s `charts/` annotation, and a second figure making the same point would compete with the first rather than reinforce it.

---

## 9. Open questions for the author

**1. Blocking research — Stage 2 must fetch these, and this is the most under-sourced chapter in the book.** The cached corpus holds **33 lines total** on this chapter's entire subject: `helm-charts-2026-08-23.md` at 23 lines (a truncated capture of the chart-structure page — it has the file list but no `Chart.yaml` field reference, no version/`appVersion`, no `crds/` semantics) and `kustomize-overview-2026-08-23.md` at 10 lines (a marketing-page summary). B1 flags **G19 (Kustomize)** as blocking; in practice §2, §3, §4 and §5 are all under-sourced. Every factual sentence in this book carries a `[source:]` tag, and this chapter cannot currently produce them. Required snapshots, in priority order:

- `helm.sh/docs/topics/charts/` — **full page**, re-fetched. The `Chart.yaml` field reference, chart version vs `appVersion`, dependencies, and the `crds/` limitations. Feeds §2, §4, §6.
- `kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/` — **G19, the critical one.** Bases, overlays, patches, generators, `kubectl apply -k`. Feeds all of §5.
- `helm.sh/docs/intro/using_helm/` — `install`, `upgrade`, `rollback`, `list`; the release and revision model. **Feeds §3, the chapter's core section.**
- `helm.sh/docs/topics/chart_repository/` — repository as an HTTP server, `index.yaml`, `helm repo`. Feeds §4 and trap 81.
- `helm.sh/docs/topics/registries/` — OCI registries as chart stores. Feeds §4.
- `helm.sh/docs/chart_best_practices/custom_resource_definitions/` — **the `crds/` ordering problem and its limitations.** This is the snapshot that discharges chapter-06:1036; without it §6 cannot be written.
- `kubectl.docs.kubernetes.io/references/kustomize/kustomization/` — field reference, for §5's patch and generator detail.
- `helm.sh/docs/faq/changes_since_helm_2/` — for the Tiller hazard; see item 5.

**2. The honesty framing — author confirmation wanted, though the recommendation is firm.** CNCF publishes "Application Delivery" and nothing more; neither cached curriculum snapshot contains the word "Helm" or "Kustomize." This chapter is built entirely on authored inference from the bundled LFS250 module and ecosystem consensus. Recommendation: state it once in Why This Chapter Matters, in the same register Ch 1 used for the unpublished 60-question figure, and enforce the no-frequency-claims rule throughout. The alternative — writing Helm as though it were a published objective — is the kind of small dishonesty that the rest of this book has consistently refused, and it would sit oddly two Parts after Ch 1 made a point of the distinction. **Confirm.**

*Related, low priority:* shipped `chapter-01:274` names "GitOps, Helm, deployment strategies" as this domain's content in an untagged sentence following a tagged one. The tagged claim (8%→16%) is fully supported; the topic list is authored gloss. Not a mis-tag and not load-bearing, but a fact-accuracy pass may query it. Recorded, no action recommended.

**3. Two facts that must not be written from memory.** (a) **What `helm rollback` does to the revision counter** — whether the rollback itself becomes a new numbered revision. This is the discriminating detail in §3's central contrast and it must come from `using_helm`, not from recall. (b) **Where Helm 3 stores release state.** The answer (Secrets in the release namespace, by default) is a genuinely good ⚓ Worth Securing because it ties straight back to Ch 4 §4 — but only if a snapshot supports it. If neither is pinned by a source, write the shape and drop the specific, per house practice.

**4. Argo CD naming — recommendation, confirm.** §7 and §6 both want to gesture at the tool that consumes charts. The ledger's projected first appearance for Argo CD is **Ch 15 §3**, and the "Earlier chapters must" column is empty, so naming it here would not violate the ledger — it would only falsify a projection. Recommendation: **do not name it.** Write "a delivery agent" and point at `Ch 15 §4 — an agent that watches a repository`. It costs nothing, it preserves Ch 15's reveal, and the pointer carries all the information the reader needs. GitOps, by contrast, *is* already in shipped Ch 1 as name-only-with-pointer and may be used the same way here.

**5. Tiller — hazard worth writing, source required.** Helm 3 removed Tiller in 2019, and a large volume of the third-party KCNA prep that B2 disclosure #3 warns about still describes the Helm 2 architecture. This is exactly the shape of hazard the book has been good at. It needs `helm.sh/docs/faq/changes_since_helm_2/` (or equivalent) before it can be stated. **If the fetch does not happen, cut the trap rather than assert it untagged.**

**6. Section-count sanity, recorded pre-emptively.** Seven sections against 5 weight points, one more than Ch 11's seven at the same weight. This is not inflation: §1 is a problem statement rather than content, §7 is the Zenith, and §4 and §6 are both short. The teaching load is genuinely in §2, §3 and §5. No compression is recommended, and §2 and §6 cannot move regardless — Ch 15 §4 and Ch 17 §4 point at those numbers.

**7. Acronym register.** No new acronyms are expected. **OCI** is registered to Ch 2 §5 and already expanded; **CRD** to Ch 6 §8. Two watch items: **SIG** (if §5 calls Kustomize a SIG CLI project — recommendation in §5's block is to avoid it) and **JSON** (ambient tier, so `JSON patch` needs no expansion, but "strategic-merge patch" and "JSON patch" should both be glossed in one clause since neither is defined anywhere else in the book). Recorded for the glossary build alongside the existing Ch 9/10/11/13 debts.

**8. Templating depth — recommendation, confirm.** Show one templated line beside its rendered output; explain that values fill placeholders; stop. Do not teach `range`, `with`, pipelines, or sprig. Rationale: this is an associate credential, the ledger assigns §2 "Go template (in the Helm sense)" rather than the language, and the chapter's own thesis is that templating is not the point — a section that taught template syntax would argue against §7 with its own page count. **Confirm.**

**9. Epigraph.** The material invites a quote about packaging, standardization, or the difference between a thing and an instance of it. Preference order per skill Part 15: a real practitioner or engineering figure over a Lodestar original. Flagged because the epigraph is `expected` in the structural contract and this chapter's register — practical, slightly dry, faintly amused at its own filing systems — narrows the field. Ch 2's shipping-container epigraph territory is adjacent and should not be repeated.