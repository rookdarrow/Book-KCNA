---
source_url: "https://opentelemetry.io/docs/concepts/signals/baggage/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "OpenTelemetry project (CNCF)"
objectives_covered: ["D4.1"]
concepts_covered: ["baggage", "signals", "context-propagation", "span-attributes"]
---
# OpenTelemetry — Baggage

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Baggage is Ch 18's Fixed Point 2 (the fourth signal, the one candidates drop) and a graded element
in Checkpoint 2. The corpus previously carried one sentence on it. This snapshot is the page.

## Definition

> "Contextual information that is passed between signals."

> Baggage is "a key-value store, which means it lets you propagate any data you like alongside
> context."

## What it is for

> "Baggage is best used to include information typically available only at the start of a request
> further downstream."

Examples the page gives: > "Account Identification, User IDs, Product IDs, and origin IPs."

## Propagation

> "Baggage means you can pass data across services and processes, making it available to add to
> traces, metrics, or logs in those services."

## Baggage is NOT span attributes

> "An important thing to note about baggage is that it is a separate key-value store and is
> unassociated with attributes on spans, metrics, or logs without explicitly adding them."

## Security caution

> "Sensitive Baggage items can be shared with unintended resources, like third-party APIs...making
> it visible to anyone inspecting your network traffic."

## Drafting note for §2 and §5

The "unassociated with attributes... without explicitly adding them" sentence is the sourced answer
to *why* baggage is a separate signal rather than a property of spans — which is exactly the fact
that makes trap #89 defensible rather than arbitrary. It is also the cleanest way to make §5's
return of baggage land: the thing being propagated is a store, not a field on the span.

The security caution is **not** exam surface and should not be graded. It is available if §2 wants
one concrete beat to keep a naming section from reading as a list.
