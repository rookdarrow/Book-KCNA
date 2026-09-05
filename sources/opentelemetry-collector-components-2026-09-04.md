---
source_url: "https://opentelemetry.io/docs/collector/architecture/"
fetched_at: "2026-09-04T17:30:00-0400"
authority: "OpenTelemetry project (CNCF) — Collector architecture page, with the component definitions from the Collector configuration page (https://opentelemetry.io/docs/collector/configuration/)"
objectives_covered: ["D4.1"]
concepts_covered: ["otel-collector", "pipeline", "receivers", "processors", "exporters", "connectors", "extensions"]
---
# OpenTelemetry Collector — pipeline components (receivers, processors, exporters)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> audit stage and must not be quoted as source text.

Fetched 2026-09-04 during the Ch 18 audit to close manifest gap G-18c. The earlier snapshot
`opentelemetry-collector-2026-08-31` carried an explicit guardrail: the words receiver, processor
and exporter as *named pipeline stages* had not been captured verbatim. They are captured here,
from the project's own documentation. Ch 18 §2 may now name the three.

## Architecture page — what a pipeline is (opentelemetry.io/docs/collector/architecture/)

> "A pipeline defines a path that data follows in the Collector: from reception, to processing
> (or modification), and finally to export."

> "Each pipeline includes the following: A set of receivers that collect the data. A series of
> optional processors that get the data from receivers and process it. A set of exporters which
> get the data from processors and send it outside the Collector."

## Configuration page — the component classes (opentelemetry.io/docs/collector/configuration/)

> "The structure of any Collector configuration file consists of four classes of pipeline
> components that access telemetry data"

> "Receivers collect telemetry from one or more sources. They can be pull or push based, and may
> support one or more data sources."

> "Processors take the data collected by receivers and modify or transform it before sending it
> to the exporters."

> "Exporters send data to one or more backends or destinations. Exporters can be pull or push
> based, and may support one or more data sources."

> "Connectors join two pipelines, acting as both exporter and receiver. A connector consumes data
> as an exporter at the end of one pipeline and emits data as a receiver at the beginning of
> another pipeline."

> "Extensions are optional components that expand the capabilities of the Collector to accomplish
> tasks not directly involved with processing telemetry data."

## Drafting note for Ch 18 §2

The three names map onto the verbatim "receive, process and export" definition already cached in
`opentelemetry-collector-2026-08-31`. Connectors and extensions are configuration-level detail and
are not KCNA surface; §2 names only receivers, processors and exporters, in one sentence, and
grades none of them.
