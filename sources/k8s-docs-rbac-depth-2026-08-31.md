---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/rbac/"
fetched_at: "2026-08-31T10:48:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["aggregated-clusterrole", "subjects-are-named-not-selected", "rule-verb-resource", "default-role-admin", "default-role-edit", "default-role-view", "binding-immutability", "least-privilege"]
---
# Using RBAC Authorization — depth passages (kubernetes.io/docs/reference/access-authn-authz/rbac/)

Companion to `k8s-docs-rbac-2026-08-23.md`, which carries the four API objects, the additive rule, the binding-immutability sentence and the four default roles at summary level. This snapshot carries the passages that chapter 12 §3 needs and that snapshot does not have. Transcribed from the page's markdown source; YAML examples omitted, Hugo shortcodes left in place where they sit inside a sentence.

## Referring to resources — resourceNames

"You can also refer to resources by name for certain requests through the `resourceNames` list. When specified, requests can be restricted to individual instances of a resource."

**Note:** "You cannot restrict **deletecollection** or top-level **create** requests by resource name. For **create**, this limitation is because the name of the new object may not be known at authorization time. However, the **create** limitation applies only to top-level resources, not subresources. For example, you can use the `resourceNames` field with `pods/exec`. If you restrict **list** or **watch** by `resourceName`, clients must include a `metadata.name` field selector in their **list** or **watch** request (that matches the specified `resourceName`) in order to be authorized. For example: `kubectl get configmaps --field-selector=metadata.name=my-configmap`"

## Aggregated ClusterRoles

"You can _aggregate_ several ClusterRoles into one combined ClusterRole. A controller, running as part of the cluster control plane, watches for ClusterRole objects with an `aggregationRule` set. The `aggregationRule` defines a label selector that the controller uses to match other ClusterRole objects that should be combined into the `rules` field of this one."

"If you create a new ClusterRole that matches the label selector of an existing aggregated ClusterRole, that change triggers adding the new rules into the aggregated ClusterRole."

"The default user-facing roles use ClusterRole aggregation. This lets you, as a cluster administrator, include rules for custom resources, such as those served by CustomResourceDefinitions or aggregated API servers, to extend the default roles."

"For example: the following ClusterRoles let the "admin" and "edit" default roles manage the custom resource named CronTab, whereas the "view" role can perform only read actions on CronTab resources. You can assume that CronTab objects are named `"crontabs"` in URLs as seen by the API server."

## Referring to subjects

"A RoleBinding or ClusterRoleBinding binds a role to subjects. Subjects can be group, users or ServiceAccounts."

"Kubernetes represents usernames as strings. These can be: plain names, such as "alice"; email-style names, like "bob@example.com"; or numeric user IDs represented as a string. It is up to you as a cluster administrator to configure the authentication modules so that authentication produces usernames in the format you want."

"In Kubernetes, Authenticator modules provide group information. Groups, like users, are represented as strings, and that string has no format requirements, other than that the prefix `system:` is reserved."

"ServiceAccounts have names prefixed with `system:serviceaccount:`, and belong to groups that have names prefixed with `system:serviceaccounts:`."

> NOTE FOR DRAFTING (§3, debt `chapter-04:839`): the docs state that subjects are *named strings*. They do **not** contain a sentence explaining *why* RBAC names subjects instead of selecting them. See § Gaps.

## Privilege escalation prevention and bootstrapping

"The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use."

### Restrictions on role creation or update

"You can only create/update a role if at least one of the following things is true:

1. You already have all the permissions contained in the role, at the same scope as the object being modified (cluster-wide for a ClusterRole, within the same namespace or cluster-wide for a Role).
2. You are granted explicit permission to perform the `escalate` verb on the `roles` or `clusterroles` resource in the `rbac.authorization.k8s.io` API group."

"For example, if `user-1` does not have the ability to list Secrets cluster-wide, they cannot create a ClusterRole containing that permission. To allow a user to create/update roles:

