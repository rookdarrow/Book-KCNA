I read the two binding contracts, the arc-outline block, B1's D3.2 entry, and verified every published pointer into Ch 16 by line number against chapters 01–15. **Five of eight sections are pinned by number** (§1–§5); only §6, §7 and §8 are free, and §6 is pinned by topic. Ch 13 also left this stage a direct instruction in an `AUTHOR-REVIEW` comment about frontmatter objectives, which this outline discharges.

```
---
chapter: 16
chapter_type: "content"
title: "Your Application, Their Cluster"
subtitle: "Four questions that separate your bug from theirs"
exam_domain: "Cloud Native Application Delivery (competency: Debugging)"
domain_weight_pct: 4
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE — CHANGED FROM THE ARC OUTLINE. See Open Question 1.
#-- B2 and B3 both carry *"Four questions that separate 'my code is
#-- broken' from 'the platform is broken'"* — thirteen words, against this
#-- stage's own <= 10 constraint, and the only subtitle in the book that
#-- breaches it. The form above is eight words, keeps the four questions,
#-- keeps the scope split, and reads correctly against the title ("theirs"
#-- = the cluster's, i.e. the platform's). No shipped chapter quotes the
#-- long form; grep of chapters 01-15 returns nothing. Author's call,
#-- flagged rather than taken silently.
#--
#-- The subtitle names the chapter's STRUCTURE (four questions) rather
#-- than a Fixed Point, which is the opposite of Ch 13's subtitle and is
#-- correct here — this chapter's Fixed Points are about tools, and a
#-- subtitle naming one would spoil §3.

#-- EXAM_DOMAIN NOTE — TWO OBJECTIVES, DELIBERATELY.
#-- Shipped chapter-13 line 392 left this stage an explicit instruction:
#--
#--   "kubectl exec, kubectl debug / ephemeral containers, kubectl
#--    port-forward, and Service/EndpointSlice debugging are all on the
#--    authored D2.3 Troubleshooting list and are all deferred to Ch 16 ...
#--    Unless Ch 16's frontmatter carries objectives: ["D3.2", "D2.3"],
#--    the book's objective index will show a substantial slice of D2.3
#--    with no owning chapter."
#--
#-- Discharged: kb_tags.objectives below carries both. `exam_domain`
#-- stays single-valued and names D3.2, because that is the domain whose
#-- WEIGHT this chapter draws against (Part IV, D3, 16%) and the house
#-- string form shipped by ch-04/-09/-10/-11/-12/-13 is one domain. The
#-- in-chapter metadata line must carry the published **16%** for D3 with
#-- its source tag and the authored-allocation disclaimer.
#--
#-- The 4% figure is this chapter's AUTHORED allocation, not CNCF data.
#-- CNCF publishes four domain weights (44/28/16/12) and no
#-- sub-competency weights — B1 gap G33, B2 disclosure #1. Do NOT present
#-- 4% as published.

#-- PREREQ NOTE — heavy, and heavy in the same shape as Ch 13: this
#-- chapter is mostly APPLIED prior material, at the arc outline's 25%
#-- retrieval CEILING. Five mandatory anchors, all named by B3:
#--   Ch 13 §1/§8 (the handoff)        -> §1   ** the opening move **
#--   Ch 5 §3 (the init sequence)      -> §2
#--   Ch 5 §5/§7 (phase, probes)       -> §1, §4
#--   Ch 9 §3/§4/§7 (Service -> slice -> Pod, DNS) -> §4
#--   Ch 6 §6 + Ch 11 §6 (StatefulSet identity + PVC) -> §6
#-- Ch 13 §1 is not optional. This chapter's first sentence is the far
#-- side of a handoff the reader was given three chapters ago; a reader
#-- who has lost the scope test cannot receive §1, and §1 is what makes
#-- the other seven sections a method rather than a tool list.
#--
#-- Consequence for drafting: the Soundings 0-2 branch names Ch 13 §1 as
#-- the one section to re-read BEFORE starting, not alongside.
#-- Ch 11/Ch 12/Ch 13 precedent.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "focused" — 4
#-- points, high retrieval load. Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Eleven published cross-bearings
#-- point at this chapter. NINE name a section by number, covering FIVE of
#-- the eight sections:
#--   chapter-05:676  -> Ch 16 §1   when the Pod is fine and the app isn't
#--   chapter-13:388  -> Ch 16 §1   (same wording)
#--   chapter-13:1828 -> Ch 16 §1   (same wording, the Voyage Ahead)
#--   chapter-05:448  -> Ch 16 §2   debugging init containers
#--   chapter-13:566  -> Ch 16 §2   debugging init containers
#--   chapter-12:1342 -> Ch 16 §3   getting inside, and adding what isn't there
#--   chapter-13:390  -> Ch 16 §3   getting inside a container
#--   chapter-09:766  -> Ch 16 §4   a Service whose endpoint list is empty
#--   chapter-13:972  -> Ch 16 §4   is anything even selected
#--   chapter-13:390  -> Ch 16 §5   bypassing the Service on purpose
#-- Two more are unnumbered and pin by TOPIC only:
#--   chapter-06:872  -> Ch 16      debugging StatefulSets and their claims
#--   chapter-08:364  -> Ch 16      `exec`, in the kubectl verb table
#-- §1, §2, §3, §4 and §5 are FIXED. §6 is pinned by topic (Ch 6:872) and
#-- takes StatefulSets. §7 and §8 are free; §8 is structurally fixed as the
#-- Zenith and as the far end of the Ch 13 §8 arc.
#-- All ten numbered pins match the B6 skeleton exactly.
#-- Verified 2026-08-31 against chapters 01-15.
sections:
  - name: "Handed Back"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig01-application-scope-triage"
    checkpoint_after: false

  - name: "When It Never Got Started"
    objectives: ["D3.2"]
    requires_figure: true
    figure_anchor: "ch16-fig05-init-sequence-debug-points"
    checkpoint_after: false

  - name: "Getting Inside, and Adding What Isn't There"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig02-ephemeral-container-debug"
    checkpoint_after: true

  - name: "Is Anything Even Selected"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig04-service-break-points"
    checkpoint_after: false

  - name: "Bypassing the Service on Purpose"
    objectives: ["D3.2", "D2.3"]
    requires_figure: true
    figure_anchor: "ch16-fig03-portforward-vs-service-path"
    checkpoint_after: true

  - name: "When Each Replica Is Its Own"
    objectives: ["D3.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false

  - name: "Before You Ship It"
    objectives: ["D3.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

  - name: "Mine, or the Platform's"
    objectives: ["D3.2"]
    requires_figure: true
    figure_anchor: "ch16-zenith-mine-or-the-platforms"
    checkpoint_after: false

#-- Skill Part 11: Soundings pre-chapter diagnostic ----------------------
soundings_planned:
  question_count: 8
  topics:
    - "The scope test from Ch 13 §1 — Running, Ready, confined to one workload, still wrong (Ch 13 §1)"
    - "What a failed init container does to the rest of the init sequence (Ch 5 §3)"
    - "Where a Running, 0/1 Ready Pod goes in its Service's endpoint list (Ch 5 §7, Ch 9 §4)"
    - "Which of port and targetPort names the port the container listens on (Ch 9 §3)"
    - "The shape of a Service's in-cluster DNS name (Ch 9 §7)"
    - "What is stable about a StatefulSet Pod when it is rescheduled (Ch 6 §6)"
    - "Whether deleting a StatefulSet replica deletes its PVC — a decay probe (Ch 11 §6)"
    - "What is actually inside a minimal image, and what a shell would require (Ch 2 §2)"

#-- Skill Part 8: practice-question budget ------------------------------
#-- B4 allocated 8 / 10 / 15 = 33. Bearings raised to 16 across three
#-- checkpoints (6+5+5), the Ch 12 and Ch 13 precedent. Reason is the same
#-- as Ch 13's and doubly binding here, because this chapter sits AT the
#-- 25% retrieval ceiling rather than below it: 16 is the smallest count
#-- that lets retrieval land at EXACTLY 25% across three checkpoints of
#-- >= 5. At B4's 10, a 25% target rounds to 2.5 and the ceiling cannot be
#-- hit cleanly; at 12 it lands (3/12) but forces two checkpoints across
#-- eight sections, leaving §6-§8 with no retrieval practice at all.
#-- Practice stays at B4's 15 — B4 records 15 as the book's floor and
#-- names this chapter and Ch 13 as the two that sit on it. New total 39.
question_budget:
  soundings: 8
  taking_your_bearings: 16             # across 3 checkpoints (6 + 5 + 5)
  practice_questions: 15
  total_this_chapter: 39

#-- Concept / objective / command tagging -------------------------------
#-- Per the Ch 13 AUTHOR-REVIEW housekeeping note: this list must claim
#-- only what the chapter actually demonstrates. Every command below is
#-- shown in a named section; nothing is listed on the strength of being
#-- adjacent to the topic.
kb_tags:
  objectives: ["D3.2", "D2.3"]
  concepts:
    - "application-scope-triage"
    - "four-triage-questions"
    - "scope-handoff-boundary"
    - "init-container-debugging"
    - "init-container-ordering-and-idempotency"
    - "config-errors-visible-at-init"
    - "distroless-image-debugging"
    - "ephemeral-containers"
    - "debug-profiles"
    - "debug-copy-to"
    - "debug-node"
    - "service-selector-mismatch"
    - "empty-endpointslice-as-symptom"
    - "port-versus-targetport"
    - "readiness-gating-endpoints"
    - "service-dns-name-shape"
    - "port-forward-as-diagnostic"
    - "service-path-versus-api-path"
    - "statefulset-application-debugging"
    - "per-replica-pvc-debugging"
    - "headless-service-dns-names"
    - "local-development-loop"
    - "in-cluster-only-reproduction"
  commands:
    - "kubectl-logs-c-init-container"
    - "kubectl-exec"
    - "kubectl-debug"
    - "kubectl-debug-copy-to"
    - "kubectl-debug-node"
    - "kubectl-port-forward"
    - "kubectl-get-endpointslices"
    - "kubectl-describe-service"

figures_planned:
  - "ch16-fig01-application-scope-triage"
  - "ch16-fig05-init-sequence-debug-points"
  - "ch16-fig02-ephemeral-container-debug"
  - "ch16-fig04-service-break-points"
  - "ch16-fig03-portforward-vs-service-path"
  - "ch16-zenith-mine-or-the-platforms"
---
```

