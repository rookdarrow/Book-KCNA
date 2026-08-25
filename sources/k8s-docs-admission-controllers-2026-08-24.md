---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/reference/access-authn-authz/admission-controllers.md"
fetched_at: "2026-08-24T18:56:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D1.2"]
concepts_covered: ["admission-controller", "mutating-admission", "validating-admission", "dynamic-admission-control", "resource-quota", "limit-range", "noderestriction"]
closes_gap: "ch-08 outline Open Question #2, secondary fetch. Supplies the mutating/validating distinction and the named built-in plugins sec.2 and sec.3 depend on."
---
# Admission Controllers Reference

> **Extraction note.** All passages below are **[VERBATIM]**.

## What are they?

> "Admission controllers are code within the Kubernetes API server that check the data arriving in a request to modify a resource."

> "Admission controllers apply to requests that create, delete, or modify objects."

> "Admission controllers do not (and cannot) block requests to read (get, watch or list) objects, because reads bypass the admission control layer."

> "Admission control mechanisms may be validating, mutating, or both. Mutating controllers may modify the data for the resource being modified; validating controllers may not."

## The two phases

> "In the first phase, mutating admission controllers are run. In the second phase, validating admission controllers are run."

> "If any of the controllers in either phase reject the request, the entire request is rejected immediately and an error is returned to the end-user."

## Why do I need them?

> "Several important features of Kubernetes require an admission controller to be enabled in order to properly support the feature. As a result, a Kubernetes API server that is not properly configured with the right set of admission controllers is an incomplete server and will not support all the features you expect."

## Selected built-in plugins

- **ResourceQuota** -- "This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the ResourceQuota object."
- **LimitRanger** -- "This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the LimitRange object."
- **NodeRestriction** -- "This admission controller limits the Node and Pod objects a kubelet can modify."
- **MutatingAdmissionWebhook** -- "This admission controller calls any mutating webhooks which match the request."
- **ValidatingAdmissionWebhook** -- "This admission controller calls any validating webhooks which match the request."

---

NOT IN THIS SNAPSHOT: the full plugin roster, plugin ordering, and enable/disable flag
syntax. All are above associate tier. The five entries above are the ones sec.2 and sec.3
name; the outline caps PSA and RBAC at one clause each.
