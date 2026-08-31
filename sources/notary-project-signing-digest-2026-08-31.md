---
source_url: "https://notaryproject.dev/"
secondary_source_url: "https://notaryproject.dev/docs/quickstart-guides/quickstart-sign-image-artifact/"
fetched_at: "2026-08-31T11:10:00-0400"
authority: "Notary Project (CNCF incubating)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["notary", "image-signing", "signature-binds-to-digest", "attestation", "supply-chain-security", "private-registry-restriction"]
---
# Notary Project (notaryproject.dev) — and the digest-binding fact

## What it is

"A set of specifications and tools intended to provide a cross-industry standard for securing software supply chains."

"Signing and verifying artifacts. Safeguarding the software delivery security from development to deployment."

"Signing and validating software artifacts, ensure they have not been tampered with and provide security policies to determine which validated artifacts are allowed to be used in your systems"

"Able to custom trust policy and determine if a signed artifact is considered authentic"

Tooling: **Notation** is the project's CLI. "Notary Project is a CNCF incubating project"

## ★ A signature binds to a digest, not a tag

From the project's quickstart for signing a container image artifact:

**"Notation resolves the tag to the digest before signing if a tag is used to identify the container image."**

**"Always reference and use the image digest instead of a tag since digest is immutable."**

> This is the primary-source basis for Chapter 12 §7's Fixed Point and for the Ch 2 §3 retrieval (tags are mutable pointers; digests are identity). It is a *Notary Project* statement, not a Kubernetes one — attribute it to the Notary Project. The equivalent Cosign statement could not be located on docs.sigstore.dev; see § Gaps.
