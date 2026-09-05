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
