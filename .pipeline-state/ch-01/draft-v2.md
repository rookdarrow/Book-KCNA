# Chapter 1: Taking Departure
## *"Ninety minutes, four domains, and a curriculum that moved"*

**Chapter Type: Orientation | Domain Weight: —**
**Complexity: Mixed | Novelty: Moderate | Prerequisites: None**

---

## Attention Budget

**Total time: ~45 minutes | Recommended: Single session**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 7 min | Low | Anytime |
| What the KCNA Is, and Who It's For | 4 min | Low | Anytime |
| Ninety Minutes: The Exam as Published | 5 min | Low | Anytime |
| The Curriculum That Moved Under Everyone's Feet | 10 min | Medium | When alert |
| ☆ Taking Your Bearings: The Exam and the Blueprint | 4 min | Medium | After brief pause |
| The Phrase We Haven't Defined Yet | 2 min | Low | Anytime |
| How This Book Is Built | 5 min | Low | Anytime |
| Three Ways to Read This Book | 3 min | Low | Anytime |
| ☆ Taking Your Bearings: Using the Instruments | 5 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read "The Curriculum That Moved Under Everyone's Feet" and take the first Taking Your Bearings checkpoint. That section is the one piece of this chapter that changes what you do next.*

---

> *"Take your departure while the landmarks are still in sight. The open sea is no place to discover your chart is wrong."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these five questions. They test what you're arriving with, not what this chapter teaches. Every one is answerable from general IT experience, and no score here is a bad score. Your result is a reading instruction, not a verdict.

**1.** A container and a virtual machine both isolate an application from its neighbors. What does a container share with its host that a virtual machine does not?

**2.** Kubernetes is often described as "the thing that runs your containers." Is that accurate? If not, what does Kubernetes actually do, and what runs the containers?

**3.** Who controls the Kubernetes project — a single vendor, a commercial company that licenses it, or an open-source foundation?

**4.** When someone says an application is "cloud native," what do most people take that to mean?

**5.** Have you written Terraform, Ansible playbooks, CloudFormation templates, or anything similar: a file that describes what infrastructure *should* look like, rather than a script that performs steps to build it?

<details>
<summary>Answers + reading strategy</summary>

**1.** The host's **operating system** — that is the documentation's word [source: k8s-docs-overview-2026-08-23]. Practitioners sharpen it: what is actually shared is the host's **kernel**, and this book uses that sharper register where the precision earns its keep. Hold both — the first is the wording to recognize on an answer sheet. *[cross-bearing: see Ch 2 §1 — what a container actually is, and why both registers are correct]*

**2.** Not accurate. Kubernetes is an **orchestrator** — it decides what should run where. A separate **container runtime** on each machine does the work of actually starting the containers [source: k8s-docs-cluster-architecture-2026-08-23]. *[cross-bearing: see Ch 2 §4 — the Container Runtime Interface]*

**3.** An open-source foundation. Kubernetes is hosted by the **Cloud Native Computing Foundation**, which is part of the nonprofit **Linux Foundation** [source: cncf-who-we-are-2026-08-23]. *[cross-bearing: see Ch 17 §2 — CNCF governance and the project lifecycle]*

**4.** Most people take it to mean "runs in a public cloud." That is the near-universal assumption, and it is not what the term means. We'll come back to it in §4 below, and *[cross-bearing: see Ch 17 §1 — the CNCF definition of cloud native]*.

**5.** No right answer here; this one is calibration only, and it isn't scored. If you've written any of those, you already hold a distinction that Chapter 4 will name for you, and you'll move through it fast. If you haven't, Chapter 4 is worth reading slowly. *[cross-bearing: see Ch 4 §1 — declarative versus imperative]*

**Scoring: question 5 isn't scored. Of the four scored questions —**

**3–4 right:** you arrive with the platform priors this book assumes. Read Chapters 2 and 3 at normal pace. The calibration in §6 will point you toward the chapters where your real gaps are. They are probably not where you expect.

**1–2 right:** this is the expected starting point for this credential. Read at normal pace throughout. The book is built for you.

**0 right:** read carefully, and give Chapters 2 and 3 a session of their own. Nothing here is beyond you. The vocabulary is new, that's all, and this book introduces every term before it uses it.

</details>

---

## ⚪ What the KCNA Is, and Who It's For

Here is a question worth carrying for the next few pages: **why does so much of the KCNA study material online describe a different exam than the one you are going to sit?**

Not a slightly different exam. A structurally different one: a different number of domains, different weights, and one whole domain that no longer exists. The material isn't fraudulent and its authors aren't careless. Something moved underneath them, and much of it hasn't caught up. Section 3 has the details. By the end of this chapter you'll be able to spot a stale guide yourself, in about fifteen seconds of skimming.

First, the credential itself.

The **Kubernetes and Cloud Native Associate**, the KCNA, is the usual entry point to the cloud native certification family. The Linux Foundation, which publishes the exam, describes it as demonstrating "a user's foundational knowledge and skills in Kubernetes and the wider cloud native ecosystem" [source: lf-kcna-exam-page-2026-08-23]. It is a CNCF credential, and CNCF is part of the nonprofit Linux Foundation [source: cncf-who-we-are-2026-08-23]. Experience level: beginner. Prerequisites: none [source: lf-kcna-exam-page-2026-08-23].