# Chapter 16 Outline — Your Application, Their Cluster

## Chapter-type note (read first)

`content`. Full structural contract applies: witty subtitle, Attention Budget, epigraph, 🧭 Soundings, Why This Chapter Matters, What You'll Learn, ≥2 ☆ Taking Your Bearings, Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead.

**Heading form:** `## <difficulty> §N — Title`, the Ch 5–8 majority form that B6 recommends for Ch 9–19 and that shipped Ch 9–13 use. **Closing section takes `☀️` in place of a difficulty glyph**, per B6 recommendation #4.

**Position note.** This is the last content chapter of Part IV. Its Voyage Ahead hands to Ch 17 and to Part V, not to another delivery chapter.

---

## 1. Why This Chapter Matters

Three chapters ago the platform finished its work and handed the reader back their own problem. This chapter is what happens next, and it opens by taking the handoff rather than by introducing itself — that reciprocity is the whole point of splitting the arc, and shipped Ch 13 has already promised it to the reader three separate times.

The curiosity gap is a genuine reversal of the previous chapter's instinct. Chapter 13 taught the reader to stop reaching for the logs and read the phase first. Here the phase has stopped having anything to say: the Pod is `Running`, it is `1/1 Ready`, its restart count is zero, its node is healthy, and the response is still wrong. Every diagnostic that worked for two hundred pages returns a clean answer, and the system is broken anyway. The question the chapter withholds is: *when every signal the platform publishes says "fine," what do you actually look at?* The answer turns out to be a different set of four questions and a different set of tools, and the reason those tools were withheld until now is that every one of them requires a running container — which is precisely the condition the reader has just finished establishing.

