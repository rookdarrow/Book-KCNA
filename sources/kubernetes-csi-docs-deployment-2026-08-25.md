---
source_url: "https://kubernetes-csi.github.io/docs/introduction.html"
fetched_at: "2026-08-25T02:36:00-0400"
authority: "Kubernetes CSI Developer Documentation (kubernetes-csi.github.io; Kubernetes SIG Storage)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "csi-driver", "absent-component-pattern"]
---
# Kubernetes CSI Developer Documentation — introduction and deployment shape

Pays the chapter-02:600 debt, which used the word *drivers*: this is what a CSI
driver is and what deploying one puts into a cluster. Linked to from the Kubernetes
glossary entry for CSI as the canonical deployment reference.

## Introduction (https://kubernetes-csi.github.io/docs/introduction.html)

"This site documents how to develop, deploy, and test a Container Storage Interface (CSI) driver on Kubernetes."

"The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Container Orchestration Systems (COs) like Kubernetes."

"Using CSI third-party storage providers can write and deploy plugins exposing new storage systems in Kubernetes without ever having to touch the core Kubernetes code."

## Deploying a CSI driver (https://kubernetes-csi.github.io/docs/deploying.html)

"A CSI driver is typically deployed in Kubernetes as two components: a controller component and a per-node component."

"The controller component can be deployed as a Deployment or StatefulSet on any node in the cluster."

"The node component should be deployed on every node in the cluster through a DaemonSet."

"Deploying a CSI driver onto Kubernetes is highlighted in detail in [Recommended Mechanism for Deploying CSI Drivers on Kubernetes]"

RETRIEVAL NOTE — these four are short exact quotations. A request for the full text
of both pages was declined by the retrieval tool, so this snapshot is a
quotation-level capture rather than a full-page transcription. It is sufficient for
KCNA depth (recall: name the interface, say what it is for) and sufficient for the
outline's 🔭 Closer Look, which needs only "controller component + per-node
component + sidecars, and you install it yourself."

NOTE FOR §5 — combined with the glossary sentence "you must first deploy it to your
cluster" and the volumes-page sentence "The core of Kubernetes does not install that
software for you", these three independent statements make the absent-component
payoff airtight: nothing in Kubernetes ships the driver, so a StorageClass naming a
driver nobody installed is the ordinary, documented failure — not an exotic one.