Take "no prerequisites" literally. No required course. No logged hours. No prior certification, no attestation of experience, no manager's signature. If you can pay the fee and stay awake for ninety minutes, you can sit it. That's unusual in this industry, and it fits what the credential is for: it gives people a defensible way to say *I understand how this world is put together* before they've had a job that let them prove it.

It is a **multiple-choice, online, proctored exam** [source: lf-kcna-exam-page-2026-08-23]. That matters more than it sounds, and it's the first place people misjudge this credential.

The hands-on Kubernetes certifications, the ones that drop you into a live terminal with a broken cluster and a running clock, measure whether you can *do* the thing [source: lf-cloud-native-certification-catalog-2026-08-23]. The KCNA measures whether you can *discriminate*. Given several plausible-sounding statements about how the scheduler decides where a Pod goes, can you identify the one that's true? Given a symptom, can you name the layer where the problem lives? That is a genuinely different skill, and it is not a lesser one. Practitioners who can execute a command from muscle memory but can't say why it works are everywhere, and they're the ones who stall at three in the morning when the situation stops matching the runbook.

> ⚓ **Worth Securing:** A conceptual exam deserves a conceptual study method. The instinct to "just get hands on a cluster and practice" is a good instinct for CKA and a partially misdirected one here. Hands-on time helps, because it makes abstractions concrete, but you will not pass this exam by drilling `kubectl` commands, and you can fail it while typing them fluently. Study for discrimination: for every concept, ask "what is the thing this is most often confused with, and what's the difference?"

Let me be direct about what this book is not. It is **not a kubectl drill book.** There are commands in it, because you cannot understand a Service without seeing how one is described, but the commands are here to illuminate concepts, not to build reflexes. When you want the reflexes, and if you stay in this field you will, the Certified Kubernetes Administrator is the next voyage: a genuinely hands-on exam taken in a live terminal [source: lf-cloud-native-certification-catalog-2026-08-23]. Lodestar Ledgers publishes a guide for that one too.

The wider certification family — the other associate-level exams, the specialist tracks, how they relate to one another — belongs in Chapter 17, alongside the ecosystem material it's part of. *[cross-bearing: see Ch 17 §4 — the cloud native certification landscape]*

---

## ⚪ Ninety Minutes: The Exam as Published

Everything in this section comes from the Linux Foundation's own exam page. Where the page is silent, I'll say so. That silence turns out to be one of the more useful facts in the chapter.

> **Dead Reckoning:** The KCNA is an online, proctored, multiple-choice exam. Duration is 90 minutes. There are no prerequisites. Registration includes a 12-month eligibility window in which to schedule and sit the exam, two exam attempts, and an exam preparation handbook. The certification is valid for two years. Pricing at the time this book's sources were captured (2026-08-23): $250 for the exam alone; $299 for the exam bundled with the LFS250 course; $495 for the exam bundled with the THRIVE-ONE annual subscription [source: lf-kcna-exam-page-2026-08-23].

Two of those facts deserve a moment.

**Two attempts are included.** Not a consolation prize. A structural feature. The second attempt is part of what you bought. This is not permission to sit the first one unprepared, but it does mean the catastrophe you may be quietly bracing for isn't on the menu: failing once costs you time and morale, not money. Adjust your anxiety accordingly.

**Two years of validity.** Cloud native tooling moves fast enough that a five-year credential would be a fiction. Two years is honest. Plan for it.

> 🔭 **Closer Look:** Prices and bundles are the most volatile facts in this section and the least load-bearing for your studying. The figures above are as of 2026-08-23. Check the exam page before you buy; if the number has moved, nothing else in this book changes.

Now a disclosure most study guides skip.

**The two numbers everyone quotes have different provenance.** The passing score *is* published: the Linux Foundation's candidate FAQ for its multiple-choice exams states that a score of 75% or above must be earned to pass [source: lf-mc-exam-faq-2026-08-23] — it just isn't on the exam page most candidates read, which states the format, the duration, the eligibility terms, the price, and the domain weights and stops there [source: lf-kcna-exam-page-2026-08-23]. The question count is published nowhere: not on the exam page, not in the FAQ, not in the CNCF curriculum.

You will nonetheless see "60 questions, 75% to pass" repeated across study sites, videos, and forum threads, stated flatly, as one fact. It is two facts with two pedigrees: a passing standard the certifying body publishes, and a question count that travels on repetition alone.


> ⚠ **Navigational Hazards**
>
> The hazard here is not the exam. It's the habit of treating a widely-repeated number as a published one.
>
> A study plan built on "60 questions in 90 minutes" yields a pacing rule of 90 seconds per question, and that rule feels precise and authoritative. If the real count is different, the rule is wrong, and you find that out at minute forty of a ninety-minute exam, with a proctor watching and no way to reset.
>
> The correction costs nothing: pace by *proportion of elapsed time*, not by question number. "A quarter of the way through the questions when a quarter of my time is gone" survives any question count. "Question 15 at the 22-minute mark" does not.

