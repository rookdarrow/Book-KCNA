---
source_url: "https://opentelemetry.io/docs/concepts/instrumentation/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["instrumentation", "code-based-instrumentation", "zero-code-instrumentation", "signals", "telemetry"]
---
# OpenTelemetry — Instrumentation

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## Instrumentation as the precondition for observability

> "For a system to be observable, it must be instrumented: that is, code from the system's
> components must emit signals."

## Two kinds

> **Code-based** — "Allow you to get deeper insight and rich telemetry from your application
> itself"

> **Zero-code** — "Great for getting started, or when you can't modify the application you need to
> get telemetry out of"

> Zero-code instrumentation "provide[s] rich telemetry from libraries you use and/or the
> environment your application runs in"

## Drafting note for §1 and §5

The zero-code sentence is the clean, sourced bridge to Ch 17 §5's mesh telemetry: it is OTel's own
statement that useful telemetry can come from a system the application did not opt into. §5's
mandatory Ch 17 anchor ("sometimes you get spans without instrumenting anything") can lean on this
rather than on the mesh material alone.

Ch 18 §1's ★ Fixed Point candidate on "properly instrumented" is in the **primer**
(`opentelemetry-observability-primer-2026-08-23.md`), not here — that page carries the sentence
about developers not needing to add more instrumentation to troubleshoot. Use the primer for that
beat and this snapshot for the precondition and the two kinds.
