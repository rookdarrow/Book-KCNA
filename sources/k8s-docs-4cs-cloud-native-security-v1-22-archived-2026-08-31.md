---
source_url: "https://kubernetes.io/docs/concepts/security/overview/"
archived_source_url: "https://raw.githubusercontent.com/kubernetes/website/release-1.22/content/en/docs/concepts/security/overview.md"
fetched_at: "2026-08-31T11:03:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), as published in the Kubernetes v1.22 documentation — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["four-cs", "image-scanning", "image-signing", "encryption-at-rest", "private-registry-restriction", "runtime-class"]
---
# Overview of Cloud Native Security — the 4Cs (archived Kubernetes v1.22 documentation)

⚠ **VERSION STATUS — read before citing.** This is the Kubernetes project's own 4Cs page as it stood in the v1.22 documentation. The current page at the same conceptual location, `k8s-docs-cloud-native-security-2026-08-23.md`, records that it *replaced* the 4Cs framing with the CNCF whitepaper's lifecycle phases. This snapshot exists to make Open question #1 option **(a)** — teach both, phases as current and 4Cs as the framing the reader will meet elsewhere — sourceable from the primary authority rather than from third-party prep. If the author picks (b) or (c), this snapshot is unused, not wrong.

"This overview defines a model for thinking about Kubernetes security in the context of Cloud Native security."

## The 4C's of Cloud Native security

"The 4C's of Cloud Native security are Cloud, Clusters, Containers, and Code."

This layered approach augments the defense in depth computing approach to security, which is widely regarded as a best practice for securing software systems.

"Each layer of the Cloud Native security model builds upon the next outermost layer." The Code layer benefits from strong foundational (Cloud, Cluster, Container) security layers. "You cannot safeguard against poor security standards in the base layers by addressing security at the Code level."

## Cloud

"In many ways, the Cloud (or co-located servers, or the corporate datacenter) is the trusted computing base of a Kubernetes cluster. If the Cloud layer is vulnerable (or configured in a vulnerable way) then there is no guarantee that the components built on top of this base are secure."

Infrastructure security suggestions, as the page tabulates them:

| Area of Concern | Recommendation |
|---|---|
| Network access to API Server (Control plane) | All access to the Kubernetes control plane is not allowed publicly on the internet and is controlled by network access control lists restricted to the set of IP addresses needed to administer the cluster. |
| Network access to Nodes | Nodes should be configured to only accept connections (via network access control lists) from the control plane on the specified ports, and accept connections for services in Kubernetes of type NodePort and LoadBalancer. If possible, these nodes should not be exposed on the public internet entirely. |
| Kubernetes access to Cloud Provider API | Each cloud provider needs to grant a different set of permissions to the Kubernetes control plane and nodes. It is best to provide the cluster with cloud provider access that follows the principle of least privilege for the resources it needs to administer. |
| Access to etcd | Access to etcd (the datastore of Kubernetes) should be limited to the control plane only. Depending on your configuration, you should attempt to use etcd over TLS. |
| etcd Encryption | Wherever possible it's a good practice to encrypt all storage at rest, and since etcd holds the state of the entire cluster (including Secrets) its disk should especially be encrypted at rest. |

## Cluster

"There are two areas of concern for securing Kubernetes: securing the cluster components that are configurable and securing the applications which run in the cluster."

The page's workload-security list points at: RBAC Authorization (access to the Kubernetes API), Authentication, Application secrets management (including encryption at rest), Pod Security Standards, Quality of Service and cluster resource management, Network Policies, and TLS for Kubernetes Ingress.

## Container

"Container security is outside the scope of this guide." General recommendations, as tabulated:

| Area of Concern | Recommendation |
|---|---|
| Container Vulnerability Scanning and OS Dependency Security | As part of an image build step, you should scan your containers for known vulnerabilities. |
| Image Signing and Enforcement | Sign container images to maintain a system of trust for the content of your containers. |
| Disallow privileged users | When constructing containers, consult your documentation for how to create users inside of the containers that have the least level of operating system privilege necessary. |
| Container runtime isolation | Select container runtime classes that provide stronger isolation. |

## Code

"Application code is one of the primary attack surfaces over which you have the most control."

| Area of Concern | Recommendation |
|---|---|
| Access over TLS only | If your code needs to communicate by TCP, perform a TLS handshake with the client ahead of time. Encrypt everything in transit. Consider mutual TLS authentication (mTLS) for two-sided verification between certificate-holding services. |
| Limiting port ranges of communication | Wherever possible you should only expose the ports on your service that are absolutely essential for communication or metric gathering. |
| 3rd Party Dependency Security | It is a good practice to regularly scan your application's third party libraries for known security vulnerabilities. |
| Static Code Analysis | Most languages provide a way for code to be analyzed for potentially unsafe coding practices. |
| Dynamic probing attacks | Run automated tools against your service to test for well-known service attacks including SQL injection, CSRF, and XSS. |
