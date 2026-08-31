---
source_url: "https://prometheus.io/docs/practices/pushing/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — pushing metrics practices"
objectives_covered: ["D4.1"]
concepts_covered: ["pushgateway", "pull-model", "batch-jobs", "scraping"]
---
# Prometheus — When to use the Pushgateway

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

This is the sharp version of Ch 18 Fixed Point 3 and trap #93. The already-cached
`prometheus-overview-2026-08-23.md` says pushing "is supported via an intermediary gateway"; this
page says how narrow that is, in the project's own voice.

## What it is

> "The Pushgateway is an intermediary service which allows you to push metrics from jobs which
> cannot be scraped."

## How narrow the use case is

> "We only recommend using the Pushgateway in certain limited cases."

> "The only valid use case for the Pushgateway is for capturing the outcome of a service-level
> batch job."

> "A 'service-level' batch job is one which is not semantically related to a specific machine or job
> instance."

## Drafting note for §4

"The only valid use case" is a stronger and more quotable claim than the overview's "short-lived
jobs," and it builds a better distractor set: an item can now offer *plausible* push scenarios
(a long-running service that would rather push; a job tied to one specific machine) that the source
itself rules out. Both phrasings are cached and both are verbatim; §4 may use either, but the Fixed
Point should carry this one.

The figure spec for `ch18-fig04-prometheus-pull-architecture` calls for Pushgateway drawn as a
"visibly narrow" single inbound path. This snapshot is the justification for that visual choice —
it is not stylistic emphasis, it is what the source says.