This book flags that distinction every time either figure appears, including in Chapter 20, whose full-length mock exam is sized to the commonly-reported format. That mock is a calibrated practice exam, built deliberately at the size the community reports, and it is framed as such. It is not a claim about what the real exam contains. *[cross-bearing: see Ch 20 §1 — how the mock exam is sized, and why]* Exam-day pacing gets its own treatment once you have content to pace through. *[cross-bearing: see Ch 19 §3 — pacing and time discipline]*

There's a broader habit here, and it's worth naming: **know which of your facts are published and which are inherited.** That distinction outlasts this exam. It's the same instinct that stops you quoting a Stack Overflow answer as documentation.

---

## 🔵 The Curriculum That Moved Under Everyone's Feet

Here's the answer to the question I opened with.

The KCNA exam blueprint was restructured, effective no earlier than **November 24, 2025** [source: lf-kcna-program-changes-2026-08-23]. Five domains became four. Weights shifted substantially. And the domain that disappeared didn't shrink. It was absorbed.

These are the four domains and weights you are being examined against:

**★ Fixed Point**

**The current KCNA blueprint is four domains: Kubernetes Fundamentals 44%, Container Orchestration 28%, Cloud Native Application Delivery 16%, Cloud Native Architecture 12%** [source: lf-kcna-exam-page-2026-08-23]**.**

If you memorize one thing from this chapter, memorize those four numbers. They are the index to everything else. Every study decision you make from here should be checkable against them.

Their named competencies:

| Domain | Weight | Competencies |
|---|---|---|
| Kubernetes Fundamentals | 44% | Kubernetes Core Concepts; Administration; Scheduling; Containerization |
| Container Orchestration | 28% | Networking; Security; Troubleshooting; Storage |
| Cloud Native Application Delivery | 16% | Application Delivery; Debugging |
| Cloud Native Architecture | 12% | Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration |

[source: lf-kcna-exam-page-2026-08-23] [source: cncf-kcna-curriculum-pdf-2026-08-23]

And here is what they replaced. The retired blueprint had five domains: Kubernetes Fundamentals 46%, Container Orchestration 22%, Cloud Native Architecture 16%, **Cloud Native Observability 8%**, and Cloud Native Application Delivery 8% [source: lf-kcna-program-changes-2026-08-23].

<!-- AUTHOR-REVIEW: Contested provenance for the five retired weights (46/22/16/8/8), and for everything derived from them below — ch01-fig01's left column, the −2/+6/×2 annotations, the "under-serve Application Delivery by roughly half" test, the 🪝 Snag on 16→12, and the Logbook Entry's premise. The fact-accuracy audit verified these against the cached snapshot lf-kcna-program-changes-2026-08-23, where they appear verbatim. The curriculum-alignment audit reports that snapshot is stale — that the research stage found the retired percentages were never on the LF page, cached a correction, and could not write it to sources/. Both cannot be right. Resolve by (a) retrieving the retired curriculum PDF from cncf/curriculum/old-versions/ and caching it as cncf-kcna-curriculum-retired-2026-08-23.md, or (b) if that fails, cutting all five percentages and respec'ing ch01-fig01 as a one-sided "what moved" diagram. The structural claim — five domains became four, observability folded into Architecture — is independently sourced and survives either way. Do NOT source the weights from the CNCF-hosted Medium repost; that is a syndicated guest post, the exact diffusion mechanism §2 teaches readers to catch. -->

<!-- FIGURE: ch01-fig01-blueprint-change-2025 -->
```
     RETIRED (five domains)                  CURRENT (four domains)
     ─────────────────────────               ──────────────────────────

     Kubernetes Fundamentals    46%  ──────► Kubernetes Fundamentals    44%   (−2)

     Container Orchestration    22%  ──────► Container Orchestration    28%   (+6)

     Cloud Native App Delivery   8%  ──────► Cloud Native App Delivery  16%   (×2)

     Cloud Native Architecture  16%  ──┐
                                       ├───► Cloud Native Architecture  12%
     Cloud Native Observability  8%  ──┘        (Observability folded in
                                                 as a competency, not a
          [domain no longer exists]              standalone domain)
```

*The 2025 KCNA blueprint restructure. Two movements matter most: Application Delivery doubled, and Observability stopped being a domain of its own.*

Three things changed in ways that should change your behavior.

**Cloud Native Observability is gone as a standalone domain.** Observability did not stop being tested. It was folded in as a competency under Cloud Native Architecture, alongside Ecosystem and Principles and Community and Collaboration [source: lf-kcna-program-changes-2026-08-23]. Prometheus, OpenTelemetry, the difference between metrics and traces: all still fair game. But the 8% once reserved for observability alone now shares a 12% domain with two other competencies. If you were planning to spend a fifth of your study time on Prometheus, that plan came off the old chart. *[cross-bearing: see Ch 18 §1 — observability under the current blueprint]*

**Cloud Native Application Delivery doubled**, from 8% to 16% [source: lf-kcna-program-changes-2026-08-23]. That is the largest proportional change among the domains that survived the restructure, and material built for the old blueprint will under-serve it by roughly half — a topic budgeted for 8% of an exam doesn't retroactively grow when the weight moves. GitOps, Helm, deployment strategies, debugging deployed applications: this is now one exam question in six. *[cross-bearing: see Ch 14–16 — the Application Delivery domain in full]*

