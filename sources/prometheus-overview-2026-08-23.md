---
source_url: "https://prometheus.io/docs/introduction/overview/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Prometheus project (CNCF)"
objectives_covered: ["D4 Observability"]
concepts_covered: ["prometheus", "metrics", "time-series", "promql", "pull-model", "exporters", "alertmanager", "pushgateway"]
---
# Prometheus Overview (prometheus.io/docs/introduction/overview/)

## What is Prometheus?
Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community. Prometheus joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes. Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.

## Features
A multi-dimensional data model with time series data identified by metric name and key/value pairs; PromQL, a flexible query language to leverage this dimensionality; no reliance on distributed storage — single server nodes are autonomous; time series collection happens via a pull model over HTTP; pushing time series is supported via an intermediary gateway; targets are discovered via service discovery or static configuration; multiple modes of graphing and dashboarding support.

## What are metrics?
In layperson terms, metrics are numeric measurements. Time series means that changes are recorded over time. What users want to measure differs from application to application. For a web server, it could be request times; for a database, it could be the number of active connections or active queries. Metrics play an important role in understanding why your application is working in a certain way.

## Components
The main Prometheus server which scrapes and stores time series data; client libraries for instrumenting application code; a push gateway for supporting short-lived jobs; special-purpose exporters for services like HAProxy, StatsD, Graphite, etc.; an alertmanager to handle alerts; various support tools. Most Prometheus components are written in Go, making them easy to build and deploy as static binaries.

## Architecture
Prometheus scrapes metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all scraped samples locally and runs rules over this data to either aggregate and record new time series from existing data or generate alerts. Grafana or other API consumers can be used to visualize the collected data.

## When does it fit? / When does it not fit?
Prometheus works well for recording any purely numeric time series. It fits both machine-centric monitoring as well as monitoring of highly dynamic service-oriented architectures. In a world of microservices, its support for multi-dimensional data collection and querying is a particular strength. Each Prometheus server is standalone, not depending on network storage or other remote services, so you can rely on it when other parts of your infrastructure are broken. Prometheus values reliability. If you need 100% accuracy, such as for per-request billing, Prometheus is not a good choice as the collected data will likely not be detailed and complete enough.
