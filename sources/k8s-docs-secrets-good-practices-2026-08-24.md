---
source_url: "https://kubernetes.io/docs/concepts/security/secrets-good-practices/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D1 Core Concepts", "D1.1"]
concepts_covered: ["secret", "secret-storage-default", "secret-hardening", "encryption-at-rest", "least-privilege"]
---
# Good practices for Kubernetes Secrets (kubernetes.io/docs/concepts/security/secrets-good-practices/)

## Opening

"In Kubernetes, a Secret is an object that stores sensitive information, such as passwords, OAuth tokens, and SSH keys. Secrets give you more control over how sensitive information is used and reduces the risk of accidental exposure. Secret values are encoded as base64 strings and are stored unencrypted by default, but can be configured to be encrypted at rest."

## Base64 encoding

"Base64 encoding is *not* an encryption method, it provides no additional confidentiality over plain text."

## Cluster administrators

### Configure encryption at rest

"By default, Secret objects are stored unencrypted in etcd. You should configure encryption of your Secret data in `etcd`. For instructions, refer to Encrypt Secret Data at Rest."

### Configure least-privilege access to Secrets

"When planning your access control mechanism, such as Kubernetes Role-based Access Control (RBAC), consider the following guidelines for access to `Secret` objects."

- "**Components**: Restrict `watch` or `list` access to only the most privileged, system-level components. Only grant `get` access for Secrets if the component's normal behavior requires it."
- "**Humans**: Restrict `get`, `watch`, or `list` access to Secrets. Only allow cluster administrators to access `etcd`. This includes read-only access."

### Improve etcd management policies

"Consider wiping or shredding the durable storage used by `etcd` once it is no longer in use. If there are multiple `etcd` instances, configure encrypted SSL/TLS communication between the instances to protect the Secret data in transit."

### Configure access to external Secrets

"You can use third-party Secrets store providers to keep your confidential data outside your cluster and then configure Pods to access that information. The Kubernetes Secrets Store CSI Driver is a DaemonSet that lets the kubelet retrieve Secrets from external stores, and mount the Secrets as a volume into specific Pods that you authorize to access the data."

## Developers

### Restrict Secret access to specific containers

"If you are defining multiple containers in a Pod, and only one of those containers needs access to a Secret, define the volume mount or environment variable configuration so that the other containers do not have access to that Secret."

### Protect Secret data after reading

"Applications still need to protect the value of confidential information after reading it from an environment variable or volume. For example, your application must avoid logging the secret data in the clear or transmitting it to an untrusted party."

### Avoid sharing Secret manifests

"If you configure a Secret through a manifest, with the secret data encoded as base64, sharing this file or checking it in to a source repository means the secret is available to everyone who can read the manifest."
