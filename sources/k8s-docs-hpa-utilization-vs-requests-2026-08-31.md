---
source_url: "https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D4.1", "D2.3"]
concepts_covered: ["utilization-relative-to-requests", "metrics-api", "metrics-server", "hpa", "resource-requests"]
---
# HorizontalPodAutoscaler — utilization is a percentage of the *request*

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

> **WHY THIS SNAPSHOT EXISTS.** Stage 1 did not flag this as a gap, but a corpus search found that
> **"utilization relative to requests" had no source anywhere in the 276 cached files.** It is
> pinned into Ch 18 §3 by two shipped chapters (`chapter-05:969`, `chapter-17:1387`), and it is
> graded three times — Soundings Q4, Checkpoint 1 item 4 (`*[retrieval: ch5]*`), and one of the
> four interleaved Practice items. It was about to be drafted from memory. It is now sourced.

## The denominator

> "Then, if a target utilization value is set, the controller calculates the utilization value as a
> percentage of the equivalent resource request on the containers in each Pod."

*(Editorial: inline documentation links removed from the sentence above; wording otherwise
unaltered.)*

## What happens with no request set

> "Please note that if some of the Pod's containers do not have the relevant resource request set,
> CPU utilization for the Pod will not be defined and the autoscaler will not take any action for
> that metric."

## Where the numbers come from

> "The common use for HorizontalPodAutoscaler is to configure it to fetch metrics from aggregated
> APIs (`metrics.k8s.io`, `custom.metrics.k8s.io`, or `external.metrics.k8s.io`). The
> `metrics.k8s.io` API is usually provided by an add-on named Metrics Server, which needs to be
> launched separately."

## The scaling algorithm

> `desiredReplicas = ceil[ currentReplicas × ( currentMetricValue / desiredMetricValue ) ]`

## Drafting note for §3

**The second quote is the payoff.** The outline asks §3 to pay off the denominator "concretely: the
number an autoscaler and a dashboard both report is a ratio, and the denominator is what the Pod
*asked for*, not what the node has." The no-request-set sentence proves it from the other side — a
Pod with no request has **no defined utilization at all**, which is only possible if the request is
the denominator. That is a better teaching move than restating the ratio, and it is sourced.

**The third quote is a bonus for §3's other half.** "which needs to be launched separately" is
Kubernetes' own statement of the Ch 10 §3 named pattern, arriving from the autoscaling side rather
than the `kubectl top` side. §3 may use it, but the pattern phrase itself —
***an object without its component does nothing*** — is the book's and must be quoted verbatim from
the ledger, never paraphrased from this page. See the B7 errata block.

**Do not draft the algorithm.** Cached for accuracy only. It is not KCNA surface and the outline
lists no objective for it.