**Container Orchestration rose six points**, from 22% to 28% [source: lf-kcna-program-changes-2026-08-23]. Networking, security, troubleshooting, and storage together now account for more than a quarter of the exam.

Kubernetes Fundamentals eased slightly, 46% to 44% [source: lf-kcna-program-changes-2026-08-23], a rounding-level change that shouldn't move anything in your plan. It remains, by a wide margin, the largest domain.

<!-- AUTHOR-REVIEW: The curriculum-alignment audit recovered a reader-facing consequence this section should carry and currently doesn't — that the only date which determines which blueprint you are examined against is the date you SIT the exam (not the purchase date, not first-attempt-versus-retake). That claim is not present in any cached snapshot on disk. Add it here with a citation once the corrected lf-kcna-program-changes snapshot lands; do not add it unsourced. -->

> 🪝 **Snag:** "Cloud Native Architecture" appears in both blueprints at different weights, 16% before and 12% now, but it isn't the same domain in a smaller hat. It *gained* observability while *losing* weight, so the material it does cover is compressed harder than the number alone suggests. Don't reason about it by comparing 16 to 12.

Now the practical use of all this.

You are going to encounter other study material. Videos, blog posts, practice question sets, competing books, a colleague's notes from when they passed. Some of it is excellent. Here is how to check whether it describes your exam, in about fifteen seconds:

**Count the domains.** If the material is organized around **five** domains, or carries a standalone chapter or section titled "Cloud Native Observability" presented as a domain in its own right, it was built for the retired blueprint. That doesn't make its facts wrong; a Pod worked the same way in 2024. But its *weighting* is wrong, which makes its emphasis wrong, which makes its practice sets wrong, which makes the picture it hands you of where the exam's mass sits wrong. Specifically, it will under-serve Application Delivery by roughly half.

Use it for facts if you like. Don't use it to allocate your time.

> 🪢 **Mnemonic:** The weights descend: 44 · 28 · 16 · 12. Four numbers, each smaller than the last, no ties to confuse. If you want a hook, **44 and 28 together make 72%**. Kubernetes itself and its orchestration mechanics are nearly three-quarters of the exam. The remaining 28% is everything *around* Kubernetes: how you deliver to it, and the ecosystem it lives in.

One disclosure, made here where it's checkable: **the CNCF publishes weights at the domain level only.** There is no published per-competency or per-topic weighting [source: lf-kcna-exam-page-2026-08-23] [source: cncf-kcna-curriculum-pdf-2026-08-23]. Where this book assigns emphasis *within* a domain, meaning how many chapters a competency gets and how much depth each receives, that is authored judgment, derived from concept count and prerequisite load rather than from a published number. Section 5 says more about how that judgment maps to chapters.

---

## ☆ Taking Your Bearings: The Exam and the Blueprint

Three questions. They test discrimination, which is the skill the whole exam is built on, so treat this checkpoint as a preview of the format as well as a check on the section.

---

**1.** Under the current KCNA blueprint, where does observability live?

A) It is its own domain, Cloud Native Observability, weighted 8%
B) It is a competency under Cloud Native Architecture
C) It is a competency under Container Orchestration, alongside Troubleshooting
D) It was removed from the exam entirely in the 2025 restructure

---

**2.** Which of the following does the Linux Foundation's KCNA exam page state?

A) The number of questions on the exam
B) The score you need to earn to pass
C) The weight of each of the four domains
D) The number of study hours recommended before sitting

---

**3.** You have limited study time and want to allocate it well. Which statement best describes how to use the domain weights?

A) Spend time in proportion to the number of chapters each domain has in this book, since chapter count reflects difficulty
B) Spend the most time on Kubernetes Fundamentals (44%), then adjust for which competencies you personally find hardest
C) Split time evenly across the four domains, since every domain contains questions
D) Prioritize Cloud Native Application Delivery, since it doubled in the 2025 restructure

---

**Answers with Explanations**

**1 — B.** Observability is a competency under **Cloud Native Architecture** in the current four-domain blueprint [source: lf-kcna-program-changes-2026-08-23].

- **A is wrong**, and it's the trap that matters. Cloud Native Observability *was* a standalone 8% domain, in the blueprint retired in the 2025 restructure. If you picked A, you may be studying from the retired blueprint, or thinking in its terms. That's the whole point of §3.
- **C is wrong.** Container Orchestration's four competencies are Networking, Security, Troubleshooting, and Storage. Troubleshooting and observability are related in practice, but the blueprint catalogues them separately.
- **D is wrong.** Nothing was removed. It was reorganized. Observability content is still examinable; it simply shares a smaller domain now.

**2 — C.** The **four domain weights** (44 / 28 / 16 / 12) are stated on the exam page, and they're the most useful published fact you have [source: lf-kcna-exam-page-2026-08-23].

- **A is wrong.** The question count is not on the exam page — or anywhere else the certifying body writes. "60 questions" is a third-party report, repeated so consistently that it reads as official. It isn't.
- **B is wrong**, for a subtler reason than A. The 75% passing score *is* published by the Linux Foundation — in its candidate FAQ for multiple-choice exams, not on the exam page the question asks about [source: lf-mc-exam-faq-2026-08-23]. Keep the two straight: the passing standard is official; the question count is not.
- **D is wrong.** No study-hour recommendation appears anywhere on the page. Certifying bodies rarely prescribe preparation time, for the obvious reason that it depends entirely on what the candidate walks in carrying.

