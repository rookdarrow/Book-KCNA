---
source_url: "https://glossary.cncf.io/observability/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary"
objectives_covered: ["D4.1"]
concepts_covered: ["observability", "actionable-insights", "observability-tools", "monitoring"]
---
# Observability — CNCF Cloud Native Glossary

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Definition

> "Observability is a system property that defines the degree to which the system can generate
> actionable insights. It allows users to understand a system's state from these external outputs
> and take (corrective) action."

## What is observed

> "Computer systems are measured by observing low-level signals such as CPU time, memory, disk
> space, and higher-level and business signals, including API response times, errors, transactions
> per second, etc. These observable systems are observed (or monitored) through specialized tools,
> so-called observability tools."

## Why it matters

> "Observable systems yield meaningful, actionable data to their operators, allowing them to
> achieve favorable outcomes (faster incident response, increased developer productivity) and less
> toil and downtime."

> "Consequently, how observable a system is will significantly impact its operating and development
> costs."

## Drafting guardrail

This entry treats "observed (or monitored)" as near-synonyms and is therefore **NOT** the source for
Ch 18 §1's observability-vs-monitoring distinction. Use the OTel primer for observability and
`cncf-tag-observability-whitepaper-2026-08-31.md` / `sre-book-monitoring-definitions-2026-08-31.md`
for monitoring. This snapshot is here for the "property of the system, not a tool" beat and for the
operating-cost consequence, both of which the other sources do not state as plainly.

## Not on this page

There is no standalone "Monitoring" entry in the CNCF Cloud Native Glossary.
`https://glossary.cncf.io/monitoring/` returned HTTP 404 on 2026-08-31.
