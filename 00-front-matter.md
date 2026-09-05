---
title: "Lodestar Ledgers: KCNA Study Guide"
subtitle: "Kubernetes and Cloud Native Associate Exam Preparation Guide"
tagline: "Study less. Pass once."
author: "Sean Bigelow"
publisher: "Lodestar Ledgers"
edition: "First Edition"
exam_version: "KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)"
---

# KCNA

## Kubernetes and Cloud Native Associate

---

# Lodestar Ledgers: KCNA

**Kubernetes and Cloud Native Associate Exam Preparation Guide**

*KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)*

---

**LODESTAR LEDGERS**

*Study less. Pass once.*

---

## Copyright

**Lodestar Ledgers: KCNA**
Kubernetes and Cloud Native Associate Exam Preparation Guide

Copyright (c) 2026 Lodestar Ledgers. All rights reserved.

No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher, except in the case of brief quotations embodied in critical reviews and certain other noncommercial uses permitted by copyright law.

**Trademarks**

Kubernetes and the Kubernetes logo are registered marks of The Linux Foundation. KCNA, KCSA, CKA, CKAD, CKS, and the CNCF logo are marks of the Cloud Native Computing Foundation. Helm, Prometheus, Argo, Flux, Envoy, Jaeger, OpenTelemetry, containerd, CRI-O, Cilium, Falco, Harbor, KEDA, Knative, Kyverno and Notary are projects of the Cloud Native Computing Foundation. All other trademarks are the property of their respective owners.

**Lodestar Ledgers is not affiliated with, endorsed by, or sponsored by the Cloud Native Computing Foundation or The Linux Foundation.**

**Disclaimer**

This study guide is designed to help candidates prepare for the KCNA examination. While every effort has been made to ensure accuracy, the author and publisher make no warranty, express or implied, regarding the completeness or accuracy of the information contained herein.

This guide contains no actual examination questions. Every practice question in these pages was written for this book.

Examination content and requirements are subject to change. Candidates should verify current exam specifications at training.linuxfoundation.org and at the CNCF curriculum repository, github.com/cncf/curriculum.

**Edition Information**

First Edition: 2026 Version: 1.0

ISBN: [To be assigned]

Author: Sean Bigelow

Published by Lodestar Ledgers
lodestarledgers.com

---

## For Those About to Navigate

Most people preparing for this exam do not study too little. They study too much, in the wrong direction, and arrive knowing a great many facts they cannot connect.

That is a navigation problem, not an effort problem. A navigator who knows every star in the sky and cannot take a bearing is not close to being useful — they are missing the one thing that turns knowledge into position. The KCNA is a conceptual exam. It does not ask you to type anything. It asks whether you can recognize the right idea among three that sound almost as good, which means the work is not accumulating more facts but knowing which distinctions carry weight and which do not.

So this book is organized around distinctions. Where two things are confused, it names the confusion and gives you a one-line test. Where the documentation says something surprising, it quotes it and tells you where it came from. Where this book is reasoning rather than citing, it says so — you should be able to tell the difference between what the project publishes and what an author concluded, because on exam day only one of those is reliable.

There is one more thing worth saying before you start. The curriculum moved under everyone's feet on 24 November 2025: five domains became four, Observability stopped being a domain of its own, and Cloud Native Application Delivery doubled in weight. A great deal of the study material you will find online still teaches the old shape. This book targets the current one, and Chapter 1 shows you exactly what changed and what it costs you.

Take a bearing. Then set out.

---

## How to Use This Guide

### Understanding the Navigation Markers

Throughout this guide, you'll encounter consistent markers that help you navigate the material:

| Marker | Name | Meaning |
|---|---|---|
| 🧭 **Soundings** | Pre-chapter diagnostic -- what you already know before you read |
| ★ **Fixed Point** | A key concept to anchor in memory -- the essential takeaway |
| ☆ **Taking Your Bearings** | Self-assessment checkpoint to verify your understanding |
| — **Dead Reckoning** | Facts-only explanation without metaphors or analogies |
| ⚠ **Navigational Hazards** | Warning about common mistakes or exam traps |
| 🏆 **Safe Harbor** | Chapter complete -- summary of what you've mastered |

