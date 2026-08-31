---
source_url: "https://opentelemetry.io/docs/collector/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["otel-collector", "vendor-agnostic", "telemetry-pipeline", "agent-vs-collector", "backends"]
---
# OpenTelemetry Collector

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Cached to close Ch 18 §2's blocking gap. Shipped Ch 17's Voyage Ahead already promised the reader
"one collector," so the term is not droppable.

## What it is

> "The OpenTelemetry Collector offers a vendor-agnostic implementation of how to receive, process
> and export telemetry data."

> "Vendor-agnostic way to receive, process and export telemetry data."

## Why use one

> "Removes the need to run, operate, and maintain multiple agents/collectors"

> "Supports open source observability data formats (e.g. Jaeger, Prometheus, Fluent Bit, etc.)
> sending to one or more open source or commercial backends"

> "In general we recommend using a collector alongside your service, since it allows your service
> to offload data quickly and the collector can take care of additional handling like retries,
> batching, encryption or even sensitive data filtering."

## Design objectives

> **Usability** — "Reasonable default configuration, supports popular protocols, runs and collects
> out of the box."

> **Performance** — "Highly stable and performant under varying loads and configurations."

> **Observability** — "An exemplar of an observable service."

> **Extensibility** — "Customizable without touching the core code."

> **Unification** — "Single codebase, deployable as an agent or collector with support for traces,
> metrics, and logs."

## ⚠ NOT CAPTURED — do not name the pipeline components

The words **receiver**, **processor** and **exporter** as named pipeline stages were not captured
verbatim from this page. §2 may say the Collector "receives, processes and exports" telemetry —
that phrasing is verbatim above — but must **not** present receivers/processors/exporters as a
named three-part taxonomy without a re-fetch. See manifest gap G-18c.

## Drafting note for §2 and §8

The Unification objective is the sourced version of §8's second synthesis beat: one codebase, three
signal types, deployable in two shapes. And "sending to one or more open source or commercial
backends" is the sourced separability claim — instrumentation and backend are different things,
which is the shape §8 says recurred all chapter (OTel exports / Jaeger receives; Prometheus stores /
Grafana reads; kubelet writes / agent ships).
