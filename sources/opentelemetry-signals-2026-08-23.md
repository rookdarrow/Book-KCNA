---
source_url: "https://opentelemetry.io/docs/concepts/signals/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4 Observability"]
concepts_covered: ["observability", "signals", "traces", "metrics", "logs", "baggage"]
---
# OpenTelemetry — Signals (opentelemetry.io/docs/concepts/signals/)

Signals are system outputs that describe the underlying activity of the operating system and applications running on a platform. A signal can be something you want to measure at a specific point in time, like temperature or memory usage, or an event that goes through the components of your distributed system that you'd like to trace.

OpenTelemetry currently supports:
- **Traces** — the path of a request through your application.
- **Metrics** — a measurement captured at runtime.
- **Logs** — a recording of an event.
- **Baggage** — contextual information that is passed between signals.
