---
source_url: "https://prometheus.io/docs/practices/naming/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — metric and label naming practices"
objectives_covered: ["D4.1"]
concepts_covered: ["metric-labels", "cardinality"]
---
# Prometheus — Metric and label naming (LABELS section)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Ch 18 §3's cardinality gap (Stage 1 Open Question #1, row 6 — non-blocking, now closed).

## The cost of a label

> "Every unique combination of key-value label pairs represents a new time series, which can
> dramatically increase the amount of data stored."

## High cardinality

> "Do not use labels to store dimensions with high cardinality (many different label values), such
> as user IDs, email addresses, or other unbounded sets of values."

## Redundant naming

> "Do not put the label names in the metric name, as this introduces redundancy and will cause
> confusion if the respective labels are aggregated away."

## Drafting note for §3

The outline's posture was: keep cardinality as a 🔭 Closer Look, not graded, unless this fetch
landed. It landed, with the concrete unbounded-set examples (user IDs, email addresses) that make
the idea teachable in two sentences. The Closer Look call is still the right one — cardinality is
not on the KCNA exam surface and B1 lists no trap for it — but it is now a sourced Closer Look
rather than an inferred one, which matters for Ethical Guardrail #8.

The redundant-naming line is **out of scope** for Ch 18. Cached only so the section is complete.
