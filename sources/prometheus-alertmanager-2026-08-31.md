---
source_url: "https://prometheus.io/docs/alerting/latest/alertmanager/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — Alertmanager documentation"
objectives_covered: ["D4.1"]
concepts_covered: ["alertmanager", "grouping", "inhibition", "silencing", "routing", "receivers"]
---
# Prometheus — Alertmanager

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## What it does

> "The Alertmanager handles alerts sent by client applications such as the Prometheus server. It
> takes care of deduplicating, grouping, and routing them to the correct receiver integration such
> as email, PagerDuty, or OpsGenie. It also takes care of silencing and inhibition of alerts."

## The four functions

> **Grouping** — "Grouping categorizes alerts of similar nature into a single notification."

> **Inhibition** — "Inhibition is a concept of suppressing notifications for certain alerts if
> certain other alerts are already firing."

> **Silencing** — "Silences are a straightforward way to simply mute alerts for a given time."

> **Routing** — notifications are directed to "the correct receiver integration such as email,
> PagerDuty, or OpsGenie."

## Drafting note for §4

**Direction of the arrow, again.** The opening sentence says Alertmanager "handles alerts *sent by*
client applications such as the Prometheus server" — so Prometheus **pushes** to Alertmanager, while
it **pulls** from targets. §4 is organised around arrow direction; this is the one place inside
Prometheus's own architecture where the arrow reverses, and a reader who has just learned "Prometheus
pulls" can be tripped by it. Worth one explicit sentence so it reads as a distinction rather than a
contradiction.

Grouping / inhibition / silencing are **below KCNA surface**. Name Alertmanager and what it is for;
do not teach the four functions and do not grade them.
