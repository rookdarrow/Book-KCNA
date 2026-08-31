---
source_url: "https://fluxcd.io/flux/security/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Flux project (CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["delivery-agent-identity", "blast-radius", "flux-controller-set"]
---
# Flux — Security model (RBAC and impersonation)

## RBAC manifests installed
"Flux installs a set of RBAC manifests. These include: A `crd-controller` `ClusterRole`, which: Has full access to all the Custom Resource Definitions defined by Flux controllers"

"A `cluster-reconciler` `ClusterRoleBinding`: References `cluster-admin` `ClusterRole` Bound to service accounts for only `kustomize-controller` and `helm-controller`"

Those two controllers are bound to `cluster-admin` because they "are the only two controllers that manage resources in the cluster."

## Multi-tenancy and impersonation
"In a soft multi-tenancy setup, Flux does not reconcile a tenant's repo under the `cluster-admin` role. Instead, you specify a different service account in your manifest, and the Flux controllers will use the Kubernetes Impersonation API under `cluster-admin` to impersonate that service account."

## Related, from the security best-practices page
(https://fluxcd.io/flux/security/best-practices/)
A controller flag "Enforces all reconciliations to impersonate a given Service Account, effectively disabling the use of the privileged service account that would otherwise be used by the controller."

CAPTURE NOTE: neither the security page nor the security best-practices page
discusses push-based versus pull-based delivery, agent placement rationale, or
credential exposure outside the cluster. Verified 2026-08-31.