| ☀️ **Zenith** | A synthesis moment — where several threads resolve into one idea |
| ⚓ **Worth Securing** | A point worth fastening down before moving on |
| 🪝 **Snag** | A place the obvious reading is the wrong one |
| 🔭 **Closer Look** | Deeper than the exam requires, included because it explains the rest |
| 🪢 **Mnemonic** | A memory hook for something arbitrary |
| 🚨 **Exam Alert** | The highest-priority facts in the chapter |
| 🗺️→🌊→🌅 **Voyage Progress** | Chart, Passage, Dawn — how far the voyage stands |

**Difficulty scale.** Every numbered section carries one of four markers: ⚪ **Foundation** (you must have this), 🔵 **Standard** (ordinary exam material), 🟡 **Advanced** (a distinction that separates candidates), 🔴 **Expert** (beyond what the exam requires, included for coherence).

### Reading for Maximum Retention

**First pass:** Read the Soundings first and answer them badly. Getting a question wrong before you read the material is what makes the material stick; the discomfort is the mechanism, not a side effect.

**At checkpoints:** Close the book. Answer from memory, out loud or on paper. If you can only recognize the answer when you see it, you have not learned it yet — recognition and recall are different, and the exam tests the second one.

**Between sessions:** Leave a gap. A day is better than an hour, and a week is better than a day, up to a point. Re-reading immediately feels productive and does almost nothing.

**Before the exam:** Work `the-lodestar.md`, this book's one-page reference. Chapter 19 §5 tells you exactly how to use it in the last hour, and what to leave alone.

### Chapter Structure

Each chapter follows a consistent structure:

1. **Attention Budget** -- Recommended time allocation and study conditions
2. **Soundings** -- A short diagnostic so you can skip what you already know
3. **Why This Chapter Matters** -- Context and motivation
4. **Core Content** -- The material you need to know
5. **Taking Your Bearings** -- Self-assessment checkpoints
6. **Exam Alert** -- High-priority topics and common traps
7. **Practice Questions** -- With explanations of why the wrong answers are wrong
8. **Chapter Summary** -- Key concepts in table format
9. **Safe Harbor** -- Chapter completion confirmation
10. **The Voyage Ahead** -- Preview of the next chapter

### Study Schedule Recommendations

| Available Time | Recommended Approach |
|----------------|---------------------|
| **One week** | Chapters 1, 19 and 20 first — the shape of the exam, the confusion pairs, and a full mock to find out where you actually stand. Then the two weakest domains the mock exposes. Do not read front to back; you will not finish. |
| **One month** | One Part per week, in order, with the checkpoints worked rather than read. Take the Chapter 20 mock at the three-week mark, not at the end, so its results still have time to change what you do. |
| **Three months** | Front to back, one chapter per sitting, checkpoints closed-book. Re-take the mock twice — once at the halfway point and once in the final week — and use the per-domain tally rather than the total. |

### What This Guide Covers

This guide aligns with the CNCF's published KCNA curriculum, effective 24 November 2025:

- **Kubernetes Fundamentals** (44%) — Core Concepts, Administration, Scheduling, Containerization — *Chapters 2–8*
- **Container Orchestration** (28%) — Networking, Security, Troubleshooting, Storage — *Chapters 9–13*
- **Cloud Native Application Delivery** (16%) — Application Delivery, Debugging — *Chapters 14–16*
- **Cloud Native Architecture** (12%) — Observability, Cloud Native Ecosystem and Principles, Cloud Native Community and Collaboration — *Chapters 17–18*

The per-chapter percentages this book prints are **authored judgment**, not published data. CNCF publishes weights per domain and names the competencies beneath them; it publishes no sub-weights and no topic list. Where this book allocates, it says so.

### What This Guide Doesn't Replace

- **Official CNCF and Linux Foundation resources** — the published curriculum, the candidate handbook, and the Kubernetes documentation itself. This book cites them; it does not supersede them.
- **Hands-on experience** — the KCNA has no terminal, so you can pass it without a cluster. You will understand it far better with one, and everything after it requires one.
- **Timed practice** — Chapter 20 is one full-length mock. One is enough to calibrate; it is not enough to practice pacing. Sit it under real conditions.
- **Your judgment** -- If something here conflicts with official guidance, defer to it

---

## Quick Reference: Domain Weights

