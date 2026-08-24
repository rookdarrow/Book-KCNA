---
source_url: "https://kubernetes.io/docs/concepts/configuration/secret/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Security", "D1 Core Concepts"]
concepts_covered: ["secret", "encryption-at-rest", "secret-types", "opaque", "tls-secret", "dockerconfigjson", "service-account-token", "least-privilege"]
---
# Secrets (kubernetes.io/docs/concepts/configuration/secret/)

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code. Secrets are similar to ConfigMaps but are specifically intended to hold confidential data.

Caution: Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd. Additionally, anyone who is authorized to create a Pod in a namespace can use that access to read any Secret in that namespace; this includes indirect access such as the ability to create a Deployment. In order to safely use Secrets, take at least the following steps: enable Encryption at Rest for Secrets; enable or configure RBAC rules with least-privilege access to Secrets; restrict Secret access to specific containers; consider using external Secret store providers.

## Uses for Secrets
Set environment variables for a container; provide credentials such as SSH keys or passwords to Pods; allow the kubelet to pull container images from private registries.

## Types of Secret
| Built-in type | Usage |
|---|---|
| Opaque | arbitrary user-defined data (the default type) |
| kubernetes.io/service-account-token | ServiceAccount token (legacy long-lived credential; since v1.22 the recommended approach is short-lived, automatically rotating tokens via the TokenRequest API) |
| kubernetes.io/dockercfg | serialized ~/.dockercfg file |
| kubernetes.io/dockerconfigjson | serialized ~/.docker/config.json file |
| kubernetes.io/basic-auth | credentials for basic authentication |
| kubernetes.io/ssh-auth | credentials for SSH authentication |
| kubernetes.io/tls | data for a TLS client or server |
| bootstrap.kubernetes.io/token | bootstrap token data |