Believing the inherited numbers isn't dangerous; *building a strategy on them* is. Answer every question, pace by elapsed time rather than by question number, and neither figure is one you need.

**3 — B.** Weight-proportional first, personal-weakness-adjusted second. Kubernetes Fundamentals is 44% of the exam, nearly half, and no allocation that under-serves it can be right.

- **A is wrong.** Chapter count tracks *how much explaining a topic needs*, not *how many questions it generates*. Those correlate loosely at best. This book's chapter allocation deviates from the published domain weights by at most 2.8 percentage points, deliberately, and §5 says so out loud. Where the two disagree, the exam weights win. They're the published number.
- **C is wrong.** An even split sounds fair and is simply inaccurate. It gives Cloud Native Architecture (12%) more than twice the attention its share of the exam warrants, and starves Kubernetes Fundamentals (44%).
- **D is wrong**, and it's the trap §3 sets by accident. A domain that doubled from a small base is still small. Growth rate is not exam share: Application Delivery moved from 8% to 16%, which makes it the fastest-growing domain and still the second-smallest one. Sixteen does not outrank forty-four.

---

**Checkpoint: You've Now Mastered**

✓ The four current domains and their weights — 44 / 28 / 16 / 12
✓ What the 2025 restructure changed, and which topic moved most
✓ How to tell, in seconds, whether a study resource targets your exam
✓ The difference between an exam fact that's published and one that's inherited

That last one is a habit rather than a fact, and it's the most portable thing in this chapter.

---

## ⚪ The Phrase We Haven't Defined Yet

You've read "cloud native" perhaps a dozen times by now. It's in the credential's name. It's in two of the four domain names. And I haven't defined it.

That's deliberate, and I'd rather tell you than have you wonder.

"Cloud native" is doing real technical work in those names. It is not decoration and it is not a synonym for "modern." It names a specific set of characteristics that a system either has or doesn't. And critically, **it does not mean "runs in a public cloud."** The CNCF's own definition covers workloads deployed across public, private, and hybrid environments [source: cncf-cloud-native-definition-2026-08-23]. That's a common assumption on arrival, it's the one the Soundings tested, and it will actively obstruct you if you carry it into Chapter 17. A rack of hardware in your own building can be thoroughly cloud native, and renting cloud instances does not by itself make a system cloud native.

The CNCF maintains a published definition with named characteristics — the Cloud Native Definition, currently at version 1.1 [source: cncf-cloud-native-definition-2026-08-23]. You will get it in full in Chapter 17: the actual document, unabridged, each characteristic examined. *[cross-bearing: see Ch 17 §1 — the CNCF cloud native definition and its characteristics]*

Why wait four hundred pages for a definition I could give you in a paragraph? Because those are two different experiences of the same sentence. Read on page ten, the definition is vocabulary: a string of adjectives you'd nod at and forget by Tuesday. Read in Chapter 17, after you have met containers, orchestration, declarative APIs, services, and delivery pipelines in person, every clause lands as a description of something you now recognize. The definition stops being a thing to memorize and becomes a summary of what you already know.

So Chapter 1 leaves you with the question rather than the answer. Hold it open. It's the only thing this book asks you to carry that far.

> **Extended Analogy:** You have been handed a chart whose legend is printed on the last page.
>
> That sounds like an error, and for most charts it would be. But this one is drawn for someone who will be sailing the water it depicts. The symbols on it, the marks for depth and hazard and anchorage, mean very little to a reader who has never seen the seabed they describe. Shown the legend first, you'd memorize that a certain mark means "rocky bottom, poor holding," and you'd have learned a fact.
>
> Sail the water first. Anchor once on rocky bottom and spend a night listening to the cable grind. Then turn to the legend, and the mark doesn't teach you anything. It *names* something your hands already know. That's what this book is trading four hundred pages for.

---

## ⚪ How This Book Is Built

The instrument panel. Six Parts, twenty chapters.

<!-- FIGURE: ch01-fig02-book-map-parts-to-domains -->
```
  PART                              CHAPTERS    EXAM DOMAIN                         WEIGHT
  ──────────────────────────────────────────────────────────────────────────────────────────
  I    Taking Departure             Ch 1        (none — orientation)                   —
  II   Ship, Cargo, and Company     Ch 2–8      Kubernetes Fundamentals               44%
  III  Underway                     Ch 9–13     Container Orchestration               28%
  IV   Dispatches                   Ch 14–16    Cloud Native Application Delivery     16%
  V    The Wider Sea                Ch 17–18    Cloud Native Architecture             12%
  VI   Making Port                  Ch 19–20    (synthesis + mock exam)                —
```

*Where you are in the book is where you are in the blueprint. Parts II through V correspond one-to-one with the four domains.*

Parts II through V map one-to-one onto the four exam domains. That isn't a coincidence of organization; it's the point. "I've finished Part III" and "I've covered the Container Orchestration domain" are the same statement, so your progress through the book reads as progress through the blueprint with no translation needed.