```
Kubernetes Fundamentals            ████████████████████████  44%   Ch 2-8
Container Orchestration            ███████████████           28%   Ch 9-13
Cloud Native App Delivery          █████████                 16%   Ch 14-16
Cloud Native Architecture          ██████                    12%   Ch 17-18
```

Nearly half the exam is Kubernetes Fundamentals, so Part II is where the hours go — but the two smallest domains are where candidates most often lose points they could have kept, because they are the easiest to skim and the hardest to bluff. Weight your study by the percentages; weight your *review* by where your mock results are weakest.

---

*Your voyage begins on the next page.*

---

# KCNA Certification Study Guide

## A Lodestar Ledgers Publication

---

## Table of Contents

## Front Matter

- [For Those About to Navigate](00-front-matter.md#for-those-about-to-navigate)
- [How to Use This Guide](00-front-matter.md#how-to-use-this-guide)

---

## Chapter 1: Taking Departure
*"Ninety minutes, four domains, and a curriculum that moved"*

[Read chapter ->](chapter-01-taking-departure.md)

- ⚪ §1 — What the KCNA Is, and Who It's For
- ⚪ §2 — Ninety Minutes: The Exam as Published
- 🔵 §3 — The Curriculum That Moved Under Everyone's Feet
- ⚪ §4 — The Phrase We Haven't Defined Yet
- ⚪ §5 — How This Book Is Built
- ⚪ §6 — Three Ways to Read This Book

---

## Chapter 2: Cargo in Standard Crates
*"Why the shipping container beat the ship"*

[Read chapter ->](chapter-02-cargo-in-standard-crates.md)

- ⚪ §1 — What a Container Actually Is
- ⚪ §2 — What's Inside an Image
- 🔵 §3 — Registries, Tags, and Digests
- 🔵 §4 — The Container Runtime Interface
- 🔵 §5 — The Open Container Initiative
- 🟡 §6 — When Kubernetes Pulls, and When It Doesn't
- 🟡 §7 — Not All Isolation Is Equal: RuntimeClass
- 🔵 §8 — The Crate, Not the Cargo

---

## Chapter 3: The Ship's Company
*"Everyone aboard has one job, and none of them is 'be in charge'"*

[Read chapter ->](chapter-03-the-ship-s-company.md)

- ⚪ §1 — How the Cluster Got the Shape It Has
- ⚪ §2 — The Control Plane
- ⚪ §3 — Node Components in Context
- 🔵 §4 — Addons, and What Else Is Optional
- 🔵 §5 — The Only Door In
- 🔵 §6 — Controllers and the Control Loop
- 🟡 §7 — Nobody Is in Charge

---

## Chapter 4: Records of Intent
*"You don't give Kubernetes orders. You file a declaration."*

[Read chapter ->](chapter-04-records-of-intent.md)

- ⚪ §1 — You File a Declaration
- ⚪ §2 — The Anatomy of a Record
- 🔵 §3 — Where a Name Lives
- 🔵 §4 — Configuration Kept Outside the Image
- 🔵 §5 — The Universal Join
- 🟡 §6 — A Declaration, Not an Order

---

## Chapter 5: The Smallest Vessel
*"A Pod is not a container, and that distinction is worth points"*

[Read chapter ->](chapter-05-the-smallest-vessel.md)

- ⚪ §1 — The Pod as the Unit of Scheduling
- 🔵 §2 — More Than One Container Aboard
- 🔵 §3 — Everything That Must Happen First
- ⚪ §4 — Scheduled Once, Replaced Never
- 🔵 §5 — Pod Phases and Container States
- ⚪ §6 — A Pod's Identity
- 🔵 §7 — Three Probes, Three Jobs
- 🟡 §8 — What a Pod Is Owed
- ☀️ §9 — The Smallest Deployable Unit

---

## Chapter 6: Fleets, Not Vessels
*"Nobody sails one Pod"*

[Read chapter ->](chapter-06-fleets-not-vessels.md)

- ⚪ §1 — The Resource That Holds the Intent
- ⚪ §2 — A Loop You Can Watch Working
- 🔵 §3 — How a Controller Knows Its Own
- 🔵 §4 — Changing the Fleet Under Way
- 🔵 §5 — Every Rollout Is a Revision
- 🔵 §6 — When Pods Are Not Interchangeable
- ⚪ §7 — One Per Node, and Work That Ends
- 🟡 §8 — The Control Loop, Extended
- ☀️ §9 — Nobody Sails One Pod

---

## Chapter 7: Assigning the Berth
*"Filter, score, bind — and then a coin flip"*

[Read chapter ->](chapter-07-assigning-the-berth.md)

- ⚪ §1 — One Decision, Made Once
- 🔵 §2 — What Makes a Node Feasible
- 🔵 §3 — Asking for a Particular Berth
- 🔵 §4 — When the Berth Refuses You
- 🟡 §5 — Placing Pods Relative to Each Other
- 🟡 §6 — Overruling the Scheduler, and Replacing It
- ☀️ §7 — Everything Is a Filter or a Score

---

## Chapter 8: Standing the Watch
*"The commands you'll actually type, and the versions that bite"*

[Read chapter ->](chapter-08-standing-the-watch.md)

- ⚪ §1 — The Grammar of a Command
- 🔵 §2 — Three Gates and a Logbook
- 🔵 §3 — Dividing a Shared Cluster
- 🔵 §4 — Taking a Node Out of Service
- ⚪ §5 — Who Owns the Control Plane
- 🟡 §6 — Versions That Are Allowed to Disagree
- 🔵 §7 — The One Backup That Matters
- ⚪ §8 — Rules, or Consequences

---

## Chapter 9: Every Pod Has an Address
*"Flat networks, stable names, and the abstraction that survives churn"*

[Read chapter ->](chapter-09-every-pod-has-an-address.md)

- ⚪ §1 — Four Rules and a Plugin
- ⚪ §2 — The Address That Doesn't Last
- 🔵 §3 — Four Ways to Be Reachable
- 🔵 §4 — The List Behind the Name
- 🟡 §5 — When You Don't Want a Single Address
- 🔵 §6 — The Component That Makes It Real
- 🔵 §7 — Names, and Where They Resolve
- ☀️ §8 — A Query With a Name

---

## Chapter 10: Traffic from Beyond the Cluster
*"Frozen, superseded, and inert without a controller"*

[Read chapter ->](chapter-10-traffic-from-beyond-the-cluster.md)

- ⚪ §1 — Where LoadBalancer Runs Out
- 🔵 §2 — Routing by Host and Path
- ⚪ §3 — The Object Is Not the Implementation
- ⚪ §4 — Frozen, Not Deprecated
- 🟡 §5 — Roles, Not Just Routes
- 🔵 §6 — Allowing, Never Denying
- 🟡 §7 — What NetworkPolicy Cannot Do
- ☀️ §8 — Nothing Happens Without a Controller

---

## Chapter 11: Below the Waterline
*"Storage outlives the Pod that asked for it"*

[Read chapter ->](chapter-11-below-the-waterline.md)

- ⚪ §1 — Three Lifetimes, and the Volumes That Have Them
- ⚪ §2 — The Claim and the Supply
- 🔵 §3 — Provisioning on Demand
- 🔵 §4 — Access Modes and What Happens After
- 🔵 §5 — Who Actually Provides the Storage
- 🔵 §6 — Pods That Are Not Interchangeable, Revisited
- ☀️ §7 — Outliving the Pod That Asked

---

## Chapter 12: Locks, Keys, and Watchstanders
*"RBAC has no deny rule, and Secrets aren't encrypted"*

[Read chapter ->](chapter-12-locks-keys-and-watchstanders.md)

- ⚪ §1 — Four Layers and Four Phases
- ⚪ §2 — Who You Are
- 🔵 §3 — What You May Do
- 🔵 §4 — Secrets Are Not Encrypted
- 🔵 §5 — What a Pod May Do to Its Node
- 🔵 §6 — Three Levels, Three Modes
- 🟡 §7 — Trusting What You Ship
- 🔵 §8 — Rules That Watch
- ☀️ §9 — Additive, Never Deny

---

## Chapter 13: When the Cluster Won't Answer
*"Read the phase before you read the logs"*

[Read chapter ->](chapter-13-when-the-cluster-won-t-answer.md)

- ⚪ §1 — Whose Problem Is This, and What to Read First
- 🔵 §2 — Pods That Never Start
- ⚪ §3 — Looking Inside
- 🔵 §4 — Pods That Start and Then Don't Stay
- 🟡 §5 — When the Node Is the Problem
- 🟡 §6 — Versions That Don't Agree
- 🔵 §7 — Numbers Nobody Collects by Default
- ☀️ §8 — Read the Phase First

---

## Chapter 14: Packing for the Voyage
*"A chart is not a release, and templates are not the point"*

[Read chapter ->](chapter-14-packing-for-the-voyage.md)

- ⚪ §1 — Why a Folder of YAML Stops Working
- ⚪ §2 — What a Chart Contains
- 🔵 §3 — Chart, Release, Revision
- ⚪ §4 — Where Charts Come From
- 🔵 §5 — Patching Instead of Templating
- 🔵 §6 — Which One, When
- ☀️ §7 — A Package, Not a Template

---

## Chapter 15: The Chart Is the Truth
*"GitOps is the control loop you already learned, pointed at a repository"*

[Read chapter ->](chapter-15-the-chart-is-the-truth.md)

- ⚪ §1 — Twelve Factors, and the Ones Kubernetes Already Solved
- 🔵 §2 — Ways to Replace What's Running
- 🔵 §3 — Push, or Pull
- 🔵 §4 — An Agent That Watches a Repository
- 🟡 §5 — Ordering the Sync
- 🔵 §6 — The Other Agent, and More Than One Cluster
- ☀️ §7 — The Control Loop, Pointed at a Repository

---

## Chapter 16: Your Application, Their Cluster
*"Four questions that separate your bug from theirs"*

[Read chapter ->](chapter-16-your-application-their-cluster.md)

- ⚪ §1 — Handed Back
- 🔵 §2 — When It Never Got Started
- 🔵 §3 — Getting Inside, and Adding What Isn't There
- 🔵 §4 — Is Anything Even Selected
- ⚪ §5 — Bypassing the Service on Purpose
- 🟡 §6 — When Each Replica Is Its Own
- 🟡 §7 — Before You Ship It
- ☀️ §8 — Mine, or the Platform's

---

## Chapter 17: The Fleet and Its Charts
*"Meshes, functions, autoscalers, and the foundation that keeps the map"*

[Read chapter ->](chapter-17-the-fleet-and-its-charts.md)

- ⚪ §1 — What "Cloud Native" Actually Names
- ⚪ §2 — Sandbox, Incubating, Graduated, and Who Decides
- 🔵 §3 — Small Pieces, Replaced Whole
- 🔵 §4 — Every Place Kubernetes Lets You In
- 🟡 §5 — A Network That Knows What It's Carrying
- 🔵 §6 — Code Without a Server to Put It On
- 🔵 §7 — Four Things That Scale
- ⚪ §8 — How the Project Actually Runs, and How You'd Join
- ☀️ §9 — One Pluggability Story

---

## Chapter 18: Reading the Instruments
*"Four signals, and the question they exist to answer"*

[Read chapter ->](chapter-18-reading-the-instruments.md)

- ⚪ §1 — What You Can Ask, and What You Already Know
- ⚪ §2 — Four Signals
- 🔵 §3 — Numbers Over Time
- 🔵 §4 — Pulling, Not Being Pushed
- 🟡 §5 — Following One Request
- 🔵 §6 — Lines From Everywhere
- 🔵 §7 — Is the Service Doing What Users Expect
- ☀️ §8 — One Question, Four Instruments

---

## Chapter 19: Bearings Before Landfall
*"Everything that connects, and the traps that don't"*

[Read chapter ->](chapter-19-bearings-before-landfall.md)

- ☀️ §1 — Nine Threads Through Eighteen Chapters
- 🟡 §2 — The Pairs That Cost Points
- ⚪ §3 — Ninety Minutes
- ⚪ §4 — Where the Weight Actually Is
- ⚪ §5 — Using The Lodestar
- ⚪ §6 — The Week Before

---

## Chapter 20: Full Mock Exam
*"Ninety minutes. No notes. Find out."*

[Read chapter ->](chapter-20-full-mock-exam.md)

- Instructions
- Exam
- Mock Exam Answers & Walkthroughs
- Scoring Rubric

---

## Back Matter

- Glossary
- The Lodestar (single-page reference)
