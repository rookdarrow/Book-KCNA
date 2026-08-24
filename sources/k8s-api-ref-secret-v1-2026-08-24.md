---
source_url: "https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/secret-v1/"
fetched_at: "2026-08-24T04:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs, Kubernetes API reference) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D1 Core Concepts", "D1.1", "D2 Security"]
concepts_covered: ["secret", "secret-types", "secret-storage-default", "opaque-secret"]
---
# Secret v1 — Kubernetes API reference (kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/secret-v1/)

## Resource description

"Secret holds secret data of a certain type. The total bytes of the values in the Data field must be less than MaxSecretSize bytes."

## Fields

### `data` (map[string][]byte)

"Data contains the secret data. Each key must consist of alphanumeric characters, '-', '_' or '.'. The serialized form of the secret data is a base64 encoded string, representing the arbitrary (possibly non-string) data value here. Described in https://tools.ietf.org/html/rfc4648#section-4"

### `stringData` (map[string]string)

"stringData allows specifying non-binary secret data in string form. It is provided as a write-only input field for convenience. All keys and values are merged into the data field on write, overwriting any existing values. The stringData field is never output when reading from the API."

### `immutable` (boolean)

"Immutable, if set to true, ensures that data stored in the Secret cannot be updated (only object metadata can be modified). If not set to true, the field can be modified at any time. Defaulted to nil."

### `type` (string)

"Used to facilitate programmatic handling of secret data. More info: https://kubernetes.io/docs/concepts/configuration/secret/#secret-types"

---

**Snapshot note (not source text):** the resource description states the limit as the symbolic constant `MaxSecretSize`; this reference page does not give a numeric byte value. See research manifest gap G-C.
