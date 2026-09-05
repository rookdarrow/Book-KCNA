---
source_url: "https://kyverno.io/docs/policy-types/cluster-policy/validate/"
fetched_at: "2026-09-04T09:20:00-0400"
authority: "Kyverno project documentation (kyverno.io/docs) — the project's own reference for its policy rule types; Kyverno is a CNCF project"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["kyverno", "validate-mutate-generate", "policy-engine", "admission-time-vs-runtime"]
---
# Kyverno — what the four rule types do (kyverno.io/docs/policy-types/)

Companion to `kyverno-overview-2026-08-23.md`, which lists the verbs validate, mutate, generate and clean up without defining them. Each definition below is quoted from the opening of the corresponding page of the project's documentation.

## Validate (https://kyverno.io/docs/policy-types/cluster-policy/validate/)

"Validation rules are probably the most common and practical types of rules you will be working with, and the main use case for admission controllers such as Kyverno."

"The FailureAction attribute controls admission control behaviors for resources that are not compliant with a policy. If the value is set to Enforce, resource creation or updates are blocked when the resource does not comply. When the value is set to Audit, a policy violation is logged in a PolicyReport or ClusterPolicyReport but the resource creation or update is allowed."

## Mutate (https://kyverno.io/docs/policy-types/cluster-policy/mutate/)

"A `mutate` rule can be used to modify matching resources and is written as either a RFC 6902 JSON Patch or a strategic merge patch."

## Generate (https://kyverno.io/docs/policy-types/cluster-policy/generate/)

"A generate rule can be used to create new Kubernetes resources in response to some other event including things like resource creation, update, or delete, or even by creating or updating a policy itself."

Among the use cases the page lists: "Create resources like a NetworkPolicy, ResourceQuota, and RoleBinding when a new Namespace is created".

## Cleanup (https://kyverno.io/docs/policy-types/cleanup-policy/)

"Kyverno has the ability to cleanup (i.e., delete) existing resources in a cluster in two different ways. The first way is via a declarative policy definition in either a `CleanupPolicy` or `ClusterCleanupPolicy`."
