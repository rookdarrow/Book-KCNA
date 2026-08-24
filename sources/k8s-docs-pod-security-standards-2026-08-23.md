---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-standards/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Security"]
concepts_covered: ["pod-security-standards", "privileged", "baseline", "restricted", "pod-security-admission", "namespace-labels"]
---
# Pod Security Standards (kubernetes.io/docs/concepts/security/pod-security-standards/)

The Pod Security Standards define three different policies to broadly cover the security spectrum. These policies are cumulative and range from highly-permissive to highly-restrictive.

| Profile | Description |
|---|---|
| Privileged | Unrestricted policy, providing the widest possible level of permissions. This policy allows for known privilege escalations. |
| Baseline | Minimally restrictive policy which prevents known privilege escalations. Allows the default (minimally specified) Pod configuration. |
| Restricted | Heavily restricted policy, following current Pod hardening best practices. |

**Privileged.** The Privileged policy is purposely-open, and entirely unrestricted. This type of policy is typically aimed at system- and infrastructure-level workloads managed by privileged, trusted users. The Privileged policy is defined by an absence of restrictions; a Pod under it is able to bypass typical container isolation mechanisms (for example, access the node's host network).

**Baseline.** The Baseline policy is aimed at ease of adoption for common containerized workloads while preventing known privilege escalations. This policy is targeted at application operators and developers of non-critical applications.

**Restricted.** The Restricted policy is aimed at enforcing current Pod hardening best practices, at the expense of some compatibility. It is targeted at operators and developers of security-critical applications, as well as lower-trust users.

The standards are enforced by the built-in Pod Security Admission controller, which applies a policy per namespace via labels of the form pod-security.kubernetes.io/<MODE>: <LEVEL>, where MODE is enforce (violations are rejected), audit (violations are recorded in the audit log), or warn (violations trigger a user-facing warning), and LEVEL is privileged, baseline, or restricted.
