---
source_url: "https://prometheus.io/docs/concepts/data_model/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["time-series", "metric-labels", "sample", "cardinality"]
---
# Prometheus — Data model

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Time series

> "Prometheus fundamentally stores all data as time series: streams of timestamped values belonging
> to the same metric and the same set of labeled dimensions."

## Identity — the sourced basis for Ch 18 §3's cardinality mechanic

> "Every time series is uniquely identified by its metric name and optional key-value pairs called
> labels."

> "The change of any label's value, including adding or removing labels, will create a new time
> series."

## Samples

> "Each sample consists of: a float64 or native histogram value [and] a millisecond-precision
> timestamp."

## Drafting note for §3

These two sentences together *are* the cardinality mechanic, stated as identity rather than as a
warning: a metric plus its label set defines the series, so changing a label value defines a
different one. §3 can teach cardinality as a consequence of the data model rather than as a rule to
memorise — which is the difference between a 🔭 Closer Look that earns its place and one that reads
as trivia. The operational warning is in
`prometheus-naming-labels-cardinality-2026-08-31.md`.
