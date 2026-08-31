---
source_url: "https://prometheus.io/docs/introduction/glossary/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Prometheus project (CNCF) — official glossary"
objectives_covered: ["D4.1"]
concepts_covered: ["exporters", "client-libraries", "pushgateway", "alertmanager", "target", "endpoint", "job", "instance", "sample", "time-series", "promql", "silence", "notification"]
---
# Prometheus — Glossary

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Highest-yield single page for Ch 18 §4, which the outline rates the densest sourced section in the
chapter. Ten of §4's introduced terms are defined here in the project's own words.

## Components

> **Exporter** — "An exporter is a binary running alongside the application you want to obtain
> metrics from."

> **Client library** — "A client library is a library in some language (e.g. Go, Java, Python,
> Ruby) that makes it easy to directly instrument your code."

> **Pushgateway** — "The Pushgateway persists the most recent push of metrics from batch jobs."

> **Alertmanager** — "The Alertmanager takes in alerts, aggregates them into groups, de-duplicates,
> applies silences, throttles, and then sends out notifications."

## What gets scraped

> **Target** — "A target is the definition of an object to scrape."

> **Endpoint** — "A source of metrics that can be scraped, usually corresponding to a single
> process."

> **Job** — "A collection of targets with the same purpose, for example monitoring a group of like
> processes replicated for scalability or reliability, is called a job."

> **Instance** — "An instance is a label that uniquely identifies a target in a job."

## Data

> **Sample** — "A sample is a single value at a point in time in a time series."

> **Time series** — "Prometheus time series are streams of timestamped values belonging to the same
> metric and the same set of labeled dimensions."

> **PromQL** — "PromQL is the Prometheus Query Language."

## Alerting

> **Silence** — "A silence in the Alertmanager prevents alerts, with labels matching the silence,
> from being included in notifications."

> **Notification** — "A notification represents a group of one or more alerts, and is sent by the
> Alertmanager to email, Pagerduty, Slack etc."

## Drafting note for §4

**Exporter vs client library is the discrimination worth teaching**, and this page makes it in one
line each: a client library instruments *your* code from the inside; an exporter is a separate
binary that gets metrics out of something you did not write. That is the same instrumentation /
backend separability §8 pays off, appearing a third time.

**Target, endpoint, job and instance are scope creep for KCNA.** They are cached for accuracy if
§4's figure needs correct labels (`ch18-fig04-prometheus-pull-architecture` shows Prometheus
scraping targets). Do not teach the four as vocabulary and do not grade them.