**The disclosure I promised in §3, placed where you can check it against the map above:** the per-chapter emphasis in this book, meaning how many chapters a domain gets and how much depth each competency receives, is authored judgment. The CNCF publishes weights at the domain level only [source: lf-kcna-exam-page-2026-08-23]. Across the seventeen content chapters, the largest divergence between a Part's share of chapters and its domain's share of the exam is **2.8 percentage points** — Part II holds seven of seventeen chapters, or 41.2%, against Kubernetes Fundamentals' 44%. The other three Parts land within 1.6 points of their domains. Where chapter allocation and exam weight diverge, it's because some concepts take more pages to explain than their exam share would suggest, and some take fewer. The exam weights are the published fact. The chapter distribution is my best reading of what it takes to get you there. Where the two disagree, trust the weights.

### The markers

You'll meet these throughout. Each one signals a specific kind of content so you can decide, at a glance, whether to slow down or move on.

| Marker | Name | What it signals |
|---|---|---|
| 🧭 | Soundings | Pre-chapter self-test; calibrates your reading pace |
| ☆ | Taking Your Bearings | Post-reading checkpoint; verifies comprehension |
| ★ | Fixed Point | Must-memorize. If you retain one thing, this |
| ⚠ | Navigational Hazards | A common mistake or exam trap, treated at length |
| — | Dead Reckoning | Facts only. No metaphor, no framing |
| 🏆 | Safe Harbor | Chapter complete |
| ☀️ | Zenith | The moment separate concepts connect |
| 🗺️→🌊→🌅 | Voyage Progress | Chart → Passage → Dawn: how far the voyage stands |

Four smaller glyphs appear inline, mid-prose, as short asides:

| Glyph | Name | What it signals |
|---|---|---|
| ⚓ | Worth Securing | A practitioner's tip worth anchoring |
| 🪝 | Snag | A specific, common slip — briefer and narrower than ⚠ |
| 🔭 | Closer Look | Deeper than the exam requires; optional |
| 🪢 | Mnemonic | A memory hook |

Two sidebar types run longer: **Logbook Entry** (a story from practice) and **Extended Analogy** (a metaphor developed at length). Both are opt-in depth; you can skip either without losing the thread.

And throughout, you'll see italic bracketed pointers like *[cross-bearing: see Ch 6 §3 — StatefulSets and stable identity]*. These are cross-bearings: forward and back references to where a concept gets its full treatment. Follow them or don't; they're there so you're never stuck wondering "did the book cover this?"

Difficulty is marked on section headings: ⚪ Foundation, 🔵 Standard, 🟡 Advanced, 🔴 Expert.

### Two mechanisms that look like padding and aren't

<!-- AUTHOR-REVIEW: The two paragraphs below make learning-science claims — the pretesting effect and the testing/spacing effect — and the second explicitly appeals to external research ("a well-established effect"). No cached source covers learning science; this cannot be verified from the current source set. This chapter spends §2 teaching readers to distinguish published facts from inherited ones, then makes an unsourced appeal to research two sections later, so this gap is worth closing rather than waiving. Open a BOOK-LEVEL research gap (both mechanisms are book-wide, so cache once rather than per chapter): Roediger & Karpicke (2006) on the testing effect; Richland, Kornell & Kao (2009) on pretesting; Bjork on desirable difficulties. Tag both paragraphs here and the QC2.2 explanation below. If the gap will not be filled, downgrade "That's a well-established effect" to authorial framing so it stops claiming external authority. -->

**The Soundings at the start of each chapter.** These are not quizzes. Nothing is scored, recorded, or held against you. They exist for two reasons. Pre-testing improves subsequent learning even when you get the answers wrong, because attempting a question primes you to notice its answer when you meet it. And a score gives you something more useful than a grade: a reading instruction. High score, skim. Low score, slow down. Skipping them to save six minutes costs you more than six minutes.

**Later chapters will test earlier chapters' material.** Chapter 13's checkpoint will ask you something from Chapter 8. This is going to feel, the first few times, like the book forgot it already covered that. It didn't. Retrieving a fact after you've had time to partly forget it strengthens the memory far more than rereading it would. That's a well-established effect and the single highest-leverage thing this book does structurally. When you hit one of those questions and think *we did this already*, that thought is the mechanism working. Answer it anyway.

### The book-level artifacts

Three things ship alongside the chapters:

- **`the-lodestar.md`** — a single page holding the exam-critical facts, distinctions, and traps, distilled from the whole book. It's the last thing to read before the exam. Chapter 19 walks you through using it. *[cross-bearing: see Ch 19 §5 — using The Lodestar]*
- **The glossary** — every term this book introduces, defined, with the chapter that introduces it.
- **The mock exam** — Chapter 20. A full-length, timed practice exam with worked answers. *[cross-bearing: see Ch 20 — full mock exam]*

---

## ⚪ Three Ways to Read This Book

You now have a Soundings score. Use it.

**If you have no Kubernetes exposure at all:** read linearly, start to finish, no skipping. Give Chapter 2 and Chapter 3 a study session each rather than folding them into a longer sitting. They carry the conceptual load everything else rests on, and rushing them is a false economy that shows up six chapters later as a vague sense that nothing is quite landing. Take every Soundings. Yours are the scores that will move most, and watching them move is worth something.

