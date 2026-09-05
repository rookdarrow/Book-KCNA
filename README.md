# Lodestar Ledgers — The Kubernetes and Cloud Native Associate

**KCNA Exam Preparation Guide**

*Study less. Pass once.*

---

## About this book

A Lodestar Ledgers study guide for the **CNCF / Linux Foundation Kubernetes and Cloud Native Associate (KCNA)** exam — the entry-level, multiple-choice credential that certifies conceptual fluency in Kubernetes and the cloud native ecosystem.

Written against the **KCNA curriculum effective 24 November 2025**, which restructured the exam into four domains:

| # | Domain | Weight | Competencies |
|---|---|---|---|
| 1 | Kubernetes Fundamentals | **44%** | Core Concepts · Administration · Scheduling · Containerization |
| 2 | Container Orchestration | **28%** | Networking · Security · Troubleshooting · Storage |
| 3 | Cloud Native Application Delivery | **16%** | Application Delivery · Debugging |
| 4 | Cloud Native Architecture | **12%** | Observability · Cloud Native Ecosystem and Principles · Cloud Native Community and Collaboration |

Exam facts (Linux Foundation, verified 2026-08-23): $250 exam-only · 90 minutes · online-proctored multiple choice · two attempts included · 12-month eligibility window · certification valid 2 years · no prerequisites.

Unlike the CKA, this exam has no terminal. It tests whether you can recognize the right concept, component, or principle among plausible alternatives — so this guide is built around mental models, distinctions, and the misconceptions that cost points, not `kubectl` drills. Readers who go on to the CKA will find [`Book-CKA`](https://github.com/rookdarrow/Book-CKA) the natural next voyage.

## Status

**Commissioned 2026-08-23; manuscript complete and audited 2026-09-05.** Drafted end-to-end through the Lodestar Ledgers pipeline at [`rookdarrow/certcomp`](https://github.com/rookdarrow/certcomp), then every chapter was read in full against `docs/chapter-audit-protocol.md` and fixed in place (verdicts: chapters 1, 2, 3, 19 and 20 tight; chapter 12 over-scoped and trimmed at sentence level; the rest defensible). Claims are tagged to cached snapshots in `sources/`; the term ledger, the front matter, `the-lodestar.md` and the listing copy were reconciled with the chapters.

**Builds.** `KCNA.epub` passes epubcheck with no errors and reflows cleanly on five e-reader profiles; `KCNA.pdf` is the screen/reference PDF. After the 2026-09-05 trim pass (Closer Look callouts retired, one sidebar per chapter, Common Traps tables folded into the Snags) and a tighter print stylesheet, the 8.5x11 interior fits KDP's 828-page maximum at 821 pages; 6x9 (1,250) and 7x10 (1,055) do not, so the paperback is 8.5x11 unless the manuscript is split or trimmed further. The cover (`KCNA.png`/`KCNA.jpg`) uses the bearing-log art direction; the print wrap waits on the page count.

**Open items** are tracked as beads (`bd list --status open`): figure renders queued for regeneration where they contradicted the prose, glossary decisions for terms the ledger marks unowned, and the print-length decision above.

**Role in the Lodestar Ledgers series:**
- Role family: **The Communications Officer** — networking and distributed-systems coordination
- Seniority in family: **Junior** (the associate rung beneath the CKA's senior comms officer; peer tier to Network+)

## Working with this book

This repo is a sibling of [`rookdarrow/certcomp`](https://github.com/rookdarrow/certcomp), the writing pipeline. Clone both side-by-side:

```bash
git clone git@github.com:rookdarrow/certcomp.git
git clone git@github.com:rookdarrow/Book-KCNA.git
cd certcomp
pip install pyyaml
```

```bash
# Structural audit
python pipeline/structural_lint.py --book kcna --all-chapters --summary-only --no-color

# Book outline (B1–B5)
python pipeline/book_orchestrator.py --book kcna --run

# Chapter pipeline
python pipeline/orchestrator.py --book kcna --run --chapter 3

# Reconcile (TOC + drift report)
python pipeline/reconcile.py --book kcna --write
```

See [`certcomp/README.md`](https://github.com/rookdarrow/certcomp/blob/main/README.md) for the full command reference.

---

## Trademarks

Kubernetes and the Kubernetes logo are registered marks of The Linux Foundation. KCNA, CKA, CKAD, and the CNCF logo are marks of the Cloud Native Computing Foundation. Lodestar Ledgers is not affiliated with, endorsed by, or sponsored by CNCF or The Linux Foundation.

Copyright © 2026 Lodestar Ledgers. All rights reserved.
