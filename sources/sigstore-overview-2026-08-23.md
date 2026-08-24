---
source_url: "https://docs.sigstore.dev/about/overview/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Sigstore project (OpenSSF)"
objectives_covered: ["D2 Security", "D1 Containerization"]
concepts_covered: ["sigstore", "cosign", "fulcio", "rekor", "keyless-signing", "supply-chain-security", "sbom"]
---
# Sigstore — Overview (docs.sigstore.dev/about/overview/)

Sigstore is an open source project for improving software supply chain security. The Sigstore framework and tooling empowers software developers and consumers to securely sign and verify software artifacts such as release files, container images, binaries, software bills of materials (SBOMs), and more. Sigstore operates as a free, public-good service under the Open Source Security Foundation (OpenSSF).

Components: **Cosign** — the client tool for signing and verifying software artifacts, including container images; **Fulcio** — the code-signing certificate authority that issues short-lived certificates bound to a verified identity rather than long-lived keys; **Rekor** — an immutable, append-only transparency log that records signing events for public audit and verification; **Policy Controller** — enforces signature verification policies within Kubernetes as an admission controller.

Keyless signing: a Cosign client creates an ephemeral key pair and requests a certificate from Fulcio using an OpenID Connect identity token; Fulcio validates the token and issues a short-lived certificate linking the public key to the verified identity; the artifact is signed, the private key is discarded after a single signing, and the signature and certificate are recorded in Rekor. Verification checks the signature, certificate validity, identity, and Rekor inclusion — establishing that the artifact came from its expected source without tampering.
