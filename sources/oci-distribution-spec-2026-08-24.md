---
source_url: "https://raw.githubusercontent.com/opencontainers/distribution-spec/main/spec.md"
fetched_at: "2026-08-24T01:05:00-0400"
authority: "Open Container Initiative (Linux Foundation) — OCI Distribution Specification"
objectives_covered: ["D1.4"]
concepts_covered: ["oci-distribution-spec", "registry", "image-digest"]
---
# OCI Distribution Specification

## What it defines

"The Open Container Initiative Distribution Specification (a.k.a. \"OCI Distribution
Spec\") defines an API protocol to facilitate and standardize the distribution of
content."

## Definitions

- Registry: "a service that handles the required APIs defined in this specification"
- Repository: "a scope for API calls on a registry for a collection of content
  (including manifests, blobs, and tags)."
- Blob: "the binary form of content that is stored by a registry, addressable by a
  digest"
- Manifest: "a JSON document uploaded via the manifests endpoint. A manifest may
  reference other manifests and blobs in a repository via descriptors."
- Digest: "a unique identifier created from a cryptographic hash of a Blob's content."

## Workflows

"Push: the act of uploading blobs and manifests to a registry"
"Pull: the act of downloading blobs and manifests from a registry"

## Note for §5

The Digest definition is Fixed Point #1's identity half stated by the standards body.
The Registry definition upgrades §5's back-bearing to §3 from "standardizes the API"
to a spec-level definition of what a registry IS. Version date (v1.0, May 2020) lives
in oci-overview-2026-08-23.md.
