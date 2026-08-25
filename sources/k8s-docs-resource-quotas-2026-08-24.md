---
source_url: "https://kubernetes.io/docs/concepts/policy/resource-quotas/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/policy/resource-quotas.md"
fetched_at: "2026-08-24T18:57:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["resource-quota", "namespaced-vs-cluster-scoped", "admission-control", "compute-resource-quota", "object-count-quota", "storage-quota"]
closes_gap: "ch-08 outline Open Question #3 (BLOCKING), first half. Previously nothing cached stated what a quota counts, or the rule that a quota'd namespace forces Pods to declare requests/limits."
scope_note: "Quota scopes, scope selectors and priority-class quota were deliberately NOT extracted -- above associate tier, per the outline's scope guard."
---
# Resource Quotas

> **Extraction note.** Passages marked **[VERBATIM]** are safe to cite. The compute and
> storage resource-name lists are transcribed enumerations of the source's tables; the
> per-row DESCRIPTION cells were **not** verbatim-verified in this pass and are marked
> **[NAMES ONLY]**. Do not quote row descriptions as source sentences.

## What it is

**[VERBATIM]**

> "When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources."

> "A resource quota, defined by a ResourceQuota object, provides constraints that limit aggregate resource consumption per namespace."

## How it works

**[VERBATIM]**

> "A cluster administrator creates at least one ResourceQuota for each namespace."

> "Users create resources (pods, services, etc.) in the namespace, and the quota system tracks usage to ensure it does not exceed hard resource limits."

> "If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden`."

> "If quotas are enabled in a namespace for resource such as `cpu` and `memory`, users must specify requests or limits for those values when they define a Pod."

## The rule that makes a valid Pod stop being valid

**[VERBATIM]**

> "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients, **must** specify either `requests` or `limits` for that resource, for every new Pod you submit. If you don't, the control plane may reject admission for that Pod."

> "You can use a LimitRange to automatically set a default request for these resources."

## Enabling

**[VERBATIM]**

> "ResourceQuota support is enabled by default for many Kubernetes distributions. It is enabled when the API server `--enable-admission-plugins=` flag has `ResourceQuota` as one of its arguments."

> "A resource quota is enforced in a particular namespace when there is a ResourceQuota in that namespace."

## Compute Resource Quota -- [NAMES ONLY]

`limits.cpu`, `limits.memory`, `requests.cpu`, `requests.memory`, `hugepages-<size>`,
`cpu` (alias for `requests.cpu`), `memory` (alias for `requests.memory`)

## Quota for storage -- [NAMES ONLY]

`requests.storage`, `persistentvolumeclaims`,
`<storage-class-name>.storageclass.storage.k8s.io/requests.storage`,
`<storage-class-name>.storageclass.storage.k8s.io/persistentvolumeclaims`

## Quota on object count -- [NAMES ONLY]

Syntax: `count/<resource>.<group>` for non-core API groups; `count/<resource>` for core
API group resources.

Countable resources include: `count/pods`, `count/persistentvolumeclaims`,
`count/services`, `count/secrets`, `count/configmaps`, `count/deployments.apps`,
`count/replicasets.apps`, `count/statefulsets.apps`, `count/jobs.batch`,
`count/cronjobs.batch`

## Quota and Cluster Capacity

**[VERBATIM, with an elision in the fetch -- marked]**

> "ResourceQuotas are independent of the cluster capacity[...]if you add nodes to your cluster, this does *not* automatically give each namespace the ability to consume more resources."

---

NOT IN THIS SNAPSHOT: quota scopes and scope selectors, priority-class quota, the
cross-namespace pod affinity quota, and the full countable-resource roster. All are above
associate tier.
