---
source_url: "https://kubernetes.io/docs/concepts/security/cloud-native-security/"
fetched_at: "2026-08-23T23:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), citing the CNCF TAG Security cloud native security whitepaper v2"
objectives_covered: ["D2 Security", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["cloud-native-security", "lifecycle-phases", "develop", "distribute", "deploy", "runtime", "supply-chain", "zero-trust", "pod-security-standards", "encryption-at-rest", "api-access-control"]
---
# Cloud Native Security and Kubernetes (kubernetes.io/docs/concepts/security/cloud-native-security/)

Kubernetes is based on a cloud native architecture and draws on advice from the CNCF about good practices for cloud native information security. The CNCF white paper on cloud native security defines security controls and practices that are appropriate to different lifecycle phases. (Note: this page replaced the older "4C's of Cloud Native Security" framing — Cloud, Cluster, Container, Code — with the CNCF whitepaper's lifecycle phases.)

## Develop lifecycle phase
Ensure the integrity of development environments. Design applications following good practices for information security, appropriate for your context. Consider end user security as part of solution design. To achieve this, you can: adopt an architecture, such as zero trust, that minimizes attack surfaces, even for internal threats; define a code review process that considers security concerns; build a threat model of your system or application that identifies trust boundaries, and use that threat model to identify risks and determine how to treat them; incorporate advanced security automation, such as fuzzing and security chaos engineering, where it's justified.

## Distribute lifecycle phase
Ensure the security of the supply chain for container images you execute. Ensure the security of the supply chain for the cluster and other components that execute your application. To achieve this, you can: scan container images and other artifacts for known vulnerabilities; ensure that software distribution uses encryption in transit, with a chain of trust for the software source; adopt and follow processes to update dependencies when updates are available, especially in response to security announcements; use validation mechanisms such as digital certificates for supply chain assurance; subscribe to feeds and other mechanisms to alert you to security risks; restrict access to artifacts — place container images in a private registry that only allows authorized clients to pull images.

## Deploy lifecycle phase
Ensure appropriate restrictions on what can be deployed, who can deploy it, and where it can be deployed. You can enforce measures from the distribute phase, such as verifying the cryptographic identity of container image artifacts. You can deploy different applications and cluster components into different namespaces. Containers and namespaces both provide isolation mechanisms that are relevant to information security. When you deploy Kubernetes, you also set the foundation for your applications' runtime environment: a Kubernetes cluster (or multiple clusters). That infrastructure must provide the security guarantees that higher layers expect.

## Runtime lifecycle phase
The Runtime phase comprises three critical areas: access, compute, and storage.

**Runtime protection: access.** The Kubernetes API is what makes your cluster work. Protecting this API is key to providing effective cluster security. Securing your cluster means implementing effective authentication and authorization for API access. Use ServiceAccounts to provide and manage security identities for workloads and cluster components. Kubernetes uses TLS to protect API traffic; make sure to deploy the cluster using TLS (including for traffic between nodes and the control plane) and protect the encryption keys.

**Runtime protection: compute.** Containers provide two things: isolation between applications and a mechanism to combine those isolated applications to run on the same host computer. Kubernetes relies on a container runtime to set up and run containers; the Kubernetes project does not recommend a specific container runtime. To protect your compute at runtime, you can: enforce Pod Security Standards for applications to help ensure they run with only the necessary privileges; run a specialized operating system on your nodes that is designed specifically for running containerized workloads (typically a read-only, immutable image); define ResourceQuotas to fairly allocate shared resources, and use LimitRanges to ensure that Pods specify their resource requirements; partition workloads across different nodes to improve isolation; use a container runtime that provides security restrictions; on Linux nodes, use a Linux security module such as AppArmor or seccomp.

**Runtime protection: storage.** Integrate your cluster with an external storage plugin that provides encryption at rest for volumes; enable encryption at rest for API objects; protect data durability using backups, and verify that you can restore them whenever needed; authenticate connections between cluster nodes and any network storage they rely upon; implement data encryption within your own application. For encryption keys, generating these within specialized hardware (a hardware security module) provides the best protection against disclosure risks.
