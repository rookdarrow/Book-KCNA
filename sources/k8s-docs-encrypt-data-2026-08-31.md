---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/"
fetched_at: "2026-08-31T10:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["encryption-at-rest", "encryptionconfiguration", "secret-storage-default-unencrypted", "secret-hardening"]
---
# Encrypting Confidential Data at Rest (kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

## Opening

"All of the APIs in Kubernetes that let you write persistent API resource data support at-rest encryption. For example, you can enable at-rest encryption for Secrets. This at-rest encryption is additional to any system-level encryption for the etcd cluster or for the filesystem(s) on hosts where you are running the kube-apiserver."

"This page shows how to enable and configure encryption of API data at rest."

"This task covers encryption for resource data stored using the Kubernetes API. For example, you can encrypt Secret objects, including the key-value data they contain."

**Note (scope):** "This task covers encryption for resource data stored using the Kubernetes API. If you want to encrypt data in filesystems that are mounted into containers, you instead need to either: use a storage integration that provides encrypted volumes [or] encrypt the data within your own application."

**"By default, the API server stores plain-text representations of resources into etcd, with no at-rest encryption."**

## Determining whether encryption at rest is already enabled

"The `kube-apiserver` process accepts an argument `--encryption-provider-config` that specifies a path to a configuration file. The contents of that file, if you specify one, control how Kubernetes API data is encrypted in etcd. If you are running the kube-apiserver without the `--encryption-provider-config` command line argument, you do not have encryption at rest enabled. If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies the `identity` provider as the first encryption provider in the list, then you do not have at-rest encryption enabled (the default `identity` provider does not provide any confidentiality protection)."

"If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies a provider other than `identity` as the first encryption provider in the list, then you already have at-rest encryption enabled."

## The EncryptionConfiguration resource

The configuration object is an `EncryptionConfiguration` in the `apiserver.config.k8s.io/v1` API group. It names the API kinds to encrypt and an ordered list of providers:
