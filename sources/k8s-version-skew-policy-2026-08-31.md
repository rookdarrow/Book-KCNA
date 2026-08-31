---
source_url: "https://kubernetes.io/releases/version-skew-policy/"
fetched_at: "2026-08-31T13:40:00-0400"
authority: "Kubernetes project (kubernetes.io/releases), CC BY 4.0"
objectives_covered: ["D2.3"]
concepts_covered: ["version-skew-symptoms", "release-known-issues"]
supersedes_note: "Fuller than k8s-version-skew-policy-2026-08-23.md (2.1KB), which Ch 8 sec.6 cites. Ch 8's citation stands; cite THIS file for Ch 13 sec.6. Version numbers on the page have advanced to the 1.35-1.37 series since the 08-23 fetch -- see manifest Notes for the author, item 5."
lts_finding: "The page contains NO statement using the term 'long-term support' or 'LTS'. It documents a three-minor-release support window and ~1 year of patch support. See manifest Notes item 6 -- this bears on outline Open Question 3."
---
# Version Skew Policy

> All passages below are **[VERBATIM]**.

> "This document describes the maximum version skew supported between various Kubernetes components. Specific cluster deployment tools may place additional restrictions on version skew."

## Supported versions

> "Kubernetes versions are expressed as **x.y.z**, where **x** is the major version, **y** is the minor version, and **z** is the patch version, following Semantic Versioning terminology."

> "The Kubernetes project maintains release branches for the most recent three minor releases (1.37, 1.36, 1.35). Kubernetes 1.19 and newer receive approximately 1 year of patch support. Kubernetes 1.18 and older received approximately 9 months of patch support."

> "Applicable fixes, including security fixes, may be backported to those three release branches, depending on severity and feasibility. Patch releases are cut from those branches at a regular cadence, plus additional urgent releases, when required."

## Supported version skew

### kube-apiserver

> "In highly-available (HA) clusters, the newest and oldest `kube-apiserver` instances must be within one minor version."

> Example: "newest `kube-apiserver` is at **1.37**; other `kube-apiserver` instances are supported at **1.37** and **1.36**"

### kubelet

> "`kubelet` must not be newer than `kube-apiserver`."
> "`kubelet` may be up to three minor versions older than `kube-apiserver` (`kubelet` < 1.25 may only be up to two minor versions older than `kube-apiserver`)."

> Example: "`kube-apiserver` is at **1.37**; `kubelet` is supported at **1.37**, **1.36**, **1.35**, and **1.34**"

> Note: "If version skew exists between `kube-apiserver` instances in an HA cluster, this narrows the allowed `kubelet` versions."

> Example: "`kube-apiserver` instances are at **1.37** and **1.36**; `kubelet` is supported at **1.36**, **1.35**, and **1.34** (**1.37** is not supported because that would be newer than the `kube-apiserver` instance at version **1.36**)"

### kube-proxy

> "`kube-proxy` must not be newer than `kube-apiserver`."
> "`kube-proxy` may be up to three minor versions older than `kube-apiserver`."
> "`kube-proxy` may be up to three minor versions older or newer than the `kubelet` instance it runs alongside."

### kube-controller-manager, kube-scheduler, and cloud-controller-manager

> "`kube-controller-manager`, `kube-scheduler`, and `cloud-controller-manager` must not be newer than the `kube-apiserver` instances they communicate with. They are expected to match the `kube-apiserver` minor version, but may be up to one minor version older (to allow live upgrades)."

### kubectl

> "`kubectl` is supported within one minor version (older or newer) of `kube-apiserver`."

> Example: "`kube-apiserver` is at **1.37**; `kubectl` is supported at **1.38**, **1.37**, and **1.36**"

## Supported component upgrade order

> "The supported version skew between components has implications on the order in which components must be upgraded."

> Note: "Project policies for API deprecation and API change guidelines require `kube-apiserver` to not skip minor versions when upgrading, even in single-instance clusters."

> Note (kubelet): "Before performing a minor version `kubelet` upgrade, drain pods from that node. In-place minor version `kubelet` upgrades are not supported."

> Warning: "Running a cluster with `kubelet` instances that are persistently three minor versions behind `kube-apiserver` means they must be upgraded before the control plane can be upgraded."

> Warning: "Running a cluster with `kube-proxy` instances that are persistently three minor versions behind `kube-apiserver` means they must be upgraded before the control plane can be upgraded."
