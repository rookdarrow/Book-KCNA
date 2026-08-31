---
source_url: "https://karpenter.sh/docs/concepts/"
fetched_at: "2026-08-31T09:50:00-0400"
authority: "Karpenter project (karpenter.sh; repository kubernetes-sigs/karpenter)"
objectives_covered: ["D4.2"]
concepts_covered: ["karpenter", "node-autoscaling", "cluster-autoscaler"]
---
# Karpenter — Documentation and Concepts (karpenter.sh/docs/, karpenter.sh/docs/concepts/)

Closes the outline's Karpenter gap. Karpenter was previously named in exactly one
clause of one snapshot.

## What Karpenter is — verbatim

> "Karpenter is an open-source node lifecycle management project built for
> Kubernetes."

## What Karpenter does — verbatim, the docs' own four bullets

> - "Watching for pods that the Kubernetes scheduler has marked as unschedulable"
> - "Evaluating scheduling constraints (resource requests, nodeselectors,
>   affinities, tolerations, and topology spread constraints) requested by the pods"
> - "Provisioning nodes that meet the requirements of the pods"
> - "Disrupting the nodes when the nodes are no longer needed"

## Summary statement — verbatim

> "Karpenter's job is to add nodes to handle unschedulable pods, schedule pods on
> those nodes, and remove the nodes when they are not needed."

## NodePool — verbatim

> "Karpenter defines a Custom Resource called a NodePool to specify configuration."

## Affiliation — what the source does and does not say

The site carries the footer "built with ❤️ at AWS" and "© 2026 Amazon.com, Inc.
or its affiliates." The upstream repository is `kubernetes-sigs/karpenter`.

**The site makes NO claim of CNCF membership, and states NO CNCF maturity level.**
The only governance statement located in any official source is on
kubernetes.io's node-autoscaling page: Karpenter and Cluster Autoscaler are "the
two Node autoscalers currently sponsored by SIG Autoscaling."

---
DRAFTING NOTE (not from source): this settles outline Open Question 5. Karpenter
may be named as a node autoscaler sponsored by Kubernetes SIG Autoscaling,
tagged to this snapshot and to `k8s-docs-node-autoscaling-2026-08-31.md`. It must
NOT be given a CNCF maturity level. Note also that "Karpenter defines a Custom
Resource called a NodePool" is a small, free bonus for §4/§9 — a fifth instance of
the pluggability shape, arriving in §7 — but the ordinal rule bars counting past
four, so if it is used at all it is used unnumbered.