**If you come from operations and are new to Kubernetes specifically:** read linearly, but check your Chapter 2 Soundings score first. Scored well on the container questions? Chapter 2's container-fundamentals material is skimmable, and you should skim it. Chapter 3 onward is where your new material starts. Your likely blind spots are the parts of the ecosystem that aren't infrastructure: Part IV's delivery tooling, and Chapter 17's ecosystem and community material.

**If you're a developer who has deployed to a cluster someone else runs:** read this paragraph twice. Chapters 2, 4, 5, and 6 will feel familiar. They are not as familiar as they feel. You have working knowledge of the objects you touch daily, which is not the same as the complete model the exam tests, and confident partial knowledge is harder to correct than no knowledge at all. Your reliable gaps are Chapter 8, Chapter 12, and Chapter 17. Of those, Chapter 17's community and collaboration material is, in my experience, what technically strong candidates skip most often. It looks like soft content next to the technical chapters. It is examinable content in a 12% domain, it is easy to learn, and skipping it is the most avoidable way to lose points on this exam. *[cross-bearing: see Ch 8, Ch 12, and Ch 17 — the three chapters this reader most often needs]*

> 🪝 **Snag:** Your Soundings score is a reading strategy, not a verdict. A 1/8 on Chapter 9's Soundings means "read Chapter 9 carefully" and nothing else. It is not a prediction about the exam, and it is certainly not information about you.

**On study time**, honestly rather than promotionally: this is a beginner-level, ninety-minute, conceptual exam. For someone with general IT literacy and no Kubernetes exposure, a few weeks of consistent evening study is a realistic frame. For someone already working around clusters, considerably less. Anyone quoting you a precise number ("Pass in 14 days!") is guessing, however confidently, because the number depends entirely on what you walk in carrying. What I can tell you is that the material is finite and well-bounded. This is not a credential you grind. It's one you understand.

> **Logbook Entry:** Picture a candidate who sits the KCNA this year having studied hard from a course recorded in 2024.
>
> They'd done everything right by their own lights: worked through the whole course, drilled the practice sets, built a mental map of the exam. That map had five domains on it. It had a standalone observability domain worth 8%, and they had studied Prometheus with the thoroughness an 8% standalone domain deserves. They knew the exporters. They knew the scrape model. They could talk about PromQL at a whiteboard.
>
> They passed. A conceptual exam is forgiving of a misallocated study plan when the underlying facts are sound. But they described the first ten minutes as recalibration, question by question, as it dawned on them that the exam's mass was not where they'd been told it was. Application Delivery kept coming up. They had given it the attention appropriate to 8% of an exam, and it is 16%.
>
> Ten minutes of a ninety-minute exam spent recalibrating is over a tenth of your time, and it goes at exactly the moment your composure matters most. That is what §3 of this chapter is for.

---

## ☆ Taking Your Bearings: Using the Instruments

Three questions. Two are about method rather than content, because the habits they describe determine whether the next nineteen chapters work. The third checks the one claim this chapter asks you to carry forward.

---

**1.** You take the Soundings at the start of Chapter 9 and score 1 out of 8. What should you do?

A) Reread Chapter 1, since a low score means you've missed something foundational
B) Skip Chapter 9's Soundings answers and come back to them after reading the chapter
C) Read Chapter 9 carefully and slowly, giving it more time than a chapter you scored well on
D) Read Chapter 9 at normal pace — a Soundings score reflects only what you knew beforehand, so it says nothing about how to read the chapter

---

**2.** Chapter 13's Taking Your Bearings checkpoint includes a question about material from Chapter 8. Why?

A) The book is repetitive; the editors didn't catch the duplication
B) Retrieving material after partly forgetting it strengthens memory more than rereading does
C) Chapter 13 requires Chapter 8 as an immediate prerequisite, so it's checking you're ready
D) It fills out the question count to meet a target

---

**3.** Your company runs Kubernetes on hardware in its own building, with no public-cloud footprint anywhere in the stack. Can that platform be described as cloud native?

A) No — "cloud native" requires running in a public cloud
B) No, unless it consumes at least some managed cloud services
C) Yes — "cloud native" describes how a system is built and operated, not where it runs
D) Only if the same workloads also run with a second provider

---

**Answers with Explanations**

**1 — C.** A Soundings score is a pacing instruction for the chapter *ahead*. Low score means slow down, take it in a dedicated session, don't skim.

- **A is wrong**, and it's the trap. A low Soundings score is not a signal that you failed to absorb something earlier. The questions test *priors you brought with you*, not material the book has taught. Chapter 9's Soundings measures what you knew about Chapter 9's subject before opening it. Rereading Chapter 1 would tell you nothing.
- **B is wrong.** The answers are part of the instrument. They're where the reading-strategy rubric lives, and several of them carry cross-bearings pointing at where the material is covered. Reading them costs a minute and shapes how you read the chapter.
- **D is wrong**, and its first half is right, which is what makes it tempting. The score genuinely says nothing about your ability. But it says a great deal about the gap between what you brought and what the chapter assumes — and that gap is exactly a pacing instruction. Discarding the score because it isn't a verdict throws away the only thing it was ever for.

