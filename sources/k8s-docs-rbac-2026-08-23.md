---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/rbac/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Security"]
concepts_covered: ["rbac", "role", "clusterrole", "rolebinding", "clusterrolebinding", "default-clusterroles"]
---
# Using RBAC Authorization (kubernetes.io/docs/reference/access-authn-authz/rbac/)

Role-based access control (RBAC) is a method of regulating access to computer or network resources based on the roles of individual users within your organization. RBAC authorization uses the rbac.authorization.k8s.io API group to drive authorization decisions, allowing you to dynamically configure policies through the Kubernetes API. To enable RBAC, start the API server with an authorization configuration that includes the RBAC authorizer, or with the --authorization-mode flag set to a comma-separated list that includes RBAC.

## API objects
The RBAC API declares four kinds of Kubernetes object: Role, ClusterRole, RoleBinding and ClusterRoleBinding.

**Role and ClusterRole.** An RBAC Role or ClusterRole contains rules that represent a set of permissions. Permissions are purely additive (there are no "deny" rules). A Role always sets permissions within a particular namespace; when you create a Role, you have to specify the namespace it belongs in. ClusterRole, by contrast, is a non-namespaced resource. ClusterRoles have several uses. You can use a ClusterRole to: define permissions on namespaced resources and be granted access within individual namespace(s); define permissions on namespaced resources and be granted access across all namespaces; define permissions on cluster-scoped resources. If you want to define a role within a namespace, use a Role; if you want to define a role cluster-wide, use a ClusterRole.

**RoleBinding and ClusterRoleBinding.** A role binding grants the permissions defined in a role to a user or set of users. It holds a list of subjects (users, groups, or service accounts), and a reference to the role being granted. A RoleBinding grants permissions within a specific namespace whereas a ClusterRoleBinding grants that access cluster-wide. A RoleBinding may reference any Role in the same namespace. Alternatively, a RoleBinding can reference a ClusterRole and bind that ClusterRole to the namespace of the RoleBinding. If you want to bind a ClusterRole to all the namespaces in your cluster, you use a ClusterRoleBinding. After you create a binding, you cannot change the Role or ClusterRole that it refers to.

## Default roles and role bindings (user-facing)
- **cluster-admin** — Allows super-user access to perform any action on any resource. When used in a ClusterRoleBinding, it gives full control over every resource in the cluster and in all namespaces. When used in a RoleBinding, it gives full control over every resource in the role binding's namespace, including the namespace itself.
- **admin** — Allows admin access, intended to be granted within a namespace using a RoleBinding. If used in a RoleBinding, allows read/write access to most resources in a namespace, including the ability to create roles and role bindings within the namespace.
- **edit** — Allows read/write access to most objects in a namespace. This role does not allow viewing or modifying roles or role bindings.
- **view** — Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets.
