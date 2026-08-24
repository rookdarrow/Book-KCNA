---
source_url: "https://github.com/kubernetes/enhancements/blob/master/keps/README.md"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes/enhancements) + kubernetes.io feature-gates reference"
objectives_covered: ["D4 Community and Collaboration", "D1 Administration"]
concepts_covered: ["kep", "enhancement-proposal", "feature-gates", "alpha", "beta", "stable", "graduation"]
---
# Kubernetes Enhancement Proposals (KEPs) and feature stages

## KEPs (github.com/kubernetes/enhancements/blob/master/keps/README.md)
A Kubernetes Enhancement Proposal (KEP) is a way to propose, communicate and coordinate on new efforts for the Kubernetes project. The process is intended to clearly communicate new efforts to the Kubernetes contributor community, using a standard proposal format with useful metadata. A KEP is required for potentially controversial changes, most new features (except very small ones), major modifications to existing features, and changes that affect most of the project. The framework provides exposure through searchable websites, cross-referencing, and structured decision-making with a discoverable record — inspired by similar processes such as IETF RFCs and Python PEPs. KEPs track a feature through the stages alpha → beta → stable (GA), with graduation criteria stated in the KEP.

## Feature stages (kubernetes.io/docs/reference/command-line-tools-reference/feature-gates/)
- **Alpha** — disabled by default; might be buggy, enabling the feature may expose bugs; support for the feature may be dropped at any time without notice; the API may change in incompatible ways in a later software release without notice; recommended for use only in short-lived testing clusters, due to increased risk of bugs and lack of long-term support.
- **Beta** — usually enabled by default; well tested; enabling the feature is considered safe; support for the overall feature will not be dropped, though details may change; the schema and/or semantics of objects may change in incompatible ways in a subsequent beta or stable release.
- **GA / Stable** — the feature is always enabled; you cannot disable it; the corresponding feature gate is no longer needed and is deprecated and removed in a later release.
