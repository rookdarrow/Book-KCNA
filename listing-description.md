# Amazon / KDP listing copy — KCNA

Listing copy for the Kindle edition. KDP's description field caps at ~4,000 characters; the
versions below are the same copy in three forms — see "Which version to use where".

---

## Title fields

| KDP field | Value |
|---|---|
| Title | Kubernetes and Cloud Native Associate |
| Subtitle | KCNA Exam Prep & Study Guide — Covers the Four-Domain Curriculum Effective November 2025 |
| Series | Lodestar Ledgers |
| Author | Lodestar Ledgers |
| Publisher | Lodestar Ledgers |

**Categories (pick 3):** Computers & Technology › Certification › Other; Computers & Technology
› Networking & Cloud Computing › Cloud Computing; Computers & Technology › Operating Systems › Linux

**Keywords (7):** KCNA exam prep · Kubernetes certification · Kubernetes and Cloud Native Associate ·
cloud native study guide · CNCF certification study · Kubernetes for beginners · container orchestration exam

---

## Formatting recipe (verified against the live CAPM listing)

Read off the published CAPM page's own markup, so the KCNA listing renders identically to CAPM and CKA:

| Element | CAPM uses | Apply to KCNA |
|---|---|---|
| Section headings | `h2` (from KDP's Heading control; submit as `<h4>`) | the hook question, "Your Unfair Advantage", "Inside This Guide", "Is This Guide Right for You?" |
| Bold | the turn line, every ALL-CAPS feature heading, each `Chapter N` label, `Yes, if:` / `No, if:`, and the closing exam-stats sentence | same, with `Part N` in place of `Chapter N` |
| Italic | a few single emphasis words, plus the sign-off | `distinctions`, `one-line test`, `before`, `why`, `understand`, and the sign-off |
| Lists | `<ul><li>` for the Yes/No items | same |
| Chapter lines | one paragraph, `<br>` between lines — not separate paragraphs | same for the Part lines |

**Paste the HTML as a single line.** KDP converts every literal newline in the field into a `<br>` -- one character becomes four, so each line break silently costs +3 against the 4,000 cap *and* injects unwanted vertical space between block elements. The block below is deliberately unwrapped for that reason; do not reformat it before pasting.

**Two ways to apply it.** If the description field accepts HTML, paste the HTML block below. If you
are using the rich-text editor, paste the plain text further down and then apply the table above with
the toolbar — Heading for the four section headings, **B** for the bold items, *I* for the italics,
and the bullet control for the two lists.

---

## Book description (KDP HTML — matches the CAPM listing)

```html
<h4>What if you are studying for an exam that no longer exists?</h4><p>On 24 November 2025 the KCNA blueprint changed: five domains became four, Observability stopped being a domain of its own, and Application Delivery now carries one question in six. Much online material still teaches the old shape, and many candidates drill kubectl for an exam that never asks them to type. The problem is not effort. <b>It is direction.</b></p><p>This guide is different. It is written to the current curriculum and built for how the KCNA tests: one right idea among three that sound almost as good. It teaches the <i>distinctions</i>.</p><h4>Your Unfair Advantage</h4><p><b>WEIGHTED TO THE CURRENT BLUEPRINT</b></p><p>Four domains at their true weight: Kubernetes Fundamentals (44%), Container Orchestration (28%), Cloud Native Application Delivery (16%), Cloud Native Architecture (12%). Parts II through V map one-to-one onto them. Chapter 1 shows how to spot material built for the retired five-domain blueprint.</p><p><b>BUILT FOR DISCRIMINATION, NOT DRILLS</b></p><p>The KCNA asks you to pick the right concept from plausible alternatives, so every chapter names the pairs candidates confuse and gives each a <i>one-line test</i>. ReadWriteOnce means one node, not one Pod. A Secret is encoded, not encrypted.</p><p><b>ACTIVE RECALL BUILT IN</b></p><p>Every chapter opens with Soundings, a pre-test that shows what you already know and can skim. Checkpoints verify your understanding <i>before</i> you move on, and later chapters re-test earlier ones, because retrieving a half-forgotten fact is what makes it stay.</p><p><b>PRACTICE QUESTIONS WITH EXPLANATIONS</b></p><p>Not just the right answer -- but <i>why</i> every wrong answer is wrong. Plus a full-length, timed mock exam scored per domain, so a weak score maps straight to the Part that fixes it.</p><p><b>THE LODESTAR</b></p><p>One page: published exam facts, confusion-pair tests, and the hazards where intuition is wrong. Work it in the last hour.</p><h4>Inside This Guide</h4><p><b>Part I</b> -- Taking Departure: the exam as published, what changed in 2025, three reading paths<br><b>Part II</b> -- Kubernetes Fundamentals (44%): containers, control plane, objects, Pods, controllers, scheduling, administration<br><b>Part III</b> -- Container Orchestration (28%): networking, Services, Ingress, NetworkPolicy, storage, security, troubleshooting<br><b>Part IV</b> -- Cloud Native Application Delivery (16%): Helm, Kustomize, deployment strategies, GitOps, debugging your application<br><b>Part V</b> -- Cloud Native Architecture (12%): cloud native defined, CNCF governance, service mesh, serverless, autoscaling, observability<br><b>Part VI</b> -- Making Port: confusion pairs, pacing, glossary, The Lodestar, full mock exam</p><h4>Is This Guide Right for You?</h4><p><b>Yes, if:</b></p><ul><li>You are sitting the KCNA and want to pass first time</li><li>You are new to Kubernetes, or know only the corners of a cluster you touch</li><li>Your study material has five domains and you suspect it describes a different exam</li><li>You learn best with structure and built-in self-testing</li></ul><p><b>No, if:</b></p><ul><li>You want a kubectl drill book (the KCNA has no terminal)</li><li>You want to skim without engaging (the methodology works only if you use it)</li><li>You are preparing for the CKA, CKAD, or CKS (different exams; Lodestar Ledgers publishes a sibling CKA guide)</li></ul><p><b>The KCNA is 90 minutes, online, proctored, multiple choice. No prerequisites, two attempts included, valid for two years.</b> Current to the November 2025 curriculum.</p><p>This is not a credential you grind. It is one you <i>understand</i>.</p><p><i>From Lodestar Ledgers -- Study less. Pass once.</i></p><p>An independent publication, not affiliated with or endorsed by the Linux Foundation or the CNCF. Kubernetes is a registered trademark of the Linux Foundation.</p>
```

---

## Book description (paste-ready plain text)

Matches the structure of the published CAPM listing: hook, problem, "Your Unfair Advantage" feature
blocks, "Inside This Guide", "Is This Guide Right for You?", close. Contractions are expanded and
dashes are written as `--`, following that listing's convention.

**Length note.** KDP's counter includes the markup its editor generates from your line breaks,
so it reads higher than a raw character count -- measured at roughly +3 per line break (a 3,902
raw draft counted 4,122 in KDP). Keep the raw text near 3,700 with ~65 line breaks and it lands
close to 3,900 by KDP's count. Re-check the counter after pasting; do not trust the raw number.

KDP's description field is a rich-text box with a formatting toolbar -- it does not interpret typed
HTML or markdown. Paste the block below as-is, then use the toolbar to bold the section headings
("Your Unfair Advantage", "Inside This Guide", "Is This Guide Right for You?") and the ALL-CAPS
feature lines. Nothing below is markdown or HTML; it pastes clean.

```
What if you are studying for an exam that no longer exists?

On 24 November 2025 the KCNA blueprint changed: five domains became four, Observability stopped being a domain of its own, and Application Delivery now carries one question in six. Much online material still teaches the old shape, and many candidates drill kubectl for an exam that never asks them to type. The problem is not effort. It is direction.

This guide is different. It is written to the current curriculum and built for how the KCNA tests: one right idea among three that sound almost as good. It teaches the distinctions.

-----------

Your Unfair Advantage

WEIGHTED TO THE CURRENT BLUEPRINT

Four domains at their true weight: Kubernetes Fundamentals (44%), Container Orchestration (28%), Cloud Native Application Delivery (16%), Cloud Native Architecture (12%). Parts II through V map one-to-one onto them. Chapter 1 shows how to spot material built for the retired five-domain blueprint.

BUILT FOR DISCRIMINATION, NOT DRILLS

The KCNA asks you to pick the right concept from plausible alternatives, so every chapter names the pairs candidates confuse and gives each a one-line test. ReadWriteOnce means one node, not one Pod. A Secret is encoded, not encrypted.

ACTIVE RECALL BUILT IN

Every chapter opens with Soundings, a pre-test that shows what you already know and can skim. Checkpoints verify your understanding before you move on, and later chapters re-test earlier ones, because retrieving a half-forgotten fact is what makes it stay.

PRACTICE QUESTIONS WITH EXPLANATIONS

Not just the right answer -- but why every wrong answer is wrong. Plus a full-length, timed mock exam scored per domain, so a weak score maps straight to the Part that fixes it.

THE LODESTAR

One page: published exam facts, confusion-pair tests, and the hazards where intuition is wrong. Work it in the last hour.

-----------

Inside This Guide

Part I -- Taking Departure: the exam as published, what changed in 2025, three reading paths
Part II -- Kubernetes Fundamentals (44%): containers, control plane, objects, Pods, controllers, scheduling, administration
Part III -- Container Orchestration (28%): networking, Services, Ingress, NetworkPolicy, storage, security, troubleshooting
Part IV -- Cloud Native Application Delivery (16%): Helm, Kustomize, deployment strategies, GitOps, debugging your application
Part V -- Cloud Native Architecture (12%): cloud native defined, CNCF governance, service mesh, serverless, autoscaling, observability
Part VI -- Making Port: confusion pairs, pacing, glossary, The Lodestar, full mock exam

-----------

Is This Guide Right for You?

Yes, if:

You are sitting the KCNA and want to pass first time
You are new to Kubernetes, or know only the corners of a cluster you touch
Your study material has five domains and you suspect it describes a different exam
You learn best with structure and built-in self-testing

No, if:

You want a kubectl drill book (the KCNA has no terminal)
You want to skim without engaging (the methodology works only if you use it)
You are preparing for the CKA, CKAD, or CKS (different exams; Lodestar Ledgers publishes a sibling CKA guide)

-----------

The KCNA is 90 minutes, online, proctored, multiple choice. No prerequisites, two attempts included, valid for two years. Current to the November 2025 curriculum.

This is not a credential you grind. It is one you understand.

From Lodestar Ledgers -- Study less. Pass once.

An independent publication, not affiliated with or endorsed by the Linux Foundation or the CNCF. Kubernetes is a registered trademark of the Linux Foundation.
```

---

## Short variants

**A+ Content / social (≈300 characters):**

The KCNA has no terminal. It asks whether you can tell the right concept from three that sound almost as good. Written to the four-domain curriculum effective November 2025 — 44/28/16/12 — this guide teaches the distinctions that cost points. Pre-tests, a full mock exam, a one-page Lodestar. Study less. Pass once.

**One-line hook:**

Most KCNA guides teach you Kubernetes. This one teaches you to tell the right answer from the three that sound just like it.

---

## Which version to use where

| Form | Where it goes |
|---|---|
| KDP HTML block | The KDP description field when it accepts HTML. Paste as a single line; check the counter after pasting. |
| Paste-ready plain text | The KDP rich-text editor (apply the formatting recipe with the toolbar), and any storefront field that strips markup. |
| Short variants | A+ Content modules and social posts (the ≈300-character block); ads, the series page, and back-cover teasers (the one-line hook). |

All three forms carry the same claims; if a fact changes, change it in all three.

---

## Notes before submission

- **No feature counts.** The CKA listing quotes checkpoint, practice-question, and glossary-term counts. This copy deliberately does not: the counts are not in the KCNA source set consulted for this file (README, table of contents, front matter, Chapter 1, The Lodestar). Once `pipeline/reconcile.py` reports final numbers, prefix them to the ALL-CAPS headings the way the CKA copy does ("N PRACTICE QUESTIONS WITH EXPLANATIONS"), and re-check the 4,000 cap -- the HTML block is at ~3,930 and has about 70 characters of headroom.
- **No retired-blueprint percentages.** Chapter 1 carries an AUTHOR-REVIEW flag on the provenance of the five retired weights. The copy states only what survives either resolution: five domains became four, Observability stopped being a standalone domain, and Application Delivery now sits at 16%.
- **No question count or pass mark.** The book's own argument is that "60 questions, 75% to pass" travels on repetition, and that both figures are handbook facts for multiple-choice exams as a class. The closing sentence uses only the README's exam-facts line (verified 2026-08-23): 90 minutes, online-proctored multiple choice, two attempts, 12-month eligibility, valid two years, no prerequisites. Price is omitted as volatile. Re-verify against the Linux Foundation exam page before publishing.
- **Author field.** The front matter names Sean Bigelow as author; the CKA listing submits Lodestar Ledgers in the Author field. The table above mirrors the CKA choice. Settle this before submission so the series pages match.
- **Endorsement language.** The exam and its administering bodies are named factually. Nothing in the copy claims affiliation, and the disclaimer paragraph is required in both blocks.
