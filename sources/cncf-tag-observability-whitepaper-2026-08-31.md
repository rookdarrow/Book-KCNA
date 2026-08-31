---
source_url: "https://github.com/cncf/tag-observability/blob/main/whitepaper.md"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Cloud Native Computing Foundation — Technical Advisory Group (TAG) Observability, Observability Whitepaper"
objectives_covered: ["D4.1"]
concepts_covered: ["observability", "monitoring", "known-unknowns", "unknown-unknowns", "signals", "metrics", "logs", "traces", "profiles", "dumps", "red-method", "use-method"]
---
# CNCF TAG Observability — Observability Whitepaper

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Observability

> "observability is a measure of how well internal states of a system can be inferred from
> knowledge of its external outputs."

> "observability is not just using all the pretty and shiny tools."

> "You must be conscious about what outputs are coming out of your system."

## Monitoring, and the distinction — THE LOAD-BEARING PASSAGE FOR Ch 18 §1

> "Monitoring is called a system that can detect known unknowns -- as opposed to observability
> which emphasizes being able to find and reason about unknown unknowns as well."

> "Monitoring, traditionally, was a system admin or human operator (ops) concern"

> "ops folks had to infer the state of the system from external signals"

## Signals

The whitepaper enumerates **five** primary signals: metrics, logs, traces, profiles and dumps.
Of these it says:

> "they are commonly mentioned and probably what you're going to start with"

Individual definitions given:

> "Metrics are numeric representations of data."

> "Logs are one or more textual entries describing usage patterns, activities, and operations."

> "Distributed tracing is the technique of understanding what happened during a distributed
> transaction."

## ⚠ SIGNAL-COUNT DISAGREEMENT — read before drafting §2

This CNCF document's signal list (metrics, logs, traces, profiles, dumps) **differs from
OpenTelemetry's** (traces, metrics, logs, baggage — see `opentelemetry-signals-2026-08-23.md`),
and also differs from the OTel primer's own passing list of three (traces, metrics, logs).

Ch 18 §2's Fixed Point "four signals, not three" is a claim about **OpenTelemetry's Signals page
specifically** and must be attributed that way. Do not write "the four signals" as though it were a
universal or CNCF-wide taxonomy — this snapshot shows it is not. A distractor built on "profiles"
is now sourced.

## RED and USE

The whitepaper references both methods by name and links out to them. It does **not** define
either. Its RED link points to the Weaveworks blog (host now defunct); its USE link points to
`https://www.brendangregg.com/usemethod.html`. See `use-method-brendan-gregg-2026-08-31.md` and
`red-method-tom-wilkie-2026-08-31.md`.
