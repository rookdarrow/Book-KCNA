---
source_url: "https://docs.fluentbit.io/manual/about/what-is-fluent-bit"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Fluent Bit project (Fluent, CNCF graduated)"
objectives_covered: ["D4 Observability"]
concepts_covered: ["fluent-bit", "fluentd", "log-processor", "telemetry-agent", "data-pipeline", "input", "parser", "filter", "buffer", "router", "output"]
---
# Fluent Bit (docs.fluentbit.io)

Fluent Bit is an open source telemetry agent that processes logs, metrics, traces, and profiles. Fluent Bit was created in 2014 by Eduardo Silva as a lightweight log processor, developed by the Fluentd team at Treasure Data for constrained environments such as embedded Linux; it is a sub-project of Fluentd, which is a CNCF graduated project. Both are commonly deployed on Kubernetes as node-level logging agents (DaemonSets) that collect container logs from each node and forward them to a backend.

## Data pipeline
The Fluent Bit data pipeline incorporates several specific concepts. Data processing flows through the pipeline following these concepts in order: **Input** — input plugins gather information from different sources; some plugins collect data from log files, and others gather metrics information from the operating system. **Parser** — parsers convert unstructured data to structured data. **Filter** — filters let you alter the collected data before delivering it to a destination. **Buffer** — the buffering phase provides a unified and persistent mechanism to store your data, using the primary in-memory model or the file system-based mode. **Router** — routing lets you route your data through filters, and then to one or multiple destinations; the router relies on the concept of tags and matching rules. **Output** — output plugins let you define destinations for your data; common destinations are remote services, local file systems, or other standard interfaces.
