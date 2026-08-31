---
source_url: "https://prometheus.io/docs/prometheus/latest/querying/basics/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["promql", "time-series"]
---
# Prometheus — Querying basics (PromQL)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## What PromQL is

> "Prometheus provides a functional query language called PromQL (Prometheus Query Language) that
> lets the user select and aggregate time series data in real time."

## Where results go

> "In the Prometheus UI, the 'Table' tab is for instant queries and the 'Graph' tab for range
> queries."

> "Other programs can fetch the result of a PromQL expression via the HTTP API."

## Drafting guardrail

The outline is explicit that PromQL is **not** on this chapter's teaching surface: it was
deliberately excluded from `kb_tags.commands` because it is a query language, not a kubectl verb,
and §4 teaches that it exists and what it is for, not syntax. **No PromQL syntax is cached in this
snapshot and none should be drafted.** One sentence — a query language for selecting and
aggregating time series — is the whole of §4's obligation.

The HTTP API sentence is the sourced link to Grafana: Grafana reads what Prometheus stores through
that API rather than being part of Prometheus. That is §8's separability shape appearing again,
and it is worth one clause.
