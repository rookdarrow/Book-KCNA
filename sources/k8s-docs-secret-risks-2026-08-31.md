---
source_url: "https://kubernetes.io/docs/concepts/configuration/secret/"
fetched_at: "2026-08-31T11:36:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["secret-storage-default-unencrypted", "secret-exposure-paths", "pod-creation-privilege-escalation", "privileged-container", "file-mount-over-env-var", "secret-hardening"]
---
# Secret — the risks and information-security sections (kubernetes.io/docs/concepts/configuration/secret/)

Companion to `k8s-docs-secret-2026-08-23.md` (which carries the object, the types, and base64) and `k8s-docs-secrets-good-practices-2026-08-24.md` (which carries the four hardening items). This snapshot carries the exposure statements §4 is built on.

## The headline caution

**"Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd."**

The recommendations that follow it: enable encryption at rest for Secrets; configure RBAC rules with least-privilege access to Secrets; restrict Secret access to specific containers; and consider using external Secret store providers.

## Information security for Secrets

Kubernetes applies protections to Secrets beyond those given to ConfigMaps:

- A Secret is only sent to a node if a Pod on that node requires it.
- The kubelet stores its copy in a temporary filesystem (tmpfs) rather than on durable storage.
- Once the Pods that depend on the Secret are deleted, the local copies are removed.

On authorization: granting `list` or `watch` on Secrets allows reading all Secret data in a namespace, not only the Secrets a caller explicitly names. Access should be restricted to the minimum necessary, and broad roles such as `cluster-admin` avoided unless administratively required.

**A container running with `privileged: true` can access all Secrets on that node.**

## Secret updates: mounted volume versus environment variable

When a Secret is mounted as a volume, updates propagate to the Pod automatically. "A container using a Secret as a subPath volume mount does not receive automated Secret updates."

## ⚠ WHAT THIS PAGE DOES *NOT* SAY — read before drafting §4's file-over-env-var argument

`chapter-11:444` promised the reader: *"File over environment variable is half an argument already, and you now hold that half."* The half the reader holds is tmpfs.

**The other half, as commonly stated in prep material — that environment variables leak into logs, `kubectl describe` output, crash reports or child processes — is NOT stated anywhere on kubernetes.io in this corpus.** It was searched for and not found.

What *is* sourced, and what §4 may therefore argue:
1. A mounted Secret's updates propagate; an environment variable is fixed at container start (this page).
2. "If you are defining multiple containers in a Pod, and only one of those containers needs access to a Secret, define the volume mount or environment variable configuration so that the other containers do not have access to that Secret" (`k8s-docs-secrets-good-practices-2026-08-24.md`).
3. "Applications still need to protect the value of confidential information after reading it from an environment variable or volume. For example, your application must avoid logging the secret data in the clear or transmitting it to an untrusted party" (same page) — note this warns about the *application's* handling, symmetrically for both mechanisms; it is **not** a claim that env vars specifically leak.

The §4 argument must be built from (1) and (2), or marked `[inferred]`. See § Gaps.