The identity frame is a promotion. Chapter 13's reader was learning to interrogate somebody else's platform. This chapter's reader is the person who shipped the thing, working inside a cluster they do not own, with permissions they did not grant themselves, on an image that may not contain a shell. That is the real posture of an application engineer on Kubernetes, and it is what the chapter title names. The professional move it teaches is not a command — it is knowing which half of the boundary you are standing on before you spend an hour on the wrong half.

The stakes are honest and specific. D3 **doubled** from 8% to 16% in the 2025-11-24 revision [B1], and Debugging is half of it. Legacy prep material sized to the old five-domain blueprint under-serves this domain more than any other. B1's stated posture for D3.2 is blunt — *know which kubectl verb answers which question* — and that is a question a glossary cannot answer, because the verbs are only distinguishable by the question each one is for.

**Voice guardrail.** Skill Part 14, subject dignity. Wry beats stay oriented at the practitioner — the shell that isn't there, the port-forward that works and proves the wrong thing, the afternoon spent editing the wrong YAML file. Nothing wry about outages that harmed users. Do not moralize about production incidents and do not frame the platform team as an adversary; the title's "their cluster" is a statement of scope, not of blame, and §1 should say so in a clause.

---

## 2. What You'll Learn

- **Take** the handoff from platform scope and state, mechanically, which side of the boundary a failure is on
- **Ask** the four questions that localize an application fault — is it running, is it healthy, is it reachable, is it configured — in the order that eliminates the most ground first
- **Read** a failing init container from the application side, and recognize the ordering and re-run assumptions that break one
- **Get inside** a running container with `exec`, and get inside one that has no shell at all with an ephemeral container and `kubectl debug`
- **Diagnose** a Service that exists, selects nothing, and is therefore working exactly as written
- **Prove** where a break is by deliberately bypassing the Service path with `port-forward`

*You'll also stop asking "is Kubernetes broken?" as your first question, which is the habit that costs application engineers the most time on somebody else's cluster.*

---

## 3. Soundings plan — 8 questions

Content chapter, so 8. Every question is answerable from Chapters 1–15 or from general professional knowledge, and **none of them can be answered only from this chapter** — which matters more here than usual, because a chapter that is mostly applied prior material will happily write a Soundings out of its own body if nobody watches.

Two questions (Q1, Q7) are deliberate **decay probes** whose repair is a named section, so the reader's own wrong answer becomes the argument for that section. Q8 is a **generation-effect** setup: it makes the reader notice §3's problem before §3 names the solution.

| # | Topic | Tests | Why it earns its place as a pre-test |
|---|---|---|---|
| 1 | A Pod is `Running`, `1/1 Ready`, restart count 0, no other workload affected, and the response is wrong. Whose problem? | Ch 13 §1 | **Primary decay probe, and the most important of the eight.** The chapter's opening move is receiving a handoff. If the reader has lost the mechanical test, §1 cannot land as a retrieval and degrades into a re-teach — which would duplicate a shipped chapter. The 0–2 branch names this section. |
| 2 | Three init containers. The second exits non-zero. What happens to the third, and to the app containers? | Ch 5 §3 | §2 debugs a sequence the reader must already be able to picture. Tests the *model* of what should happen — Ch 5:448 explicitly said that was Ch 5's job and the method was this chapter's. |
| 3 | A Pod is `Running` and `0/1 READY`. What has happened to its membership in its Service's endpoint list? | Ch 5 §7, Ch 9 §4 | The hinge between §4 and everything before it. Ch 13 §4 called readiness failure "the quiet one"; this measures whether that landed. |
| 4 | Of `port` and `targetPort`, which one names the port the container is actually listening on? | Ch 9 §3 | A genuinely slippery prior, and one of §4's four break points. Pure recall of a shipped field definition, no diagnosis in the stem. |
| 5 | Write the in-cluster DNS name a Pod would use to reach a Service `api` in namespace `payments` | Ch 9 §7 | §4's last break point is a name that resolves to nothing. Tests the shape, not the failure. |
| 6 | A StatefulSet Pod is rescheduled to a different node. Name one thing about it that does not change. | Ch 6 §6 | §6 is built on ordinal identity. Deliberately open-ended — hostname, ordinal, PVC and DNS name are all acceptable, which is the point. |
| 7 | You delete `web-2` from a three-replica StatefulSet. What happens to its PersistentVolumeClaim? | Ch 11 §6 | **Second decay probe.** Ch 11 §6 closed the book's one deliberate forward reference with this fact, five chapters ago. §6's most useful correction depends on the reader having it or knowing they have lost it. |
| 8 | An image is built from a minimal base with no package manager and no `/bin/sh`. What does `kubectl exec ... -- sh` do? | Ch 2 §2 | **Generation-effect setup for §3.** Tests an *image* fact the reader owns — an image contains only what was put in it — and produces the problem statement §3 exists to solve, without naming ephemeral containers, `kubectl debug`, or any remedy. |

### FIXED-POINT SPOILER CHECK

The chapter's candidate Fixed Points, and confirmation that no Soundings question states one:

| Candidate ★ Fixed Point | Spoiled by any Soundings question? |
|---|---|
| You cannot add a container to a running Pod. That is why ephemeral containers exist. | **No.** Q8 establishes the *problem* (no shell in the image) and stops. No stem or answer mentions adding a container, ephemeral containers, or `kubectl debug`. |
| `kubectl debug --copy-to` makes a **copy**. The broken Pod is untouched, and that is the feature. | **No.** Appears in no stem. |
| An ephemeral container cannot be removed or restarted once added, and gets no resource guarantees or probes. | **No.** Appears in no stem. |
| A Service with no endpoints is not broken — it is correct and selecting nothing. Two causes, two files. | **Partly at risk, and permitted.** Q3 tests *one* of the two causes (readiness) as a Ch 5/Ch 9 prior, which Ch 9:766 explicitly handed forward to be "retrieved by name." No stem pairs the two causes or asks the reader to choose between them; that pairing is §4's. Drafting must not let Q3's answer text enumerate both. |
| A working `port-forward` beside a failing Service call does not mean the app is fine — it localizes the fault to the Service layer. | **No.** `port-forward` appears in no stem. Q4 and Q5 test two of the fields it would exonerate, separately, without the diagnostic move. |
| Once you are in application scope, the platform's own signals will keep reporting "fine." That is not reassurance; it is the boundary. | **No.** Q1 tests the Ch 13 boundary test, which is a shipped prior. |

