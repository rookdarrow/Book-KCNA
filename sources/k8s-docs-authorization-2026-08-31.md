---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/authorization/"
fetched_at: "2026-08-31T10:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["authorization-mode", "rbac", "kubectl-auth-can-i", "rule-verb-resource"]
---
# Authorization (kubernetes.io/docs/reference/access-authn-authz/authorization/)

This is the source for §3's one-clause ABAC disposal (Open question #8) — the clause that must be written before ABAC may be used as a distractor.

## Default deny

"All parts of an API request must be allowed by some authorization mechanism in order to proceed."

## How multiple authorizers combine

"[Each authorizer] is checked in sequence. If any authorizer approves or denies a request, that decision is immediately returned and no other authorizer is consulted. If all modules have no opinion on the request, then the request is denied."

## Request attributes considered

Authorization decisions consider these API request attributes: the user, group membership, extra metadata, whether the request is for an API resource, the request path, the API request verb (`get`, `list`, `create`, `update`, `patch`, `watch`, `delete`, `deletecollection`), the HTTP request verb, the resource name/ID, the subresource, the namespace, and the API group.

## Authorization modules

**Node** — "A special-purpose authorization mode that grants permissions to kubelets based on the pods they are scheduled to run."

**ABAC** — "Kubernetes ABAC mode defines an access control paradigm whereby access rights are granted to users through the use of policies which combine attributes together."

**RBAC** — "Kubernetes RBAC is a method of regulating access to computer or network resources based on the roles of individual users within an enterprise."

**Webhook** — "Kubernetes webhook mode for authorization makes a synchronous HTTP callout, blocking the request until the remote HTTP service responds to the query."

## Checking API access

Users can check their own authorization with `kubectl auth can-i`, which queries the authorization layer to determine whether an action is permitted. The `--as` flag impersonates another user or service account, so an administrator can check what another principal is permitted to do.

> FIDELITY NOTE: the "Request attributes considered" and "Checking API access" paragraphs are **condensed**, not verbatim; the four module descriptions and the two sentences above them are the page's own words. Do not quote the condensed paragraphs as documentation sentences.