1. Grant them a role that allows them to create/update Role or ClusterRole objects, as desired.
2. Grant them permission to include specific permissions in the roles they create/update:
   * implicitly, by giving them those permissions (if they attempt to create or modify a Role or ClusterRole with permissions they themselves have not been granted, the API request will be forbidden)
   * or explicitly allow specifying any permission in a `Role` or `ClusterRole` by giving them permission to perform the `escalate` verb on `roles` or `clusterroles` resources in the `rbac.authorization.k8s.io` API group"

### Restrictions on role binding creation or update

"You can only create/update a role binding if you already have all the permissions contained in the referenced role (at the same scope as the role binding) *or* if you have been authorized to perform the `bind` verb on the referenced role. For example, if `user-1` does not have the ability to list Secrets cluster-wide, they cannot create a ClusterRoleBinding to a role that grants that permission. To allow a user to create/update role bindings:

1. Grant them a role that allows them to create/update RoleBinding or ClusterRoleBinding objects, as desired.
2. Grant them permissions needed to bind a particular role:
   * implicitly, by giving them the permissions contained in the role.
   * explicitly, by giving them permission to perform the `bind` verb on the particular Role (or ClusterRole)."

"When bootstrapping the first roles and role bindings, it is necessary for the initial user to grant permissions they do not yet have. To bootstrap initial roles and role bindings:

* Use a credential with the "system:masters" group, which is bound to the "cluster-admin" super-user role by the default bindings."

## Default roles and role bindings — the `admin`, `edit` and `view` Description cells, in full

**`admin`:** "If used in a **RoleBinding**, allows read/write access to most resources in a namespace, including the ability to create roles and role bindings within the namespace. This role does not allow write access to resource quota or to the namespace itself. This role also does not allow write access to EndpointSlices in clusters created using Kubernetes v1.22+. More information is available in the "Write Access for EndpointSlices" section."

**`edit`:** "This role does not allow viewing or modifying roles or role bindings. However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. This role also does not allow write access to EndpointSlices in clusters created using Kubernetes v1.22+. More information is available in the "Write Access for EndpointSlices" section."

**`view`:** "Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation)."

> ⚠ FACT-CHECK FOR §3 AND B1 TRAP #58. The `edit` role **does** allow *accessing* Secrets, per the sentence above; what it does not allow is viewing or modifying roles and role bindings. The book must not state that `edit` cannot read Secrets. `view` is the role that cannot. Trap #58 as inventoried ("`edit` can manage RBAC in its namespace → it cannot; `admin` can") is correct and is directly supported.

## Bootstrapping and auto-reconciliation

Default ClusterRoles and ClusterRoleBindings are labelled `kubernetes.io/bootstrapping=rbac-defaults`. The API server reconciles the defaults at startup, restoring missing permissions and subjects. Auto-reconciliation can be disabled per object by setting the `rbac.authorization.kubernetes.io/autoupdate` annotation to `false`, which the page warns may leave a non-functional cluster.

## Discovery roles

| Default ClusterRole | Default ClusterRoleBinding | Description |
|---|---|---|
| `system:basic-user` | `system:authenticated` group | Read-only access to basic self-information |
| `system:discovery` | `system:authenticated` group | Read-only access to API discovery endpoints |
| `system:public-info-viewer` | `system:authenticated` and `system:unauthenticated` groups | Read-only access to non-sensitive cluster information |

## Command-line utilities

The page documents `kubectl create role`, `kubectl create clusterrole`, `kubectl create rolebinding`, `kubectl create clusterrolebinding` and `kubectl auth reconcile`. `kubectl create role` creates a Role within a single namespace; `kubectl create clusterrole` creates a ClusterRole, which additionally supports non-resource URLs (for example `/logs/*`) and aggregation rules; `kubectl create rolebinding` grants a Role or ClusterRole within a namespace; `kubectl create clusterrolebinding` grants a ClusterRole cluster-wide. `kubectl auth reconcile` creates or updates RBAC objects from manifest files and supports `--remove-extra-permissions` and `--remove-extra-subjects`.

> FIDELITY NOTE: the "Bootstrapping", "Discovery roles" and "Command-line utilities" paragraphs immediately above are **condensed**, not verbatim. Do not quote them as documentation sentences. Everything above them in this file is transcribed.