Clean, with one watched edge (Q3). The subtitle names the chapter's *structure*, not a Fixed Point, so unlike Ch 13 there is no subtitle leak to argue about.

**Rubric branches (all three mandatory):** 6+ → skim, but read §3 and §6 properly, since those two carry the material with no analog in Ch 13. 3–5 → normal pace; this chapter is calibrated for you. 0–2 → **re-read Ch 13 §1 before starting**, not alongside — name the section, not the chapter.

---

## 4. Section plan

### `## ⚪ §1 — Handed Back`

Receives the Ch 13 §8 handoff as the chapter's first move, and owns **the four triage questions** that structure everything after it: *is it running, is it healthy, is it reachable, is it configured.* Restates the scope boundary **from the application side only** — Ch 13 §1 owns the boundary and its figure, and this section must not re-derive it. What is new here is the direction of travel and one honest addition: on somebody else's cluster you will often be unable to check the platform side yourself, so the boundary is also a statement about what you have permission to see. Must also close the loop the title opens — "their cluster" is scope, not blame.

The four questions map onto the sections, and the mapping should be stated plainly so the reader can navigate:

| Question | Answered in |
|---|---|
| Is it running? | §2 |
| Is it healthy — and is it configured the way you think? | §3 |
| Is it reachable? | §4, then §5 |
| *(all four, for workloads whose replicas are not interchangeable)* | §6 |

**Note the doubling:** "is it configured" is answered in two places, because a config fault surfaces at two different times — as a Pod that never got past init (§2), and as a value the running process read wrongly (§3). Say this rather than hiding it; a reader who expects four questions and four sections will otherwise count wrong.

