---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/rbac/"
fetched_at: "2026-09-04T09:10:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["rolebinding", "clusterrole", "binding-determines-scope", "four-way-binding-matrix"]
---
# Using RBAC Authorization — RoleBinding referencing a ClusterRole (kubernetes.io/docs/reference/access-authn-authz/rbac/)

Companion to `k8s-docs-rbac-2026-08-23.md` and `k8s-docs-rbac-depth-2026-08-31.md`. This snapshot carries the two sentences from the current page that state, in the documentation's own words, that a RoleBinding referencing a ClusterRole grants that ClusterRole's permissions only to resources *inside the RoleBinding's namespace*. That is the sentence Ch 12 §3's derivation rests on: a rule about a cluster-scoped resource has no namespace to land in when it is bound by a RoleBinding.

## RoleBinding and ClusterRoleBinding

"A role binding grants the permissions defined in a role to a user or set of users. It holds a list of *subjects* (users, groups, or service accounts), and a reference to the role being granted. A RoleBinding grants permissions within a specific namespace whereas a ClusterRoleBinding grants that access cluster-wide."

"A RoleBinding may reference any Role in the same namespace. Alternatively, a RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding. If you want to bind a ClusterRole to all the namespaces in your cluster, you use a ClusterRoleBinding."

"A RoleBinding can also reference a ClusterRole to grant the permissions defined in that ClusterRole to resources inside the RoleBinding's namespace. This kind of reference lets you define a set of common roles across your cluster, then reuse them within multiple namespaces."

"For instance, even though the following RoleBinding refers to a ClusterRole, "dave" (the subject, case sensitive) will only be able to read Secrets in the "development" namespace, because the RoleBinding's namespace (in its metadata) is "development"."

> NOTE FOR DRAFTING: the page does not spell out the cluster-scoped corollary in a single sentence. The corollary — that a ClusterRole rule over a cluster-scoped resource (Node, PersistentVolume, Namespace) grants nothing when the ClusterRole is bound by a RoleBinding — follows from "to resources inside the RoleBinding's namespace" together with the fact that a cluster-scoped resource is inside no namespace. Cite this snapshot for the premise; the corollary is the chapter's derivation.
