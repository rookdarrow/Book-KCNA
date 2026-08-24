---
source_url: "https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1", "D2 Security"]
concepts_covered: ["secret", "secret-storage-default", "manifest"]
---
# Managing Secrets using Configuration File (kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/)

## Create the Secret

"The `data` field is used to store arbitrary data, encoded using base64. The `stringData` field is provided for convenience, and it allows you to provide the same data as unencoded strings."

"The serialized JSON and YAML values of Secret data are encoded as base64 strings. Newlines are not valid within these strings and must be omitted."

## Specify unencoded data when creating a Secret

"This field allows you to put a non-base64 encoded string directly into the Secret, and the string will be encoded for you when the Secret is created or updated."

"When you retrieve the Secret data, the command returns the encoded values, and not the plaintext values you provided in `stringData`."

---

**Snapshot note (not source text):** this page documents *that* Secret `data` is base64-encoded. It does **not** contain the claim that base64 is not encryption. For that claim, cite `k8s-docs-secrets-good-practices-2026-08-24.md`.
