---
source_url: "https://opentelemetry.io/docs/concepts/context-propagation/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["context-propagation", "context", "propagation", "trace-id", "span-id", "w3c-tracecontext", "baggage"]
---
# OpenTelemetry — Context Propagation

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Cached to close Ch 18 §5's blocking gap. Context propagation is the mechanism the whole section
rests on: it is the answer to Soundings Q7 (what five independent log files cannot do between them).

## Context

> "Context is an object that contains the information for the sending and receiving service, or
> execution unit, to correlate one signal with another."

## Propagation

> "Propagation is the mechanism that moves context between services and processes."

## Context propagation

> "With context propagation, signals (traces, metrics, and logs) can be correlated with each other,
> regardless of where they are generated."

> "Context propagation allows traces to build causal information about a system across services
> that are arbitrarily distributed across process and network boundaries."

## How the correlation is carried

> "Service A includes a trace ID and a span ID as part of the context. Service B uses these values
> to create a new span that belongs to the same trace."

## The wire format

> "The default propagator uses the headers specified by the W3C TraceContext specification."

The page gives the header shape as `<version>-<trace-id>-<parent-id>-<trace-flags>`.

## Baggage

> "Baggage allows you to propagate arbitrary key-value pairs."

## Drafting note for §5

"Arbitrarily distributed across process and network boundaries" is the sourced sentence that closes
the loop shipped Ch 17 opened ("Break a monolith into microservices and one request becomes
twenty"). The Service A / Service B sentence is concrete enough to carry the mechanism without a
code sample, which matters because B1 rates D4 recall-and-recognition and §5 must not drift into
implementation.

W3C TraceContext is **not** exam surface at KCNA level. Name it at most once; do not grade it.
