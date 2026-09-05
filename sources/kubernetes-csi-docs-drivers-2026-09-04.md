---
source_url: "https://kubernetes-csi.github.io/docs/drivers.html"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes CSI developer documentation (the kubernetes-csi/docs repository, maintained under Kubernetes SIG Storage). The drivers table is filled in by driver maintainers via pull request and carries the project's own disclaimer that SIG-Storage has not validated its contents. Text taken from the page's Markdown source (master branch, book/src/drivers.md)."
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "csi-driver"]
---

# Drivers (kubernetes-csi.github.io/docs/drivers.html)

Closes the research gap recorded in Ch 11 §5, where a Snag naming three CSI drivers had been
genericized for want of a source. Verbatim except where marked. At retrieval the "Production
Drivers" table held 138 rows; the three rows below are reproduced exactly, restricted to the
table's first four columns (the remaining columns — Persistence (Beyond Pod Lifetime), Supported
Access Modes, Dynamic Provisioning, Other Features — are omitted). Row names are rendered links on
the page; the link targets are dropped here.

"The following are a set of CSI driver which can be used with Kubernetes:"

"NOTE: If you would like your driver to be added to this table, please open a pull request in this repo updating this file. Other Features is allowed to be filled in Raw Block, Snapshot, Expansion, Cloning and Topology. If driver did not implement any Other Features, please leave it blank."

"DISCLAIMER: Information in this table has not been validated by Kubernetes SIG-Storage. Users who want to use these CSI drivers need to contact driver maintainers for driver capabilities."

## Production Drivers (three rows of 138)

| Name | CSI Driver Name | Compatible with CSI Version(s) | Description |
|---|---|---|---|
| AWS Elastic Block Storage | `ebs.csi.aws.com` | v0.3, v1.0 | A Container Storage Interface (CSI) Driver for AWS Elastic Block Storage (EBS) |
| Ceph RBD | `rbd.csi.ceph.com` | v0.3, >=v1.0.0 | A Container Storage Interface (CSI)  Driver for Ceph RBD |
| vSphere | `csi.vsphere.vmware.com` | v1.4 | A Container Storage Interface (CSI) Driver for VMware vSphere |

USE NOTE — cite this file for the existence, ownership and registered names of vendor-written
CSI drivers, and for the size of the list. Do not cite it for any driver's capabilities: the
project's own disclaimer says the table is not validated.
