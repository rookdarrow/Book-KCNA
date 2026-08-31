---
source_url: "https://spdx.dev/learn/overview/"
secondary_source_url: "https://cyclonedx.org/"
fetched_at: "2026-08-31T11:25:00-0400"
authority: "SPDX (Linux Foundation; ISO/IEC 5962:2021) and OWASP CycloneDX (Ecma International ECMA-424)"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["sbom", "supply-chain-security", "provenance"]
---
# SBOM — the two bill-of-materials standards

⚠ **PARTIAL SOURCE. Read the caveat at the bottom before drafting §7.**

## SPDX (Linux Foundation)

"The System Package Data Exchange (SPDX®) specification is an open standard designed to facilitate the communication of Bill of Materials (BOM) information across diverse domains, including software, artificial intelligence (AI), datasets, and system components."

What SPDX covers, in the project's own words: "Metadata for collections of software (Packages), individual Files, and portions of files (Snippets)"; "Comprehensive licensing information"; and "Provenance and Integrity: Tracking the origin and history of components, including checksums and cryptographic hashes."

"SPDX is a collaborative effort driven by the Linux Foundation and supported by a global community of developers, organizations, and industry experts."

Standards status: "SPDX 3.0 (a major revision to SPDX 2.2.1, aka free ISO/IEC 5962:2021 – SPDX® Specification V2.2.1)"

## CycloneDX (OWASP / Ecma International)

"OWASP CycloneDX is a full-stack Bill of Materials (BOM) standard that provides advanced supply chain capabilities for cyber risk reduction."

"CycloneDX: The International Standard for Bill of Materials (ECMA-424)"

BOM types the project lists: "SBOM, SaaSBOM, CBOM, VEX, HBOM, AI/ML-BOM"

"The OWASP Foundation and Ecma International Technical Committee for Software & System Transparency (TC54) drive the continued advancement of the specification."

## Sigstore, on SBOMs as a signable artifact class

From `sigstore-overview-2026-08-23.md`, already in the corpus: Sigstore "empowers software developers and consumers to securely sign and verify software artifacts such as release files, container images, binaries, software bills of materials (SBOMs), and more."

## ⚠ CAVEAT — what is NOT sourced here

**No source in this corpus defines what an SBOM *is* in a single sentence.** Neither SPDX's overview nor CycloneDX's landing page states a definition of the form "an SBOM is a formal, machine-readable inventory of the components and dependencies that make up a piece of software." The canonical definitions live at CISA and NTIA, both of which refused automated retrieval on 2026-08-31 (HTTP 403), and the CNCF Cloud Native Glossary has no SBOM entry (confirmed against its index).

What §7 **may** say from these sources: that a bill of materials is a standardised record of a software artifact's components, licensing, and provenance/integrity information; that the two dominant standards are SPDX (Linux Foundation, ISO/IEC 5962) and CycloneDX (OWASP/Ecma, ECMA-424); and that an SBOM is itself an artifact that can be signed. What §7 **may not** do is quote a definition of SBOM as though a source supplied one. See § Gaps.
