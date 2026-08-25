---
source_url: "https://github.com/container-storage-interface/spec/blob/master/spec.md"
fetched_at: "2026-08-25T02:39:00-0400"
authority: "Container Storage Interface project (CNCF; container-storage-interface/spec)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "fourth-pluggable-interface", "csi-driver"]
---
# Container Storage Interface specification — Objective

The interface's own statement of purpose, from the specification document rather than
from Kubernetes documentation about it. This is the right citation for §5's Fixed
Point, because the Fixed Point is about CSI being a *published contract between two
parties* rather than a Kubernetes feature — and the spec is the contract.

## Objective

"define an industry standard 'Container Storage Interface' (CSI) that will enable storage vendors (SP) to develop a plugin once and have it work across a number of container orchestration (CO) systems."

## Goals in MVP (as summarised by the specification's own bullet list)

The specification's stated goals include: enabling SP authors to write one CSI
compliant Plugin that "just works" across all COs that implement CSI; defining APIs
(RPCs) for dynamic provisioning and deprovisioning of volumes, attaching and
detaching volumes from nodes, mounting and unmounting volumes, consumption of block
and mountable volumes, support for local storage providers, and creation and deletion
of snapshots; and defining plugin protocol recommendations.

## Non-Goals in MVP

The specification explicitly does not define mechanisms for Plugin Supervisor
lifecycle management, deployment/installation/upgrade/uninstall/monitoring, a
first-class message structure for storage grades, protocol-level authentication and
authorization, plugin packaging, or POSIX compliance guarantees.

"SHALL NOT obstruct a Plugin Supervisor or CO from interacting with Plugin-managed volumes in a POSIX-compliant manner."

RETRIEVAL NOTE — the Objective sentence and the closing POSIX sentence are verbatim
quotations. The "Goals in MVP" and "Non-Goals in MVP" paragraphs are the retrieval's
condensation of the spec's bullet lists and are recorded as SUMMARY, not verbatim.
Do not present them inside quotation marks in the drafted chapter. The Objective
sentence alone carries everything §5 actually needs.

NOTE FOR §5 — the phrase "across a number of container orchestration (CO) systems"
is worth noticing: CSI is not a Kubernetes interface that vendors happen to use, it
is a cross-orchestrator standard that Kubernetes happens to implement. That is a
sharper version of the §5 Fixed Point than the Kubernetes docs can supply, and it is
the same claim shape as OCI in Ch 2 (see the cached oci-overview snapshot).
