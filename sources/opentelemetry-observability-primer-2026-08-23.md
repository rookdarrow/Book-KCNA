---
source_url: "https://opentelemetry.io/docs/concepts/observability-primer/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4 Observability"]
concepts_covered: ["observability", "instrumentation", "logs", "spans", "distributed-traces", "metrics", "sli", "slo", "reliability"]
---
# OpenTelemetry — Observability primer (opentelemetry.io/docs/concepts/observability-primer/)

## What is observability?
Observability lets you understand a system from the outside by letting you ask questions about that system without knowing its inner workings. Furthermore, it allows you to easily troubleshoot and handle novel problems, that is, "unknown unknowns". It also helps you answer the question "Why is this happening?" To ask those questions about your system, your application must be properly instrumented. That is, the application code must emit signals such as traces, metrics, and logs. An application is properly instrumented when developers don't need to add more instrumentation to troubleshoot an issue, because they have all of the information they need.

## Reliability and metrics
Telemetry refers to data emitted from a system and its behavior. The data can come in the form of traces, metrics, and logs. Reliability answers the question: "Is the service doing what users expect it to be doing?" Metrics are aggregations over a period of time of numeric data about your infrastructure or application. Examples include: system error rate, CPU utilization, and request rate for a given service. An SLI, or Service Level Indicator, represents a measurement of a service's behavior. A good SLI measures your service from the perspective of your users. An SLO, or Service Level Objective, is the means by which reliability is communicated to an organization/other teams. This is accomplished by attaching one or more SLIs to business value.

## Understanding distributed tracing
A log is a timestamped message emitted by services or other components. Unlike traces, they aren't necessarily associated with any particular user request or transaction. Logs are not extremely useful for tracking code execution on their own, as they typically lack contextual information; they become far more useful when they are included as part of a span, or when they are correlated with a trace and a span.

A span represents a unit of work or operation. Spans track specific operations that a request makes, painting a picture of what happened during the time in which that operation was executed. A span contains name, time-related data, structured log messages, and other metadata (that is, attributes) to provide information about the operation it tracks.

A distributed trace, more commonly known as a trace, records the paths taken by requests (made by an application or end-user) as they propagate through multi-service architectures, like microservice and serverless applications. A trace is made of one or more spans. The first span represents the root span; each root span represents a request from start to finish. The spans underneath the parent provide a more in-depth context of what occurs during a request.
