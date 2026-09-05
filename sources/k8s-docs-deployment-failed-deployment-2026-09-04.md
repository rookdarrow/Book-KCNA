---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#failed-deployment"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/controllers/deployment.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched from the kubernetes/website source markdown that kubernetes.io renders"
objectives_covered: ["D2.3", "D1.1"]
concepts_covered: ["replicafailure-condition", "failedcreate", "admission-rejection-versus-pod-failure", "progressdeadlineexceeded", "deployment-stuck-causes"]
closes_gap: "ch-13 sec.2 RESEARCH GAP: no cached snapshot showed where a refused Pod creation is recorded when a controller, not a person, issued the create. This section shows the API server's refusal ('is forbidden: exceeded quota') surfacing as a ReplicaFailure condition with reason FailedCreate, with the refusal message copied verbatim — and no Pod object anywhere in the example."
---

# Deployments — the "Failed Deployment" section

> All passages below are **[VERBATIM]** from the `### Failed Deployment` section.

## Why a rollout gets stuck

"Your Deployment may get stuck trying to deploy its newest ReplicaSet without ever completing. This can occur due to some of the following factors:"

- "Insufficient quota"
- "Readiness probe failures"
- "Image pull errors"
- "Insufficient permissions"
- "Limit ranges"
- "Application runtime misconfiguration"

## Where a refused create is recorded

"You may experience transient errors with your Deployments, either due to a low timeout that you have set or due to any other kind of error that can be treated as transient. For example, let's suppose you have insufficient quota. If you describe the Deployment you will notice the following section:"

```
kubectl describe deployment nginx-deployment
```

"The output is similar to this:"

```
<...>
Conditions:
  Type            Status  Reason
  ----            ------  ------
  Available       True    MinimumReplicasAvailable
  Progressing     True    ReplicaSetUpdated
  ReplicaFailure  True    FailedCreate
<...>
```

"If you run `kubectl get deployment nginx-deployment -o yaml`, the Deployment status is similar to this:"

```
  - lastTransitionTime: 2016-10-04T12:25:39Z
    lastUpdateTime: 2016-10-04T12:25:39Z
    message: 'Error creating: pods "nginx-deployment-4262182780-" is forbidden: exceeded quota:
      object-counts, requested: pods=1, used: pods=3, limited: pods=2'
    reason: FailedCreate
    status: "True"
    type: ReplicaFailure
```

## What this supports

- The refusal is the API server's own admission message ("is forbidden: exceeded quota"), and it is recorded on the workload objects, not on a Pod — the example contains no Pod name because no Pod was created. The named object in the message is the ReplicaSet (`nginx-deployment-4262182780`) whose create attempt failed; the Deployment surfaces it as a `ReplicaFailure` condition with reason `FailedCreate`.
- `Progressing` still reads `True`/`ReplicaSetUpdated` at that moment: the Deployment does not fail loudly on its own. The refusal is visible only if you read the conditions, or describe the ReplicaSet that tried.
- The "six causes" list is the same one Chapter 6 and Chapter 13 §3 cite from k8s-docs-deployment-spec-fields-2026-08-24; this snapshot carries it verbatim from the concept page as well.
