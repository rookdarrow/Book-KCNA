---
source_url: "https://kubernetes.io/releases/version-skew-policy/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/releases)"
objectives_covered: ["D1 Administration"]
concepts_covered: ["semantic-versioning", "supported-versions", "patch-support", "version-skew", "upgrade-order"]
---
# Version Skew Policy (kubernetes.io/releases/version-skew-policy/)

## Supported versions
Kubernetes versions are expressed as x.y.z, where x is the major version, y is the minor version, and z is the patch version, following Semantic Versioning terminology. The Kubernetes project maintains release branches for the most recent three minor releases (1.36, 1.35, 1.34 as of this snapshot). Kubernetes 1.19 and newer receive approximately 1 year of patch support. Applicable fixes, including security fixes, may be backported to those three release branches, depending on severity and feasibility. Patch releases are cut from those branches at a regular cadence, plus additional urgent releases, when required.

## Supported version skew
- kube-apiserver — In highly-available (HA) clusters, the newest and oldest kube-apiserver instances must be within one minor version.
- kubelet — kubelet must not be newer than kube-apiserver. kubelet may be up to three minor versions older than kube-apiserver (kubelet < 1.25 may only be up to two minor versions older). Example: kube-apiserver at 1.36 supports kubelet at 1.36, 1.35, 1.34, and 1.33.
- kube-proxy — must not be newer than kube-apiserver; may be up to three minor versions older than kube-apiserver; may be up to three minor versions older or newer than the kubelet instance it runs alongside.
- kube-controller-manager, kube-scheduler, and cloud-controller-manager — must not be newer than the kube-apiserver instances they communicate with. They are expected to match the kube-apiserver minor version, but may be up to one minor version older (to allow live upgrades).
- kubectl — supported within one minor version (older or newer) of kube-apiserver. Example: kube-apiserver at 1.36 supports kubectl at 1.37, 1.36, and 1.35.
