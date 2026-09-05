---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/deployment/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project documentation (kubernetes.io) — Deployment concept page, section 'Writing a Deployment Spec'; text taken verbatim from the page source at github.com/kubernetes/website, content/en/docs/concepts/workloads/controllers/deployment.md (main branch), because the rendered page truncates before this section when fetched"
objectives_covered: ["D1.1"]
concepts_covered: ["pod-template", "podtemplatespec", "deployment", "selector-template-agreement", "selector-immutability", "deployment-strategy", "rolling-update"]
---

# Deployments — Writing a Deployment Spec (Pod Template · Selector · Strategy)

## Pod Template

"The `.spec.template` is a Pod template. It has exactly the same schema as a Pod, except it is nested and does not have an `apiVersion` or `kind`."

"In addition to required fields for a Pod, a Pod template in a Deployment must specify appropriate labels and an appropriate restart policy."

"Only a `.spec.template.spec.restartPolicy` equal to `Always` is allowed, which is the default if not specified."

## Selector

"Also note that `.spec.selector` is immutable after creation of the Deployment in `apps/v1`."

## Strategy

"`RollingUpdate` is the default value."
