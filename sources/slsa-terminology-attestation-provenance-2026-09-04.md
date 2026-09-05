---
source_url: "https://slsa.dev/spec/v1.0/terminology"
fetched_at: "2026-09-04T09:15:00-0400"
authority: "SLSA (Supply-chain Levels for Software Artifacts) specification v1.0 — an OpenSSF (Linux Foundation) project; the specification's own terminology page and attestation model"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["attestation", "provenance", "supply-chain-security", "image-signing"]
---
# SLSA v1.0 — Terminology, and the attestation model

Two pages of the SLSA specification, quoted for the two definitions Ch 12 §7 relies on and that no other snapshot in this corpus states in one sentence. in-toto's landing page (`in-toto-overview-2026-08-31.md`) describes what its framework records but does not define either word; SLSA's attestation format is itself built on in-toto's attestation framework.

## Terminology (https://slsa.dev/spec/v1.0/terminology)

**Artifact** — "An immutable blob of data; primarily refers to software, but SLSA can be used for any artifact."

**Attestation** — "An authenticated statement (metadata) about a software artifact or collection of software artifacts."

**Build** — "Process that transforms a set of input artifacts into a set of output artifacts."

**Provenance** — "Attestation (metadata) describing how the outputs were produced, including identification of the platform and external parameters."

**Software supply chain** — "The sequence of steps resulting in the creation of an artifact."

## Attestation model (https://slsa.dev/spec/v1.0/attestation-model)

"A software attestation is an authenticated statement (metadata) about a software artifact or collection of software artifacts."

The page names the SLSA Provenance format as one standardized predicate type: an attestation that records exactly how an artifact was produced, including the build command that was run and all of its dependencies.
