---
source_url: "https://knative.dev/docs/serving/autoscaling/"
fetched_at: "2026-08-31T09:52:00-0400"
authority: "Knative project (CNCF graduated)"
objectives_covered: ["D4.2"]
concepts_covered: ["scale-to-zero", "knative-serving", "serverless"]
---
# Knative Serving — Autoscaling (knative.dev/docs/serving/autoscaling/)

Sources §6's Fixed Point (the scale-to-zero LIFECYCLE) and the figure
`ch17-fig07-scale-to-zero-and-the-knative-service`.

## What the autoscaler is — verbatim

> "Knative Serving provides automatic scaling, or _autoscaling_, for applications
> to match incoming demand."

## The default autoscaler — verbatim

> "This is provided by default, by using the Knative Pod Autoscaler (KPA)."

## Scale to zero — verbatim

> "If an application is receiving no traffic and scale to zero is enabled,
> Knative Serving scales the application down to zero replicas."

## Alternative autoscaler — verbatim fragment

> "Configure your Knative deployment to use the Kubernetes Horizontal Pod
> Autoscaler (HPA) instead of the default KPA."

## Not stated on this page

The page does not use the phrase "request-driven scaling model".

---
DRAFTING NOTE (not from source): the KPA-vs-HPA choice is a real fact but is
arguably above associate tier. It IS however a clean, sourced bridge from §6 to
§7 ("Ch 17 §7 — four things that scale" is already a listed cross-bearing out of
§6), and it reinforces §7's taxonomy rather than complicating it. Optional; see
Notes 8.
