---
source_url: "https://sre.google/sre-book/monitoring-distributed-systems/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 6 'Monitoring Distributed Systems' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["monitoring", "white-box-monitoring", "black-box-monitoring", "alert", "root-cause", "why-monitor"]
---
# Monitoring — definitions (Site Reliability Engineering, ch. 6)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Companion snapshot to `sre-book-four-golden-signals-2026-08-23.md`, which is the same chapter.
This one carries the chapter's **Definitions** section, cached to close the Ch 18 §1 gap: the
corpus previously had a sourced definition of observability and none of monitoring.

## Definitions

> **Monitoring** — "Collecting, processing, aggregating, and displaying real-time quantitative data
> about a system"

> **White-box monitoring** — "Monitoring based on metrics exposed by the internals of the system,
> including logs, interfaces"

> **Black-box monitoring** — "Testing externally visible behavior as a user would see it"

> **Alert** — "A notification intended to be read by a human and that is pushed to a system such as
> a bug or ticket queue"

> **Root cause** — "A defect in a software or human system that, if repaired, instills confidence
> that this event won't happen again"

**Excerpt note.** The Monitoring definition as printed continues past "about a system" with a list
of examples. That continuation was not captured. Quote only as far as the text above runs; do not
extend it from memory.

## Why Monitor?

The chapter gives four reasons, each illustrated by a question:

> **Long-term trends** — "How big is my database and how fast is it growing?"

> **Alerting** — "Something is broken, and somebody needs to fix it right now!"

> **Building dashboards** — "Dashboards should answer basic questions about your service"

> **Debugging** — "Our latency just shot up; what else happened around the same time?"

## Drafting note for §1

These four reasons are the sharpest available support for the chapter's curiosity gap. Every one
of them is a question **chosen in advance** — which is precisely the property §1 contrasts against
observability's "unknown unknowns." The contrast is available without editorialising: monitoring's
own canonical text defines it by the questions you decided to ask.
