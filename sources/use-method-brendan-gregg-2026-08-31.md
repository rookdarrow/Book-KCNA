---
source_url: "https://www.brendangregg.com/usemethod.html"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Brendan Gregg — author and originator of the USE Method; the reference linked by the CNCF TAG Observability whitepaper"
objectives_covered: ["D4.1"]
concepts_covered: ["use-method", "utilization", "saturation", "errors", "resource-bottlenecks"]
---
# The USE Method

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

**Authority note.** This is the method's originating publication by its author, and it is the live
link the CNCF TAG Observability whitepaper points to for USE. It is a personal technical site rather
than vendor or standards documentation — tier 3 by the stage's priority order. Better sourced than
RED (see `red-method-tom-wilkie-2026-08-31.md`).

## What it is

> "The Utilization Saturation and Errors (USE) Method is a methodology for analyzing the
> performance of any system."

## The three terms

> **Utilization** — "the average time that the resource was busy servicing work"

> **Saturation** — "the degree to which the resource has extra work which it can't service, often
> queued"

> **Errors** — "the count of error events"

## What it is for

> "It directs the construction of a checklist, which for server analysis can be used for quickly
> identifying resource bottlenecks or errors."

> "The USE Method helps you identify which metrics to use"

## Origin

> "I developed the USE Method to teach others how to solve common performance issues quickly,
> without overlooking important areas."

## ⚠ VOCABULARY COLLISION — read before drafting §7

**"Utilization" now means three different things inside Chapter 18, and all three are sourced:**

| Meaning | Source | Section |
|---|---|---|
| A percentage of the containers' **resource request** | `k8s-docs-hpa-utilization-vs-requests-2026-08-31.md` | §3 |
| The **golden signal** "saturation" — how full the service is; latency rises before 100% | `sre-book-four-golden-signals-2026-08-23.md` | §7 |
| **The average time a resource was busy** — a duration fraction | this snapshot | §7 |

§3 and §7 sit two sections apart. **Recommendation: §7 says "saturation" and never "utilization,"**
so §3 keeps the word to itself and the reader's §3 encoding is not overwritten forty minutes later.
The USE method's own U is unavoidable if USE is named — which is a further argument for the
outline's fallback posture of naming it only, in one non-graded clause.

Per the outline: no Practice or Bearings item may depend on USE.