- **Objectives:** D3.2 (Troubleshooting Applications — scope), D2.3 (the boundary's far side)
- **Introduces:** application-scope-triage; four-triage-questions; scope-handoff-boundary
- **Figure:** `ch16-fig01-application-scope-triage`
- **Cross-bearings out:** `Ch 13 §1 — whose problem is this, and what to read first`; `Ch 13 §8 — read the phase first`; `Ch 5 §5 — Pod phase and container state`
- **Guardrail — hard.** Three shipped pointers land here with the same words, *"when the Pod is fine and the application isn't"* (Ch 5:676, Ch 13:388, Ch 13:1828). The opening paragraph must actually deliver that sentence's content in its first breath. Do not open with an epigraph gloss or a scene; open by taking the handoff.
- **Guardrail — do not re-teach.** Ch 13 §1 already gave the reader the mechanical test *and* the load-bearing middle clause (a fault that is not confined to one workload is still the platform's). Retrieve both in one paragraph with a pointer. If this section runs longer than Ch 13 §1's treatment of the same boundary, it has taken the wrong turn.
- **Checkpoint:** none

### `## 🔵 §2 — When It Never Got Started`

Owns **init-container debugging from the application side**. Two shipped chapters point here by number and their debts are different, so both must be discharged explicitly: Ch 5:448 promised *the method* for a Pod stuck behind a failing init container, having deliberately taught only the model; Ch 13:566 handed off the application-side half of the same failure after owning the platform-side half. The section's content is therefore: reading the init sequence's state, `kubectl logs -c <init-container>` and why the plain form returns nothing useful, the **ordering** mistakes (an init container that waits for a dependency that is itself waiting on this Pod), the **non-idempotency** mistake (an init container that cannot survive being re-run, which it will be), and **config errors visible at init** — a mounted ConfigMap key that does not exist, a Secret whose value is the wrong shape.

- **Objectives:** D3.2 (Debugging Init Containers)
- **Introduces:** init-container-debugging; init-container-ordering-and-idempotency; config-errors-visible-at-init
- **Figure:** `ch16-fig05-init-sequence-debug-points` — **new, not in the arc stub list**
- **Cross-bearings out:** `Ch 5 §3 — everything that must happen first`; `Ch 5 §4 — restartPolicy and restart backoff`; `Ch 4 §4 — ConfigMaps and Secrets`; `Ch 13 §2 — pods that never start`; `Ch 13 §3 — reading logs from a multi-container Pod`
- **Ledger guardrail:** the init sequence itself is **owned by Ch 5 §3**; `kubectl logs -c` is **owned by Ch 13 §3**. This section owns neither. It owns what you *do* with them, and must refer rather than restate. If drafting finds itself explaining what an init container is, it has crossed a line two chapters back.
- **Boundary guardrail:** an init container that cannot pull its image is Ch 13 §2's, not this section's. The split is the same as everywhere else — the platform failing to start the init container is platform scope; the init container running and doing the wrong thing is here.
- **Checkpoint:** none

### `## 🔵 §3 — Getting Inside, and Adding What Isn't There`

The chapter's densest section and the one with no analog anywhere else in the book. Owns `kubectl exec` and its `-c`; the **distroless problem** — an image with no shell, no package manager, and nothing to exec *into*, which is a hardening win that costs you your debugging surface; **ephemeral containers** and the reason they had to be invented (a Pod's `containers` list is immutable once the Pod exists, so the only way to add a process is a mechanism designed for it); **`kubectl debug`**, its **debug profiles**, and **`--copy-to`**; and **`kubectl debug node/`** for the case where the target is the node rather than the workload. Also owns the application-side half of "is it configured": exec in and read the value the process actually got, which is frequently not the value the manifest appears to set.

- **Objectives:** D3.2 (Debugging Running Pods; `kubectl debug`), D2.3 (B1 lists `exec` and `debug` under Troubleshooting — see the exam_domain note)
- **Introduces:** distroless-image-debugging; ephemeral-containers; debug-profiles; debug-copy-to; debug-node
- **Figure:** `ch16-fig02-ephemeral-container-debug`
- **Cross-bearings out:** `Ch 5 §1 — the Pod as the unit of scheduling`; `Ch 2 §2 — what's inside an image`; `Ch 8 §1 — the grammar of a command`; `Ch 12 §5 — what a Pod may do to its node`; `Ch 12 §6 — three levels, three modes`
- **Debt discharged:** Ch 8:364's verb table says `exec` lives "ahead, in Ch 16." This is that.
- **Debt discharged — the sharp one.** Ch 12:1342 pointed here with a specific claim: *a debug container is a container*, and in a namespace enforcing `restricted`, injecting one with elevated privileges can be **refused by admission**. That is not a footnote; it is the single most likely way a reader's `kubectl debug` fails on somebody else's cluster, and Ch 12 already primed them for it. It must appear as a ⚠ Navigational Hazards or a 🪝 Snag, retrieving Ch 12 §6 rather than re-explaining Pod Security Admission.
- **Guardrail — `--copy-to` is a Fixed Point, not a flag.** The reader's default mental model is that debugging tools modify the thing being debugged. `--copy-to` does not: it builds a copy and leaves the broken Pod exactly as it was, which is what makes it safe on a workload you did not deploy. Teach that as the point and the flag as the implementation.
- **Sourcing guardrail:** the **debug profile names** and the exact ephemeral-container restrictions have both moved across releases. Both must carry `[source:]` tags. See Open Question 4.
- **Checkpoint:** ☆ TYB 1

### `## 🔵 §4 — Is Anything Even Selected`

Owns application-side Service debugging as a **procedure**, against Ch 9 §4's **fact**. Ch 9:766 said so in as many words: *"Chapters 13 and 16 own the troubleshooting workflow, and they will retrieve this by name."* Four break points, and the section's job is to make them separable rather than to list them:

1. **Selector/label mismatch** — the Service's `selector` and the Pod template's `labels` are edited in two different places and drift
2. **Not Ready** — the Pods match, and readiness is holding them out of the slice
3. **`port` vs `targetPort`** — everything selects correctly and the traffic arrives at a closed port
4. **The name** — the DNS name the client is using does not resolve to this Service at all

Commands: `kubectl get endpointslices -l kubernetes.io/service-name=<name>` (the exact form shipped Ch 9 already gave the reader) and `kubectl describe service`.

- **Objectives:** D3.2 (Debugging Services), D2.3
- **Introduces:** service-selector-mismatch; empty-endpointslice-as-symptom; port-versus-targetport; service-dns-name-shape (as a failure mode)
- **Figure:** `ch16-fig04-service-break-points` — **new, not in the arc stub list**
- **Cross-bearings out:** `Ch 9 §4 — the list behind the name`; `Ch 9 §3 — four ways to be reachable`; `Ch 9 §7 — names, and where they resolve`; `Ch 4 §5 — labels and selectors`; `Ch 5 §7 — liveness, readiness, and startup probes`; `Ch 13 §4 — pods that start and then don't stay`
- **Ledger guardrail:** the Service model is **owned by Ch 9** entirely. Do not restate Service types, EndpointSlice mechanics, or DNS record shapes. Ch 9's 🪝 Snag already gave the reader "two different bugs in two different files"; §4 owns the step that tells them *which of the two*, which Ch 9 deliberately withheld.
- **Guardrail — hold to two causes for the empty list.** Shipped Ch 9 states two, sourced. Break points 3 and 4 above are **not** causes of an empty endpoint list — they are causes of a *failed request past a populated one*, and the section must keep that distinction visible or it will teach a wrong signature.
- **Checkpoint:** none

### `## ⚪ §5 — Bypassing the Service on Purpose`

Short, and structurally the chapter's cleverest move. Owns **`kubectl port-forward` as a diagnostic that deliberately skips the Service path**, and the inference that follows: a working port-forward beside a failing Service call proves the application is listening and serving correctly, which *localizes* the fault to the four break points in §4 rather than clearing anything. Also owns what the two paths actually are — client → Service → service proxy → Pod, versus client → API server → kubelet → Pod — because the inference is only sound if the reader can see that the second path shares almost nothing with the first.

- **Objectives:** D3.2, D2.3
- **Introduces:** port-forward-as-diagnostic; service-path-versus-api-path
- **Figure:** `ch16-fig03-portforward-vs-service-path`
- **Cross-bearings out:** `Ch 9 §6 — the component that makes it real`; `Ch 9 §2 — the address that doesn't last`; `Ch 3 §5 — the only door in`; `Ch 13 §1 — whose problem is this`
- **Debt discharged:** Ch 13:390 pinned this section by number and by phrase, having withheld the tool on the explicit grounds that it requires a running container.
- **Guardrail — the trap is the payoff.** The reader's instinct on a successful port-forward is relief ("the app works"). The section exists to convert that into a narrowing step. Frame it as evidence, not as a verdict, and state the negative case too: a port-forward that *also* fails moves the investigation back inside the container, to §3.
- **Guardrail — scope.** `port-forward` as a way to reach a cluster service from a laptop for convenience is real and not this section's subject. One clause acknowledging it, then back to the diagnostic use. Do not let this become a networking section; Ch 9 owns networking.
- **Checkpoint:** ☆ TYB 2

### `## 🟡 §6 — When Each Replica Is Its Own`

Owns **StatefulSet debugging from the application side** — the case where the four questions have to be asked of a *particular* replica rather than of the workload. Three things make it different, and each is a retrieval with a diagnostic turn on it: **ordinal identity** means "the app is broken" is frequently "`web-2` is broken" and the other two are fine, so the first move is to find out which; **the per-replica PVC** means a replica's state travels with it and a bad write survives every restart you try, which is the failure that most looks like a platform fault and is not; and **headless-Service per-Pod DNS names** mean peer discovery between replicas can fail in ways a ClusterIP workload never sees.

- **Objectives:** D3.2 (Debugging StatefulSets)
- **Introduces:** statefulset-application-debugging; per-replica-pvc-debugging; headless-service-dns-names (as a failure mode)
- **Figure:** none, deliberately — see Required figures
- **Cross-bearings out:** `Ch 6 §6 — when Pods are not interchangeable`; `Ch 11 §6 — Pods that are not interchangeable, revisited`; `Ch 9 §5 — when you don't want a single address`; `Ch 11 §2 — the claim and the supply`
- **Debt discharged:** Ch 6:872's unnumbered pointer, *"debugging StatefulSets and their claims."* Unnumbered means the section number is free; the topic is not.
- **Ledger guardrail — three owners, none of them here.** Ordinal identity is Ch 6 §6. `volumeClaimTemplates` and PVC survival are Ch 11 §6. Headless Services are Ch 9 §5. This section owns the *consequences for a person holding a bug report* and nothing else. It is the section most at risk of becoming a StatefulSet recap; if drafting is explaining what a StatefulSet is, stop.
- **Decay-repair note:** Soundings Q7 probes PVC survival precisely so this section can retrieve it rather than re-derive it. If Q7 is where readers fail, that is a signal for the drafting stage, not a licence to re-teach Ch 11.
- **Checkpoint:** none

### `## 🟡 §7 — Before You Ship It`

Owns the **local development and debugging loop**, and the judgment call that goes with it: when reproducing a failure on your own machine is the fastest path, and when the reproduction is worthless because the thing that broke only exists in-cluster. The dividing line is the useful content — anything that depends on cluster-supplied identity, DNS, injected config, admission mutation, or a Service's routing is not reproducible locally by definition, and trying is how an afternoon disappears. Everything else usually is.

- **Objectives:** D3.2 (developing and debugging services locally)
- **Introduces:** local-development-loop; in-cluster-only-reproduction
- **Figure:** none
- **Cross-bearings out:** `Ch 8 §5 — who owns the control plane` (kind, minikube, k3s as local clusters); `Ch 15 §1 — twelve factors, and the ones Kubernetes already solved` (factor III, config in the environment); `Ch 14 §5 — patching instead of templating` (an overlay for a local target)
- **Depth ruling — associate tier, and this is the section most likely to overrun.** Recommendation: own the *decision*, name the pattern (proxy a local process into the cluster so it sees real dependencies), and name at most one tool, source-tagged, as an example of the pattern. Do not teach a toolchain. See Open Question 5.
- **Guardrail:** this section closes the practical arc, so it should end by pointing at §8 rather than at another tool. It is the least exam-weighted section in the chapter and should read as the shortest.
- **Checkpoint:** ☆ TYB 3

### `## ☀️ §8 — Mine, or the Platform's`

Zenith, and the far end of a two-chapter arc. The recognition is that the two chapters were never two subjects: **the boundary is the method.** Chapter 13 taught the reader to read the phase, and the phase's last and most valuable answer is *"this is no longer mine."* Chapter 16 taught four questions, and their real function is not to find the bug — it is to keep narrowing until the bug has nowhere left to be, which is the same move at a different altitude. A practitioner who can place a failure on the right side of that line in ninety seconds is doing the thing that separates them from someone who has read about Kubernetes, and both halves of the arc exist to build that one judgment.

- **Figure:** `ch16-zenith-mine-or-the-platforms`
- **Cross-bearings out:** `Ch 13 §1 — whose problem is this, and what to read first`; `Ch 13 §8 — read the phase first`
- **⛑ CONVENTION guardrail — read before drafting.** State the pattern, never the count. §8 may observe that narrowing-by-elimination is a shape the reader has met before; it **must not** assert an ordinal ("the third time," "the sixth"). Two collisions have already reached shipped text in this book and both had to be repaired at a later gate.
- **Zenith guardrail — do not borrow Ch 15 §7.** Ch 15 §7 is the book's **primary Zenith** and its payoff is the control loop pointed at a repository. This chapter's Zenith is its own and is about scope, not reconciliation. Do not reach for the control loop here; it is one chapter behind and the reader's recognition has just been spent on it.
- **Closing guardrail:** §8 closes Part IV. The Voyage Ahead that follows hands to Ch 17 and Part V — patterns and instruments — not to another delivery chapter.

---

## 5. ☆ Taking Your Bearings checkpoints

Three checkpoints, 16 questions, **4 retrieval questions = exactly 25.0%**, the arc outline's ceiling. This chapter sits *at* the ceiling rather than below it, which is why the count was raised from B4's 10 (see the frontmatter note).

**Retrieval is defined narrowly, and the drafting stage must hold the line.** A retrieval question is one whose *answer* lives in an earlier chapter. A question about diagnosing an empty endpoint list that merely leans on Ch 9's Service model is a **chapter** question, not a retrieval question — otherwise this chapter would score 90% retrieval and the number would mean nothing. Ch 13's outline made the same ruling and it binds identically here.

| # | Falls after | Topic | Qs | Retrieval | Drawn from |
|---|---|---|---|---|---|
| TYB 1 | §3 | Taking the handoff, and getting inside | 6 | 1 | Ch 2 §2 — what an image does and does not contain |
| TYB 2 | §5 | Reachability: what selects, what routes, what proves | 5 | 2 | Ch 9 §3 — `port` and `targetPort`; Ch 5 §7 — readiness |
| TYB 3 | §7 | Identity, storage, and the limits of reproducing it locally | 5 | 1 | Ch 11 §6 — PVC survival across replica rescheduling |

**TYB 2 runs 40% retrieval locally, and that is deliberate.** §4 and §5 are the sections where this chapter's method depends most completely on shipped Ch 9 facts, and this is where the repair gets verified. The chapter average is at the ceiling, which is the number that governs.

Every checkpoint carries trap answers targeting the misconceptions tabulated in the Exam Alert, why-wrong explanations for **all** options, and a revision prompt naming a **section** for 0–2 scorers.

---

## 6. Exam Alert plan

**High-priority topics.** Four, and the first is B1's stated posture for this competency verbatim:

1. **Which verb answers which question.** `logs` for what it said, `exec` for what it can see, `debug` for when there is nothing to exec into, `port-forward` for where the break is, `describe`/`get endpointslices` for whether anything is selected. The exam tests the mapping, not the flags.
2. **Ephemeral containers exist because a Pod's container list is immutable.** That single fact explains the whole tool.
3. **`kubectl debug` has three shapes** — inject into the running Pod, `--copy-to` a copy, and `node/` for the host. Each answers a different question and they are not interchangeable.
4. **An empty endpoint list has two causes** — selector mismatch, or Pods not Ready — and they live in two different files.

**Common traps** — ⚠ Navigational Hazards, loss-aversion framing:

| Trap | The correct understanding |
|---|---|
| Assuming `kubectl exec ... -- sh` works on any container | It requires a shell *in the image*. A minimal or distroless image has none, and that is the whole reason ephemeral containers exist. |
| Expecting `kubectl debug` to repair the broken Pod | It adds a process to look with, or makes a copy to experiment on. It fixes nothing, and an ephemeral container cannot be removed once added. |
| Reading `--copy-to` as "debug the running Pod" | It is the opposite. The original is untouched — which is the point on a workload you did not deploy. |
| Treating a working `port-forward` as proof the application is fine | It proves the application is fine **and** the Service path is not. That is a narrowing step, not a clean bill of health. |
| Confusing `port` with `targetPort` | `targetPort` is the port the container listens on. A mismatch produces a Service that selects perfectly and routes into nothing. |
| Reading an empty EndpointSlice as a broken Service | The Service is correct and selecting nothing. Two different bugs, two different files. |
| Running plain `kubectl logs` on a Pod stuck in init | You get nothing useful. Name the init container with `-c`. |
| Assuming a rescheduled StatefulSet replica comes back with empty storage | The PVC follows the identity. A corrupt write survives every restart you try, which is exactly why it looks like a platform fault. |
| Assuming `kubectl debug` always succeeds if you have RBAC for it | A debug container is a container. Under `restricted` enforcement, admission can refuse it. Ch 12 already warned the reader. |
| Treating D3.2 Debugging as a different subject from D2.3 Troubleshooting | B1 trap #87. The split is *scope*, not tooling — a question tagged to one may test the other's commands. |

---

## 7. Practice Questions plan

**Target: 15**, per `question_budget.practice_questions` and B4, which records 15 as the book's floor and names this chapter and Ch 13 as the two that sit on it.

| Section | Items | Rationale |
|---|---|---|
| §1 scope and the four questions | 2 | The chapter's spine; better tested by scenario stems than by definition recall |
| §2 init containers | 3 | Two inbound pointers and a competency named explicitly in the curriculum |
| §3 exec, ephemeral containers, `kubectl debug` | 4 | The densest section and the one with the most new material in the chapter |
| §4 Service selection | 3 | Four break points, and the confusion the exam can reach most directly |
| §5 `port-forward` | 1 | One section, one clean inference; more would be padding |
| §6 StatefulSet | 1 | Proportionate to an advanced-band section with one inbound pointer |
| §7 local development | 1 | The least exam-weighted section; one item that tests the *decision*, not a tool |

**Interleaving strategy.** At least five stems present a *symptom* and require the reader to choose the next diagnostic step rather than name a command — the shape the exam favors, and the shape a glossary cannot answer. Four stems cross domains deliberately: one pairs a Service that selects nothing with the readiness probe that caused it (D2.1 + D1.1), one pairs a refused debug container with Pod Security Admission (D2.2), one pairs a StatefulSet replica with its surviving PVC (D2.4), and one pairs a config value the process actually read with the ConfigMap that appears to set it (D1.1). Per skill Part 10, wrong options are built to catch the specific misconceptions tabulated above, and every option gets a why-wrong explanation.

**Retrieval-practice items** carry the same 25% ceiling as the Bearings and count separately from them; at least three Practice items should draw their *answer* from Ch 5, Ch 9 or Ch 11.

**Barred from all graded text in this chapter** (per the term ledger's Part 2 rulings, restated so no item quietly adopts one): PodDisruptionBudget (unowned, ⚑3), ABAC, SRE, descheduler, eBPF, and any item hinging on the absence of a Kubernetes LTS. Also barred: `static Pod` and `mirror Pod` may be *used* here only if Ch 13's shipped treatment is cited, since Ch 13's gate ruled they still lack glossary entries.

---

## 8. Required figures

Six anchors: five concept diagrams plus one Zenith, inside skill Part 18.10's 2–8 band.

| Anchor | § | Type | Purpose and content |
|---|---|---|---|
| `ch16-fig01-application-scope-triage` | §1 | Process flow | The four triage questions as a flow, with the **inbound handoff arrow from Ch 13** entering at the top. **Reciprocal-pair constraint:** this figure must visually rhyme with `ch13-fig01-two-audience-split` the way `ch15-zenith` must rhyme with `ch03-fig02` — same two-column vocabulary, arrow reversed, application column now the subject. The recognition is the payoff and it fails if the two figures do not answer each other. ≤7 labels. |
| `ch16-fig05-init-sequence-debug-points` | §2 | Process flow | The init sequence as a timeline with **what to read at each stage** annotated beneath it — not the sequence itself, which Ch 5 §3 owns. Payload is the diagnostic overlay. **New, not in the arc stub list.** |
| `ch16-fig02-ephemeral-container-debug` | §3 | Comparative | Three shapes side by side: ephemeral container injected into the running Pod; `--copy-to` producing a separate copy with the original untouched; `debug node/` attaching to the host. Makes the "which question does each answer" distinction visible. **Relocated from §2 to §3 per B6**, which already ruled on it. ≤7 labels — if three shapes plus annotations breach that, drop `node/` to prose. |
| `ch16-fig04-service-break-points` | §4 | Pipeline | The chain client → DNS name → Service → EndpointSlice → Pod → container port, with the four break points marked on the links they actually break. **Pipeline family, so it carries Lucide glyphs** per style-decisions 2026-08-25. Must visually separate "empty list" (two causes, upstream) from "populated list, request still fails" (two causes, downstream) — that separation is §4's whole argument. **New, not in the arc stub list.** |
| `ch16-fig03-portforward-vs-service-path` | §5 | Comparative / pipeline | Two request paths in parallel: client → Service → service proxy → Pod, versus client → API server → kubelet → Pod. Annotated with what each path proves when it works and when it does not. **Pipeline family, so glyphs**; confirm at the image-specs stage. |
| `ch16-zenith-mine-or-the-platforms` | §8 | Dramatic synthesis | The two chapters' diagnostic paths converging on a single boundary line, with the line itself — not either side — as the visual subject. The claim is that the boundary *is* the method. Exactly one Zenith per content chapter, per Part 18.10. |

**Numbering note, so no downstream stage reads it as an error.** `ch16-fig05` and `ch16-fig04` appear before `ch16-fig02` and `ch16-fig03` in document order. This is deliberate and follows the Ch 13 precedent: the three arc-outline stub IDs (`fig01`, `fig02`, `fig03`) are preserved exactly as stubbed so the join key with `image-specs.md` and the diagram pipeline's `figures-metadata.yaml` stays stable, and the two new figures take the next free numbers. Anchor IDs are identifiers, not an ordering contract; the structural contract's `anchor_id_pattern` imposes no sequence. One arc stub moved section (`fig02`, §2 → §3, per B6's own ruling); two are new (`fig04`, `fig05`); none was dropped.

**Sections without a figure, and why.** §6 gets none because every candidate figure for it — ordinal identity, `volumeClaimTemplates`, headless DNS names — would restate a diagram that Ch 6 §6, Ch 11 §6 or Ch 9 §5 already owns, and Part 18.4's coherence principle forbids a visual that adds nothing. §7 gets none because its content is a judgment call, not a structure. Both are correct at 0.

---

## 9. Open questions for the author

**1. The subtitle breaches this stage's own ≤10-word constraint.** B2 and B3 both carry *"Four questions that separate 'my code is broken' from 'the platform is broken'"* — thirteen words, and the only subtitle in the book over the limit. The frontmatter above adopts an eight-word form, *"Four questions that separate your bug from theirs,"* which keeps the four questions, keeps the scope split, and reads against the title. No shipped chapter quotes the long form. **Recommendation: adopt the short form and update the lineup.** If the author prefers the original, revert the frontmatter and record a documented exception — do not leave the two artifacts disagreeing.

**2. Blocking research — Stage 2 must fetch these before drafting.** B1 flags G1 and G2 as blocking for this chapter, and the cached corpus is thinner here than for any chapter since Ch 13. Of the 243 snapshots on disk, the debugging set is index-level: `k8s-docs-debug-pods-2026-08-31.md` is 21 lines and stops at "take a look at it"; `k8s-docs-debug-overview-2026-08-23.md` is a table of contents; `k8s-docs-troubleshoot-kubectl-2026-08-31.md` self-declares as truncated. **Not one of this chapter's five new tools is documented in the corpus.** Required:

- `kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/` — **the critical one.** `exec`, ephemeral containers, `kubectl debug`, debug profiles, `--copy-to`, `debug node/`. Five of the chapter's Fixed Points live on this page and nowhere else.
- `kubernetes.io/docs/tasks/debug/debug-application/debug-init-containers/` — §2
- `kubernetes.io/docs/tasks/debug/debug-application/debug-service/` — §4
- `kubernetes.io/docs/tasks/debug/debug-application/debug-statefulset/` — §6
- `kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/` — §2, and the D3.2 competency name
- `kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/` — §5
- `kubernetes.io/docs/tasks/debug/debug-cluster/local-debugging/` — §7
- `kubernetes.io/docs/reference/kubectl/generated/kubectl_debug/` — profile names, if the concept page does not pin them
- **Re-fetch** `.../debug-application/debug-pods/` in full. The 08-31 snapshot stops three sentences in, and this chapter needs the "My pod is running but not doing what I told it to do" section, which is §1's and §3's material by name.

**3. §7's depth — recommendation, needs confirmation.** The Kubernetes docs page for local debugging names specific third-party tooling. This is an associate exam and the tooling churns. **Recommendation: own the decision (what is and is not reproducible locally), name the pattern (proxy a local process into the cluster so it sees real dependencies), and name at most one tool, source-tagged, as an instance of the pattern.** Do not teach a toolchain, and do not let this section outgrow §6. Confirm.

**4. Two facts that must not be written from memory.** The **`kubectl debug` profile names** (`legacy`, `general`, `baseline`, `restricted`, `netadmin`, `sysadmin`) and the **ephemeral-container restriction list** (no resources, no probes, no removal, no restart) have both changed across recent releases. Both must carry a `[source:]` tag against a dated snapshot. If the snapshot does not pin the full profile set, name two and describe the shape rather than printing a list that may be incomplete. Same treatment Ch 13 applied to the event TTL and the backoff schedule.

**5. `kubectl debug node/` — in or out?** It is on the `debug-running-pod` page and it is genuinely useful, but it is a *node* operation appearing in an application-scope chapter, which cuts against §1's boundary. **Recommendation: in, at one paragraph, explicitly marked as the moment you step back across the line** — which makes it an argument for the boundary rather than an exception to it. The alternative is to cut it and let Ch 13 §5 own everything node-level. Confirm.

**6. Ch 6:872's pointer is unnumbered, and that is fine.** It reads *"see Ch 16 — debugging StatefulSets and their claims"* with no `§`. §6 discharges it. Recorded so a later stage does not "fix" Ch 6 by inserting a section number that was never wrong to omit — and so nobody moves the StatefulSet material out of §6 on the grounds that nothing pins it there.

**7. Ch 1 remains unaddressable by section number** (B6 Collision #1). Nothing in this chapter needs to point at Ch 1, and nothing should. Restated only so the drafting stage does not invent `Ch 1 §N`.

**8. Acronym-register and glossary additions.** Queue for the glossary build: **distroless** (used throughout §3, currently owned nowhere and absent from the ambient tier — it reaches graded text in this chapter, so it needs a lookup path), **ephemeral container** (owned here at §3, needs a register row), and **`--copy-to`** as a named mechanism. Also still open from earlier gates and not this chapter's to fix: `reverse proxy` (Ch 10), `static Pod` and `mirror Pod` (Ch 13), `crictl` (Ch 13).

**9. One inbound pointer's wording is worth a second look — not a defect.** Ch 12:1342 points at *"Ch 16 §3 — getting inside, and adding what isn't there,"* which matches the B6 section title exactly. Ch 13:390 points at the same section as *"getting inside a container."* Both resolve to §3 and neither is wrong, but the two phrasings differ enough that a reader following both may wonder whether they are the same place. No edit recommended — §3's opening should simply use both phrases in its first paragraph, which costs nothing and closes the question.