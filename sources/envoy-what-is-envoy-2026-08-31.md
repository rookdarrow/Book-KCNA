---
source_url: "https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy"
fetched_at: "2026-08-31T09:44:00-0400"
authority: "Envoy project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["envoy", "mesh-data-plane", "service-mesh", "sidecar-mode"]
---
# Envoy — What is Envoy (envoyproxy.io/docs/envoy/latest/intro/what_is_envoy)

Envoy is named in kb_tags and in three §5 traps but had no snapshot of its own.

## What Envoy is — verbatim

> "Envoy is an L7 proxy and communication bus designed for large modern service
> oriented architectures."

## Out of process architecture — verbatim

> "Envoy is a self contained process that is designed to run alongside every
> application server. All of the Envoys form a transparent communication mesh in
> which each application sends and receives messages to and from localhost and is
> unaware of the network topology."

## Language independence — verbatim fragments

> "Envoy works with any application language"

> "Envoy can be deployed and upgraded quickly across an entire infrastructure
> transparently"

[Paraphrase, NOT verbatim: the document positions Envoy as a language-agnostic
proxy that operates alongside applications to form a service mesh.]

---
DRAFTING NOTE (not from source): "each application sends and receives messages to
and from localhost and is unaware of the network topology" is Envoy's own
statement of the without-code-changes property, from the data plane's side. It
pairs directly with Soundings Q4, which tests what a sidecar shares with the
container beside it — the answer being the Pod's network namespace, i.e. localhost.