**2 — B.** Retrieval practice. Recalling something after a delay, once you've partly forgotten it, builds a substantially more durable memory than rereading the same passage would. Spacing those retrievals across chapters is what makes the material stick past exam day.

- **A is wrong**, and this is the reflex worth inoculating against right now. When a later checkpoint asks about earlier material, it will feel like repetition. It isn't. It's the one structural feature of this book most likely to be skipped by readers trying to be efficient, and skipping it costs the most.
- **C is wrong.** Retrieval questions are scheduled by *spacing interval*, not by prerequisite relationship. Chapter 13 does not necessarily depend on Chapter 8; the question appears there because enough time has passed for the retrieval to be worth something.
- **D is wrong.** Question counts in this book are budgeted per chapter, but no question exists solely to fill a slot. Retrieval questions are chosen for what they reinforce.

**3 — C.** "Cloud native" describes characteristics of how a system is built and operated. The CNCF's definition explicitly spans public, private, and hybrid environments [source: cncf-cloud-native-definition-2026-08-23], so owning the hardware disqualifies nothing.

- **A is wrong**, and it's a common assumption on arrival — the one the Soundings tested and §4 exists to dislodge. The phrase contains the word "cloud," which does most of the misleading on its own.
- **B is wrong.** This is the halfway version of the same error: conceding that location isn't the test, then smuggling it back in as "well, *some* cloud services, surely." Managed services are one way to build such a system. They are not in the definition.
- **D is wrong.** Multi-cloud is a deployment choice an organization makes for its own reasons. It appears nowhere in the definition, and a single-site platform is not disqualified by it.

The positive half of this — what the characteristics actually are — is Chapter 17's, and it's worth the wait. *[cross-bearing: see Ch 17 §1 — the CNCF cloud native definition and its characteristics]*

---

**Checkpoint: You've Now Mastered**

✓ What a Soundings score means and what to do with it
✓ Why later chapters test earlier material — and why to answer those questions rather than skip them
✓ Which reading path fits your starting point
✓ That "cloud native" is a statement about how a system is built, not about where it runs

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| What the KCNA is | Beginner-level, no prerequisites, multiple-choice, online and proctored — a test of discrimination, not of typing speed |
| Published exam facts | 90 minutes · no prerequisites · 12-month eligibility window · 2 attempts included · valid 2 years · $250 exam-only as of 2026-08-23 |
| Not on the exam page | The question count (published nowhere) and the passing score (75% — published in the Linux Foundation's candidate FAQ, not on the exam page) |
| The four domains | **44 / 28 / 16 / 12** — Kubernetes Fundamentals · Container Orchestration · Cloud Native Application Delivery · Cloud Native Architecture |
| The 2025 restructure | Effective no earlier than 2025-11-24. Five domains → four. Observability folded into Architecture. App Delivery doubled (8% → 16%). Orchestration +6 points |
| Spotting stale material | Five domains, or a standalone "Cloud Native Observability" section, means the retired blueprint. Facts may be fine; weighting isn't |
| Weight disclosure | CNCF publishes domain-level weights only. Per-chapter emphasis in this book is authored judgment, diverging from the published weights by at most 2.8 points |
| "Cloud native" | Deliberately undefined until Chapter 17. It does **not** mean "runs in a public cloud" |
| How the book maps | Parts II–V ↔ the four domains, one-to-one. Progress through the book = progress through the blueprint |
| Soundings | A pacing instrument, not a quiz. Low score = read slowly. Never a verdict |
| Retrieval questions | Later chapters test earlier material on purpose. When it feels repetitive, that's the mechanism working |

[source: lf-kcna-exam-page-2026-08-23] [source: lf-kcna-program-changes-2026-08-23] [source: cncf-cloud-native-definition-2026-08-23]

---

🏆 **Safe Harbor**

Chapter 1 complete. You know what you're sitting, when the blueprint moved, and how to tell whether any given resource knows that. You've got a reading path calibrated to your own starting point, and a question about "cloud native" that you're carrying, unanswered, for the next four hundred pages.

That's the whole job of an orientation chapter, and it's done.

🗺️ *Chart* → 🌊 Passage → 🌅 Dawn

---

## The Voyage Ahead

Chapter 2 opens with a shipping container. An actual one: corrugated steel, standardized corner fittings, the sort that stacks by the thousand on a container ship.

That is not decoration, and it is not a metaphor chosen for the scenery. The intermodal shipping container changed global trade not by being a better box, but by being a box that cranes, truck beds, railcars, and ships' holds could all agree to handle identically. The contents stopped mattering to the infrastructure. That one decoupling, between what's inside and what moves it, is precisely what a software container does, and it's why Chapter 2 starts there rather than with a definition.

<!-- AUTHOR-REVIEW: The intermodal-container history above is uncached and load-bearing for all of Chapter 2's opening. Cache an authority during Chapter 2's research pass — Levinson, *The Box*, or ISO 668 — and tag it there. The specific "stacks eight high" figure from the prior draft has been softened out pending that source. -->

You'll get the definition too. But you'll get it after you can already see why it had to be that way.

44% of your exam begins on the next page.

> *"A chart is only as good as the survey behind it. Check the date in the corner before you trust the depths."*
