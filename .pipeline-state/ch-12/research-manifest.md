# Research Manifest — KCNA Chapter 12

**Stage 2 · Source Snapshot Research · Locks, Keys, and Watchstanders**
Book dir: `../Book-KCNA` · Exam: KCNA (CNCF / Linux Foundation), curriculum effective 2025-11-24
Research run: 2026-08-31 · Corpus before this run: 168 snapshots · Delivered here: 16 new

---

## Executive summary for the author

| Outline gap | Status after this run |
|---|---|
| **G5 — `securityContext`, PSS/PSA** (§5 undraftable, §6 partial) | **CLOSED.** A1, A2, A3, A4. §5 is now the *best*-sourced section in the chapter, not the worst. |
| **Encryption at rest** (§4 could not state the mechanism) | **CLOSED.** A5. |
| **RBAC good practices / privilege-escalation framing** (§3 + §4) | **CLOSED, and better than hoped.** A6 carries the Pod-creation escalation path *verbatim from kubernetes.io*, which converts B1 trap #61 from `[inferred]` reasoning into a `[source]` quotation. |
| **G6 — the 4Cs** (§1 blocked on an editorial call) | **UNBLOCKED.** A9 is the Kubernetes project's own archived 4Cs page (v1.22 docs). Open question #1 option **(a)** is now fully sourceable. The decision is still the author's; the research obstacle is gone. |
| **G22 — supply chain** (§7 partial) | **MOSTLY CLOSED.** A10–A14. The §7 **Fixed Point** — *a signature binds to a digest, not a tag* — is now sourced verbatim from the Notary Project. **CVE remains a gap.** |
| **§9's design rationale** (Open question #5) | **CONFIRMED UNSOURCEABLE.** Nothing found. §9's note stands unchanged — the argument must be marked as the author's reading. |

Three new gaps opened that the outline did not anticipate. They are in § Gaps below; the **file-over-env-var** one touches a pinned cross-bearing (`chapter-11:444`) and needs the author's eye.

---

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-security-context-2026-08-31.md` | Kubernetes project | D2.2 | securitycontext · pod-scope-vs-container-scope · run-as-user · linux-capabilities · allow-privilege-escalation · read-only-root-filesystem · seccomp · apparmor |
| `k8s-docs-linux-kernel-security-constraints-2026-08-31.md` | Kubernetes project | D2.2 | seccomp · apparmor · privileged-container · run-as-non-root · linux-capabilities · workload-to-host-boundary |
| `k8s-docs-pod-security-admission-2026-08-31.md` | Kubernetes project | D2.2 | pod-security-admission · psa-enforce · psa-audit · psa-warn · namespace-label-control-surface · podsecuritypolicy-removed |
| `k8s-docs-pod-security-standards-profiles-2026-08-31.md` | Kubernetes project | D2.2 | pss-privileged · pss-baseline · pss-restricted · run-as-non-root · allow-privilege-escalation · linux-capabilities |
| `k8s-docs-encrypt-data-2026-08-31.md` | Kubernetes project | D2.2 | encryption-at-rest · encryptionconfiguration · secret-storage-default-unencrypted |
| `k8s-docs-rbac-good-practices-2026-08-31.md` | Kubernetes project | D2.2 | least-privilege · pod-creation-privilege-escalation · secret-exposure-paths · workload-to-host-boundary · namespace-label-control-surface |
| `k8s-docs-rbac-depth-2026-08-31.md` | Kubernetes project | D2.2 | aggregated-clusterrole · subjects-are-named-not-selected · rule-verb-resource · default-role-admin/edit/view |
| `k8s-docs-authorization-2026-08-31.md` | Kubernetes project | D2.2 | authorization-mode · rbac · kubectl-auth-can-i |
| `k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31.md` | Kubernetes project (archived v1.22 docs) | D2.2 | four-cs · image-scanning · image-signing · encryption-at-rest |
| `notary-project-signing-digest-2026-08-31.md` | Notary Project (CNCF) | D2.2 | signature-binds-to-digest · notary · image-signing · attestation |
| `in-toto-overview-2026-08-31.md` | in-toto (CNCF graduated) | D2.2 | in-toto · provenance · supply-chain-security |
| `tuf-overview-2026-08-31.md` | TUF (CNCF graduated) | D2.2 | tuf · supply-chain-security |
| `harbor-overview-2026-08-31.md` | Harbor (CNCF graduated) | D2.2 | harbor · image-scanning · private-registry-restriction · image-signing |
| `sbom-standards-spdx-cyclonedx-2026-08-31.md` | Linux Foundation (SPDX) / OWASP + Ecma (CycloneDX) | D2.2 | sbom · supply-chain-security |
| `cncf-glossary-policy-as-code-2026-08-31.md` | CNCF Cloud Native Glossary | D2.2 / D4 | policy-engine · validate-mutate-generate |
| `k8s-docs-secret-risks-2026-08-31.md` | Kubernetes project | D2.2 | secret-exposure-paths · secret-storage-default-unencrypted · privileged-container · file-mount-over-env-var |

---

### A1 · `k8s-docs-security-context-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/configure-pod-container/security-context/"
fetched_at: "2026-08-31T10:05:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["securitycontext", "pod-scope-vs-container-scope", "run-as-user", "run-as-non-root", "linux-capabilities", "allow-privilege-escalation", "read-only-root-filesystem", "seccomp", "apparmor", "workload-to-host-boundary"]
---
# Configure a Security Context for a Pod or Container (kubernetes.io/docs/tasks/configure-pod-container/security-context/)

Transcribed from the page's markdown source. YAML manifests and shell transcripts omitted; prose is the source's own.

## What is a security context

"A security context defines privilege and access control settings for a Pod or Container. Security context settings include, but are not limited to:

* Discretionary Access Control: Permission to access an object, like a file, is based on user ID (UID) and group ID (GID).

* Security Enhanced Linux (SELinux): Objects are assigned security labels.

* Running as privileged or unprivileged.

* Linux Capabilities: Give a process some privileges, but not all the privileges of the root user.

* AppArmor: Use program profiles to restrict the capabilities of individual programs.

* Seccomp: Filter a process's system calls.

* `allowPrivilegeEscalation`: Controls whether a process can gain more privileges than its parent process. This bool directly controls whether the `no_new_privs` flag gets set on the container process. `allowPrivilegeEscalation` is always true when the container:
  * is run as privileged, or
  * has `CAP_SYS_ADMIN`

* `readOnlyRootFilesystem`: Mounts the container's root filesystem as read-only."

## Set the security context for a Pod

"To specify security settings for a Pod, include the `securityContext` field in the Pod specification. The `securityContext` field is a PodSecurityContext object. The security settings that you specify for a Pod apply to all Containers in the Pod."

"The `runAsUser` field specifies that for any Containers in the Pod, all processes run with user ID 1000. The `runAsGroup` field specifies the primary group ID of 3000 for all processes within any containers of the Pod. If this field is omitted, the primary group ID of the containers will be root(0). Any files created will also be owned by user 1000 and group 3000 when `runAsGroup` is specified. Since `fsGroup` field is specified, all processes of the container are also part of the supplementary group ID 2000. The owner for volume `/data/demo` and any files created in that volume will be Group ID 2000. Additionally, when the `supplementalGroups` field is specified, all processes of the container are also part of the specified groups. If this field is omitted, it means empty."

## Set the security context for a Container

"To specify security settings for a Container, include the `securityContext` field in the Container manifest. The `securityContext` field is a SecurityContext object. Security settings that you specify for a Container apply only to the individual Container, and they override settings made at the Pod level when there is overlap. Container settings do not affect the Pod's Volumes."

## Set capabilities for a Container

"With Linux capabilities, you can grant certain privileges to a process without granting all the privileges of the root user. To add or drop Linux capabilities for a Container, include the `capabilities` field in the `securityContext` section of the Container manifest."

"Without specifying a `capabilities` field, containers receive default capabilities. The default capabilities bitmap for a container process can be viewed by checking the status of process 1."

"When additional capabilities are set, such as `CAP_NET_ADMIN` and `CAP_SYS_TIME`, the capabilities bitmap changes to reflect these additions. Bit 12 represents `CAP_NET_ADMIN`, and bit 25 represents `CAP_SYS_TIME`."

"Linux capability constants have the form `CAP_XXX`. But when you list capabilities in your container manifest, you must omit the `CAP_` portion of the constant. For example, to add `CAP_SYS_TIME`, include `SYS_TIME` in your list of capabilities."

## Set the Seccomp Profile for a Container

"To set the Seccomp profile for a Container, include the `seccompProfile` field in the `securityContext` section of your Pod or Container manifest. The `seccompProfile` field is a SeccompProfile object consisting of `type` and `localhostProfile`. Valid options for `type` include `RuntimeDefault`, `Unconfined`, and `Localhost`. `localhostProfile` must only be set if `type: Localhost`. It indicates the path of the pre-configured profile on the node, relative to the kubelet's configured Seccomp profile location (configured with the `--root-dir` flag)."

## Set the AppArmor Profile for a Container

"To set the AppArmor profile for a Container, include the `appArmorProfile` field in the `securityContext` section of your Container. The `appArmorProfile` field is an AppArmorProfile object consisting of `type` and `localhostProfile`. Valid options for `type` include `RuntimeDefault`(default), `Unconfined`, and `Localhost`. `localhostProfile` must only be set if `type` is `Localhost`. It indicates the name of the pre-configured profile on the node. The profile needs to be loaded onto all nodes suitable for the Pod, since you don't know where the pod will be scheduled."

"If `containers[*].securityContext.appArmorProfile.type` is explicitly set to `RuntimeDefault`, then the Pod will not be admitted if AppArmor is not enabled on the Node. However if `containers[*].securityContext.appArmorProfile.type` is not specified, then the default (which is also `RuntimeDefault`) will only be applied if the node has AppArmor enabled. If the node has AppArmor disabled the Pod will be admitted but the Container will not be restricted by the `RuntimeDefault` profile."

## Assign SELinux labels to a Container

"To assign SELinux labels to a Container, include the `seLinuxOptions` field in the `securityContext` section of your Pod or Container manifest. The `seLinuxOptions` field is an SELinuxOptions object."

"To assign SELinux labels, the SELinux security module must be loaded on the host operating system. On Windows and Linux worker nodes without SELinux support, this field and any SELinux feature gates described below have no effect."
```

---

### A2 · `k8s-docs-linux-kernel-security-constraints-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/security/linux-kernel-security-constraints/"
fetched_at: "2026-08-31T10:12:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["seccomp", "apparmor", "privileged-container", "run-as-non-root", "linux-capabilities", "allow-privilege-escalation", "workload-to-host-boundary", "securitycontext"]
---
# Linux kernel security constraints for Pods and containers (kubernetes.io/docs/concepts/security/linux-kernel-security-constraints/)

Transcribed from the page's markdown source. Code blocks omitted; prose is the source's own.

## Run workloads without root privileges

"When you deploy a workload in Kubernetes, use the Pod specification to restrict that workload from running as the root user on the node. You can use the Pod `securityContext` to define the specific Linux user and group for the processes in the Pod, and explicitly restrict containers from running as root users. Setting these values in the Pod manifest takes precedence over similar values in the container image, which is especially useful if you're running images that you don't own."

"Ensure that the user or group that you assign to the workload has the permissions required for the application to function correctly. Changing the user or group to one that doesn't have the correct permissions could lead to file access issues or failed operations."

"Configuring the kernel security features on this page provides fine-grained control over the actions that processes in your cluster can take, but managing these configurations can be challenging at scale. Running containers as non-root, or in user namespaces if you need root privileges, helps to reduce the chance that you'll need to enforce your configured kernel security capabilities."

## Security features in the Linux kernel

"Kubernetes lets you configure and use Linux kernel features to improve isolation and harden your containerized workloads. Common features include the following:

* **Secure computing mode (seccomp)**: Filter which system calls a process can make
* **AppArmor**: Restrict the access privileges of individual programs
* **Security Enhanced Linux (SELinux)**: Assign security labels to objects for more manageable security policy enforcement"

"To configure settings for one of these features, the operating system that you choose for your nodes must enable the feature in the kernel. For example, Ubuntu 7.10 and later enable AppArmor by default. To learn whether your OS enables a specific feature, consult the OS documentation."

"You use the `securityContext` field in your Pod specification to define the constraints that apply to those processes. The `securityContext` field also supports other security settings, such as specific Linux capabilities or file access permissions using UIDs and GIDs."

### seccomp

"Some of your workloads might need privileges to perform specific actions as the root user on your node's host machine. Linux uses capabilities to divide the available privileges into categories, so that processes can get the privileges required to perform specific actions without being granted all privileges. Each capability has a set of system calls (syscalls) that a process can make. seccomp lets you restrict these individual syscalls. It can be used to sandbox the privileges of a process, restricting the calls it is able to make from userspace into the kernel."

"In Kubernetes, you use a *container runtime* on each node to run your containers. Example runtimes include CRI-O, Docker, or containerd. Each runtime allows only a subset of Linux capabilities by default. You can further limit the allowed syscalls individually by using a seccomp profile. Container runtimes usually include a default seccomp profile. Kubernetes lets you automatically apply seccomp profiles loaded onto a node to your Pods and containers."

"Kubernetes also has the `allowPrivilegeEscalation` setting for Pods and containers. When set to `false`, this prevents processes from gaining new capabilities and restricts unprivileged users from changing the applied seccomp profile to a more permissive profile."

#### Considerations for seccomp

"seccomp is a low-level security configuration that you should only configure yourself if you require fine-grained control over Linux syscalls. Using seccomp, especially at scale, has the following risks:

* Configurations might break during application updates
* Attackers can still use allowed syscalls to exploit vulnerabilities
* Profile management for individual applications becomes challenging at scale"

"Recommendation: Use the default seccomp profile that's bundled with your container runtime. If you need a more isolated environment, consider using a sandbox, such as gVisor. Sandboxes solve the preceding risks with custom seccomp profiles, but require more compute resources on your nodes and might have compatibility issues with GPUs and other specialized hardware."

### AppArmor and SELinux: policy-based mandatory access control

"You can use Linux policy-based mandatory access control (MAC) mechanisms, such as AppArmor and SELinux, to harden your Kubernetes workloads."

#### AppArmor

"AppArmor is a Linux kernel security module that supplements the standard Linux user and group based permissions to confine programs to a limited set of resources. AppArmor can be configured for any application to reduce its potential attack surface and provide greater in-depth defense. It is configured through profiles tuned to allow the access needed by a specific program or container, such as Linux capabilities, network access, and file permissions. Each profile can be run in either enforcing mode, which blocks access to disallowed resources, or complain mode, which only reports violations."

"AppArmor can help you to run a more secure deployment by restricting what containers are allowed to do, and/or provide better auditing through system logs. The container runtime that you use might ship with a default AppArmor profile, or you can use a custom profile."

#### SELinux

"SELinux is a Linux kernel security module that lets you restrict the access that a specific *subject*, such as a process, has to the files on your system. You define security policies that apply to subjects that have specific SELinux labels. When a process that has an SELinux label attempts to access a file, the SELinux server checks whether that process' security policy allows the access and makes an authorization decision."

"In Kubernetes, you can set an SELinux label in the `securityContext` field of your manifest. The specified labels are assigned to those processes. If you have configured security policies that affect those labels, the host OS kernel enforces these policies."

#### Differences between AppArmor and SELinux

"The operating system on your Linux nodes usually includes one of either AppArmor or SELinux. Both mechanisms provide similar types of protection, but have differences such as the following:

* **Configuration**: AppArmor uses profiles to define access to resources. SELinux uses policies that apply to specific labels.
* **Policy application**: In AppArmor, you define resources using file paths. SELinux uses the index node (inode) of a resource to identify the resource."

### Summary of features

"The following table describes the use cases and scope of each security control. You can use all of these controls together to build a more hardened system."

| Security feature | Description | How to use | Example |
|---|---|---|---|
| seccomp | Restrict individual kernel calls in the userspace. Reduces the likelihood that a vulnerability that uses a restricted syscall would compromise the system. | Specify a loaded seccomp profile in the Pod or container specification to apply its constraints to the processes in the Pod. | Reject the `unshare` syscall, which was used in CVE-2022-0185. |
| AppArmor | Restrict program access to specific resources. Reduces the attack surface of the program. Improves audit logging. | Specify a loaded AppArmor profile in the container specification. | Restrict a read-only program from writing to any file path in the system. |
| SELinux | Restrict access to resources such as files, applications, ports, and processes using labels and security policies. | Specify access restrictions for specific labels. Tag processes with those labels to enforce the access restrictions related to the label. | Restrict a container from accessing files outside its own filesystem. |

"Mechanisms like AppArmor and SELinux can provide protection that extends beyond the container. For example, you can use SELinux to help mitigate CVE-2019-5736."

### Considerations for managing custom configurations

"seccomp, AppArmor, and SELinux usually have a default configuration that offers basic protections. You can also create custom profiles and policies that meet the requirements of your workloads. Managing and distributing these custom configurations at scale might be challenging, especially if you use all three features together."

## Kernel-level security features and privileged containers

"Kubernetes lets you specify that some trusted containers can run in *privileged* mode. Any container in a Pod can run in privileged mode to use operating system administrative capabilities that would otherwise be inaccessible. This is available for both Windows and Linux."

"Privileged containers explicitly override some of the Linux kernel constraints that you might use in your workloads, as follows:

* **seccomp**: Privileged containers run as the `Unconfined` seccomp profile, overriding any seccomp profile that you specified in your manifest.
* **AppArmor**: Privileged containers ignore any applied AppArmor profiles.
* **SELinux**: Privileged containers run as the `unconfined_t` domain."

### Privileged containers

"Any container in a Pod can enable *Privileged mode* if you set the `privileged: true` field in the `securityContext` field for the container. Privileged containers override or undo many other hardening settings such as the applied seccomp profile, AppArmor profile, or SELinux constraints. Privileged containers are given all Linux capabilities, including capabilities that they don't require. For example, a root user in a privileged container might be able to use the `CAP_SYS_ADMIN` and `CAP_NET_ADMIN` capabilities on the node, bypassing the runtime seccomp configuration and other restrictions."

"In most cases, you should avoid using privileged containers, and instead grant the specific capabilities required by your container using the `capabilities` field in the `securityContext` field. Only use privileged mode if you have a capability that you can't grant with the securityContext. This is useful for containers that want to use operating system administrative capabilities such as manipulating the network stack or accessing hardware devices."

"In Kubernetes version 1.26 and later, you can also run Windows containers in a similarly privileged mode by setting the `windowsOptions.hostProcess` flag on the security context of the Pod spec."

## Recommendations and best practices

"* Before configuring kernel-level security capabilities, you should consider implementing network-level isolation. For more information, read the Security Checklist.
* Unless necessary, run Linux workloads as non-root by setting specific user and group IDs in your Pod manifest and by specifying `runAsNonRoot: true`."

"Additionally, you can run workloads in user namespaces by setting `hostUsers: false` in your Pod manifest. This lets you run containers as root users in the user namespace, but as non-root users in the host namespace on the node. This is still in early stages of development and might not have the level of support that you need."
```

---

### A3 · `k8s-docs-pod-security-admission-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-admission/"
fetched_at: "2026-08-31T10:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["pod-security-admission", "psa-enforce", "psa-audit", "psa-warn", "namespace-label-control-surface", "pod-security-standards", "podsecuritypolicy-removed"]
---
# Pod Security Admission (kubernetes.io/docs/concepts/security/pod-security-admission/)

All passages below are the page's own sentences, quoted exactly.

## Feature state and what it is

"Feature state: Stable since Kubernetes v1.25"

"Kubernetes offers a built-in _Pod Security_ admission controller to enforce the Pod Security Standards."

## Pod Security levels

"Pod Security admission places requirements on a Pod's Security Context and other related fields according to the three levels defined by the Pod Security Standards: `privileged`, `baseline`, and `restricted`. Refer to the Pod Security Standards page for an in-depth look at those requirements."

> NOTE FOR DRAFTING: this page does **not** restate the one-line description of each level. Those live on the Pod Security Standards page — see `k8s-docs-pod-security-standards-2026-08-23.md` and `k8s-docs-pod-security-standards-profiles-2026-08-31.md`.

## Pod Security Admission labels for namespaces

The label form:

```
pod-security.kubernetes.io/<MODE>: <LEVEL>
```

"MODE must be one of `enforce`, `audit`, or `warn`. LEVEL must be one of `privileged`, `baseline`, or `restricted`."

The three modes, exactly as the page describes them:

| Mode | Description |
|---|---|
| `enforce` | "Policy violations will cause the pod to be rejected." |
| `audit` | "Policy violations will trigger the addition of an audit annotation to the event recorded in the audit log, but are otherwise allowed." |
| `warn` | "Policy violations will trigger a user-facing warning, but are otherwise allowed." |

"A namespace can configure any or all modes, or even set a different level for different modes."

Optional per-mode version pinning:

```
pod-security.kubernetes.io/<MODE>-version: <VERSION>
```

"Optional: per-mode version label that can be used to pin the policy to the version that shipped with a given Kubernetes minor version (for example v1.37). MODE must be one of `enforce`, `audit`, or `warn`. VERSION must be a valid Kubernetes minor version, or `latest`."

## Workload resources and Pod templates

"Pods are often created indirectly, by creating a workload object such as a Deployment or Job. The workload object defines a _Pod template_ and a controller for the workload resource creates Pods based on that template. To help catch violations early, both the audit and warning modes are applied to the workload resources. However, enforce mode is **not** applied to workload resources, only to the resulting pod objects."

## Exemptions

"Exemptions can be statically configured in the Admission Controller configuration."

"Exemptions must be explicitly enumerated. Requests meeting exemption criteria are _ignored_ by the Admission Controller (all `enforce`, `audit` and `warn` behaviors are skipped)."

"Exemption dimensions include:

* **Usernames:** requests from users with an exempt authenticated (or impersonated) username are ignored.
* **RuntimeClassNames:** pods and workload resources specifying an exempt runtime class name are ignored.
* **Namespaces:** pods and workload resources in an exempt namespace are ignored."

"Most pods are created by a controller in response to a workload resource, meaning that exempting an end user will only exempt them from enforcement when creating pods directly, but not when creating a workload resource."

## PodSecurityPolicy

"If you are running an older version of Kubernetes and want to upgrade to a version of Kubernetes that does not include PodSecurityPolicies, read migrate from PodSecurityPolicy to the Built-In PodSecurity Admission Controller."

> NOTE FOR DRAFTING: the sentence "PodSecurityPolicy was removed" is **not** on this page. This page only implies removal via the migration pointer. Do not attribute a removal statement to this URL.
```

---

### A4 · `k8s-docs-pod-security-standards-profiles-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/security/pod-security-standards/"
fetched_at: "2026-08-31T10:26:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["pod-security-standards", "pss-privileged", "pss-baseline", "pss-restricted", "run-as-non-root", "run-as-user", "allow-privilege-escalation", "linux-capabilities", "privileged-container", "seccomp", "apparmor", "policy-engine"]
---
# Pod Security Standards — the profile control tables (kubernetes.io/docs/concepts/security/pod-security-standards/)

Companion to `k8s-docs-pod-security-standards-2026-08-23.md`, which carries the summary table and the three profile descriptions. This snapshot carries the per-control detail that `ch12-fig04` needs: the specific `securityContext` fields each level constrains and the values each permits.

## Summary table (repeated for context)

| Profile | Description |
|---|---|
| Privileged | "Unrestricted policy, providing the widest possible level of permissions." |
| Baseline | "Minimally restrictive policy which prevents known privilege escalations." |
| Restricted | "Heavily restricted policy, following current Pod hardening best practices." |

## Privileged

"The _Privileged_ policy is purposely-open, and entirely unrestricted." Targeted at system- and infrastructure-level workloads managed by privileged, trusted users. A Pod under it is able to bypass typical container isolation mechanisms — for example, accessing the node's host network.

## Baseline

"The _Baseline_ policy is aimed at ease of adoption for common containerized workloads while preventing known privilege escalations."

### Baseline controls, with the fields restricted and the values allowed

- **HostProcess** — disallow Windows host access.
  Fields: `spec.securityContext.windowsOptions.hostProcess`, and the `containers[*]` / `initContainers[*]` / `ephemeralContainers[*]` variants.
  Allowed: `undefined/nil`, `false`.
- **Host Namespaces** — prevent host namespace sharing.
  Fields: `spec.hostNetwork`, `spec.hostPID`, `spec.hostIPC`.
  Allowed: `undefined/nil`, `false`.
- **Privileged Containers** — disallow privileged mode.
  Fields: `spec.containers[*].securityContext.privileged` and the init/ephemeral variants.
  Allowed: `undefined/nil`, `false`.
- **Capabilities** — restrict which additional Linux capabilities may be added.
  Fields: `spec.containers[*].securityContext.capabilities.add` and variants.
  Allowed: `undefined/nil`, `AUDIT_WRITE`, `CHOWN`, `DAC_OVERRIDE`, `FOWNER`, `FSETID`, `KILL`, `MKNOD`, `NET_BIND_SERVICE`, `SETFCAP`, `SETGID`, `SETPCAP`, `SETUID`, `SYS_CHROOT`.
- **HostPath Volumes** — forbid host filesystem access.
  Fields: `spec.volumes[*].hostPath`.
  Allowed: `undefined/nil`.
- **Host Ports** — restrict or disallow direct host port binding.
  Fields: `spec.containers[*].ports[*].hostPort` and variants.
  Allowed: `undefined/nil`, a known list, `0`.
- **Host Probes / Lifecycle Hooks** (v1.34+) — disallow direct host connections.
  Fields: the probe and lifecycle-hook host fields across containers, init containers and ephemeral containers.
  Allowed: `undefined/nil`, `""`.
- **AppArmor** — enforce the default or approved profiles.
  Fields: `spec.securityContext.appArmorProfile.type` and variants.
  Allowed: `undefined/nil`, `RuntimeDefault`, `Localhost`.
  Annotation field: `metadata.annotations["container.apparmor.security.beta.kubernetes.io/*"]`; allowed `undefined/nil`, `runtime/default`, `localhost/*`.
- **SELinux** — restrict SELinux type, and forbid user/role assignment.
  Type fields: `spec.securityContext.seLinuxOptions.type` and variants. Allowed: `undefined/""`, `container_t`, `container_init_t`, `container_kvm_t`, `container_engine_t` (v1.31+).
  User/role fields: `spec.securityContext.seLinuxOptions.user`, `.role` and variants. Allowed: `undefined/""`.
- **/proc Mount Type** — require the default `/proc` masking.
  Fields: `spec.containers[*].securityContext.procMount` and variants.
  Allowed: `undefined/nil`, `Default`.
- **Seccomp** — disallow unconfined profiles.
  Fields: `spec.securityContext.seccompProfile.type` and variants.
  Allowed: `undefined/nil`, `RuntimeDefault`, `Localhost`.
- **Sysctls** — allow only safe, namespaced sysctls.
  Fields: `spec.securityContext.sysctls[*].name`.
  Allowed: `undefined/nil`, `kernel.shm_rmid_forced`, `net.ipv4.ip_local_port_range`, `net.ipv4.ip_unprivileged_port_start`, `net.ipv4.tcp_syncookies`, `net.ipv4.ping_group_range`, `net.ipv4.ip_local_reserved_ports` (v1.27+), `net.ipv4.tcp_keepalive_time` (v1.29+), `net.ipv4.tcp_fin_timeout` (v1.29+), `net.ipv4.tcp_keepalive_intvl` (v1.29+), `net.ipv4.tcp_keepalive_probes` (v1.29+).

## Restricted

"The _Restricted_ policy is aimed at enforcing current Pod hardening best practices, at the expense of some compatibility." Targeted at operators and developers of security-critical applications, and at lower-trust users.

The Restricted policy is cumulative: it includes every Baseline requirement, plus the following.

- **Volume Types** — limit to the safe volume types.
  Fields: `spec.volumes[*]`.
  Allowed: `configMap`, `csi`, `downwardAPI`, `emptyDir`, `ephemeral`, `persistentVolumeClaim`, `projected`, `secret`.
- **Privilege Escalation** (v1.8+) — prevent setuid/setgid escalation.
  Fields: `spec.containers[*].securityContext.allowPrivilegeEscalation` and variants.
  Allowed: `false`. (Linux only, v1.25+.)
- **Running as Non-root** — require non-root execution.
  Fields: `spec.securityContext.runAsNonRoot` and the container/init/ephemeral variants.
  Allowed: `true`.
- **Running as Non-root user** (v1.23+) — forbid UID 0.
  Fields: `spec.securityContext.runAsUser` and variants.
  Allowed: any non-zero value, or `undefined/null`.
- **Seccomp** (v1.19+) — mandate explicit confinement.
  Fields: `spec.securityContext.seccompProfile.type` and variants.
  Allowed: `RuntimeDefault`, `Localhost`. (Linux only, v1.25+.)
- **Capabilities** (v1.22+) — drop all, and optionally add back only `NET_BIND_SERVICE`.
  Drop fields: `spec.containers[*].securityContext.capabilities.drop` and variants. Allowed: any list containing `ALL`.
  Add fields: `spec.containers[*].securityContext.capabilities.add` and variants. Allowed: `undefined/nil`, `NET_BIND_SERVICE`. (Linux only, v1.25+.)

## Policy Instantiation

"Decoupling policy definition from policy instantiation allows for a common understanding and consistent language of policies across clusters, independent of the underlying enforcement mechanism."

Enforcement mechanisms named on the page include the built-in Pod Security Admission controller and third-party tools such as Kubewarden, Kyverno and OPA Gatekeeper.

## FAQ — why is there no profile between privileged and baseline?

"The three profiles defined here have a clear linear progression from most secure (Restricted) to least secure (Privileged), and cover a broad set of workloads. Privileges required above the Baseline policy are typically very application specific, so we do not offer a standard profile in this niche."
```

---

### A5 · `k8s-docs-encrypt-data-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/"
fetched_at: "2026-08-31T10:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["encryption-at-rest", "encryptionconfiguration", "secret-storage-default-unencrypted", "secret-hardening"]
---
# Encrypting Confidential Data at Rest (kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

## Opening

"All of the APIs in Kubernetes that let you write persistent API resource data support at-rest encryption. For example, you can enable at-rest encryption for Secrets. This at-rest encryption is additional to any system-level encryption for the etcd cluster or for the filesystem(s) on hosts where you are running the kube-apiserver."

"This page shows how to enable and configure encryption of API data at rest."

"This task covers encryption for resource data stored using the Kubernetes API. For example, you can encrypt Secret objects, including the key-value data they contain."

**Note (scope):** "This task covers encryption for resource data stored using the Kubernetes API. If you want to encrypt data in filesystems that are mounted into containers, you instead need to either: use a storage integration that provides encrypted volumes [or] encrypt the data within your own application."

**"By default, the API server stores plain-text representations of resources into etcd, with no at-rest encryption."**

## Determining whether encryption at rest is already enabled

"The `kube-apiserver` process accepts an argument `--encryption-provider-config` that specifies a path to a configuration file. The contents of that file, if you specify one, control how Kubernetes API data is encrypted in etcd. If you are running the kube-apiserver without the `--encryption-provider-config` command line argument, you do not have encryption at rest enabled. If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies the `identity` provider as the first encryption provider in the list, then you do not have at-rest encryption enabled (the default `identity` provider does not provide any confidentiality protection)."

"If you are running the kube-apiserver with the `--encryption-provider-config` command line argument, and the file that it references specifies a provider other than `identity` as the first encryption provider in the list, then you already have at-rest encryption enabled."

## The EncryptionConfiguration resource

The configuration object is an `EncryptionConfiguration` in the `apiserver.config.k8s.io/v1` API group. It names the API kinds to encrypt and an ordered list of providers:

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: <base64-encoded-key>
      - identity: {}
```

"The first provider in the list is used to encrypt resources written into the storage. When reading resources from storage, each provider that matches the stored data attempts in order to decrypt the data. If no provider can read the stored data due to a mismatch in format or secret key, an error is returned which prevents clients from accessing that resource."

**Note:** "Use of wildcards that overlap within the same resource list or across multiple entries are not allowed since part of the configuration would be ineffective."

## Providers

The page's provider table covers `identity`, `aescbc`, `aesgcm`, `kms` v1 (deprecated since v1.28), `kms` v2 and `secretbox`. The page's own characterisations:

- `identity` — no encryption. "The default `identity` provider does not provide any confidentiality protection." Resources are written unencrypted.
- `aescbc` — AES-CBC with PKCS#7 padding; 16, 24 or 32-byte keys. Strength: **weak**. "Not recommended due to CBC's vulnerability to padding oracle attacks. Key material accessible from control plane host."
- `aesgcm` — AES-GCM with a random nonce; 16, 24 or 32-byte keys. "Not recommended for use except when an automated key rotation scheme is implemented. Key material accessible from control plane host." Must be rotated every 200,000 writes.
- `kms` v1 — "Data is encrypted by data encryption keys (DEKs) using AES-GCM; DEKs are encrypted by key encryption keys (KEKs) according to configuration in Key Management Service (KMS)." Strongest; slower than v2; 32-byte keys. Deprecated since v1.28.
- `kms` v2 — "Data is encrypted by data encryption keys (DEKs) using AES-GCM; DEKs are encrypted by key encryption keys (KEKs) according to configuration in Key Management Service (KMS). Kubernetes generates a new DEK per encryption from a secret seed." Strongest; fast; 32-byte keys.
- `secretbox` — XSalsa20 and Poly1305; 32-byte keys. "Uses relatively new encryption technologies that may not be considered acceptable in environments that require high levels of review."

## Cautions and warnings on the page

**On what a locally managed key does and does not defend against:**
"Encrypting secret data with a locally managed key protects against an etcd compromise, but it fails to protect against a host compromise. Since the encryption keys are stored on the host in the EncryptionConfiguration YAML file, a skilled attacker can access that file and extract the encryption keys."

"In the KMS case, an attacker who intends to get unauthorised access to the plaintext values would need to compromise etcd **and** the third-party KMS provider."

**Caution:** "Storing the raw encryption key in the EncryptionConfig only moderately improves your security posture, compared to no encryption."

**Caution:** "The encryption configuration file may contain keys that can decrypt content in etcd. If the configuration file contains any key material, you must properly restrict permissions on all your control plane hosts so only the user who runs the kube-apiserver can read this configuration."

**Caution:** "If any resource is not readable via the encryption configuration (because keys were changed), and you cannot restore a working configuration, your only recourse is to delete that entry from the underlying etcd directly."

**Caution (multi-control-plane):** "For cluster configurations with two or more control plane nodes, the encryption configuration should be identical across each control plane node. If there is a difference in the encryption provider configuration between control plane nodes, this difference may mean that the kube-apiserver can't decrypt data."

**Warning:** "Making this change prevents the API server from retrieving resources that are marked as encrypted at rest, but are actually stored in the clear. When you have configured encryption at rest for an API (for example: the API kind `Secret`, representing `secrets` resources in the core API group), you **must** ensure that all those resources in this cluster really are encrypted at rest."

**Note:** "Keep the encryption key confidential, including while you generate it and ideally even after you are no longer actively using it."

## Ensure all relevant data are encrypted

"It's often not enough to make sure that new objects get encrypted: you also want that encryption to apply to the objects that are already stored. For this example, you have configured your cluster so that Secrets are encrypted on write. Performing a replace operation for each Secret will encrypt that content at rest, where the objects are unchanged. You can make this change across all Secrets in your cluster:"

```
kubectl get secrets --all-namespaces -o json | kubectl replace -f -
```

"The command above reads all Secrets and then updates them with the same data, in order to apply server side encryption."

**Note:** "If an error occurs due to a conflicting write, retry the command. It is safe to run that command more than once. For larger clusters, you may wish to subdivide the Secrets by namespace, or script an update."

## Verify that data is encrypted

"Data is encrypted when written to etcd. After restarting your kube-apiserver, any newly created or updated Secret (or other resource kinds configured in EncryptionConfiguration) should be encrypted when stored. To check this, you can use the `etcdctl` command line program to retrieve the contents of your secret data."

Verification is by reading the raw etcd value and confirming it carries the provider prefix (for example `k8s:enc:aescbc:v1:`) rather than plaintext.

## ⚠ WHAT THIS PAGE DOES *NOT* SAY — read before drafting §4

The outline expects a statement that encryption at rest "protects the object as written to etcd and not the object as returned by the API to an authorized caller." **That sentence is not on this page in that form.** What is sourced is the pair above: encryption at rest defends against an etcd compromise but not a host compromise, and (from `k8s-docs-secret-risks-2026-08-31.md`) "Anyone with API access can retrieve or modify a Secret". The distinction §4 wants must be built by the author from those two sourced facts and marked accordingly — it must not be quoted as a documentation sentence.
```

---

### A6 · `k8s-docs-rbac-good-practices-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/security/rbac-good-practices/"
fetched_at: "2026-08-31T10:41:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["least-privilege", "rbac", "pod-creation-privilege-escalation", "secret-exposure-paths", "workload-to-host-boundary", "namespace-label-control-surface", "default-role-cluster-admin", "tokenrequest"]
---
# Role Based Access Control Good Practices (kubernetes.io/docs/concepts/security/rbac-good-practices/)

Full page, transcribed. This is the authoritative home of the privilege-escalation framing that Ch 12 §3 and §4 both lean on.

"Kubernetes RBAC is a key security control to ensure that cluster users and workloads have only the access to resources required to execute their roles. It is important to ensure that, when designing permissions for cluster users, the cluster administrator understands the areas where privilege escalation could occur, to reduce the risk of excessive access leading to security incidents."

"The good practices laid out here should be read in conjunction with the general RBAC documentation."

## General good practice

### Least privilege

"Ideally, minimal RBAC rights should be assigned to users and service accounts. Only permissions explicitly required for their operation should be used. While each cluster will be different, some general rules that can be applied are:

- Assign permissions at the namespace level where possible. Use RoleBindings as opposed to ClusterRoleBindings to give users rights only within a specific namespace.
- Avoid providing wildcard permissions when possible, especially to all resources. As Kubernetes is an extensible system, providing wildcard access gives rights not just to all object types that currently exist in the cluster, but also to all object types which are created in the future.
- Administrators should not use `cluster-admin` accounts except where specifically needed. Providing a low privileged account with impersonation rights can avoid accidental modification of cluster resources.
- Avoid adding users to the `system:masters` group. Any user who is a member of this group bypasses all RBAC rights checks and will always have unrestricted superuser access, which cannot be revoked by removing RoleBindings or ClusterRoleBindings. As an aside, if a cluster is using an authorization webhook, membership of this group also bypasses that webhook (requests from users who are members of that group are never sent to the webhook)."

### Minimize distribution of privileged tokens

"Ideally, pods shouldn't be assigned service accounts that have been granted powerful permissions (for example, any of the rights listed under privilege escalation risks). In cases where a workload requires powerful permissions, consider the following practices:

- Limit the number of nodes running powerful pods. Ensure that any DaemonSets you run are necessary and are run with least privilege to limit the blast radius of container escapes.
- Avoid running powerful pods alongside untrusted or publicly-exposed ones. Consider using Taints and Toleration, NodeAffinity, or PodAntiAffinity to ensure pods don't run alongside untrusted or less-trusted Pods. Pay special attention to situations where less-trustworthy Pods are not meeting the **Restricted** Pod Security Standard."

### Hardening

"Kubernetes defaults to providing access which may not be required in every cluster. Reviewing the RBAC rights provided by default can provide opportunities for security hardening. In general, changes should not be made to rights provided to `system:` accounts some options to harden cluster rights exist:

- Review bindings for the `system:unauthenticated` group and remove them where possible, as this gives access to anyone who can contact the API server at a network level.
- Avoid the default auto-mounting of service account tokens by setting `automountServiceAccountToken: false`. For more details, see using default service account token. Setting this value for a Pod will overwrite the service account setting, workloads which require service account tokens can still mount them."

### Periodic review

"It is vital to periodically review the Kubernetes RBAC settings for redundant entries and possible privilege escalations. If an attacker is able to create a user account with the same name as a deleted user, they can automatically inherit all the rights of the deleted user, especially the rights assigned to that user."

## Kubernetes RBAC - privilege escalation risks

"Within Kubernetes RBAC there are a number of privileges which, if granted, can allow a user or a service account to escalate their privileges in the cluster or affect systems outside the cluster."

"This section is intended to provide visibility of the areas where cluster operators should take care, to ensure that they do not inadvertently allow for more access to clusters than intended."

### Listing secrets

"It is generally clear that allowing `get` access on Secrets will allow a user to read their contents. It is also important to note that `list` and `watch` access also effectively allow for users to reveal the Secret contents. For example, when a List response is returned (for example, via `kubectl get secrets -A -o yaml`), the response includes the contents of all Secrets."

### Workload creation

"Permission to create workloads (either Pods, or workload resources that manage Pods) in a namespace implicitly grants access to many other resources in that namespace, such as Secrets, ConfigMaps, and PersistentVolumes that can be mounted in Pods. Additionally, since Pods can run as any ServiceAccount, granting permission to create workloads also implicitly grants the API access levels of any service account in that namespace."

"Users who can run privileged Pods can use that access to gain node access and potentially to further elevate their privileges. Where you do not fully trust a user or other principal with the ability to create suitably secure and isolated Pods, you should enforce either the **Baseline** or **Restricted** Pod Security Standard. You can use Pod Security admission or other (third party) mechanisms to implement that enforcement."

"For these reasons, namespaces should be used to separate resources requiring different levels of trust or tenancy. It is still considered best practice to follow least privilege principles and assign the minimum set of permissions, but boundaries within a namespace should be considered weak."

### Persistent volume creation

"If someone - or some application - is allowed to create arbitrary PersistentVolumes, that access includes the creation of `hostPath` volumes, which then means that a Pod would get access to the underlying host filesystem(s) on the associated node. Granting that ability is a security risk."

"There are many ways a container with unrestricted access to the host filesystem can escalate privileges, including reading data from other containers, and abusing the credentials of system services, such as Kubelet."

"You should only allow access to create PersistentVolume objects for:

- Users (cluster operators) that need this access for their work, and who you trust.
- The Kubernetes control plane components which creates PersistentVolumes based on PersistentVolumeClaims that are configured for automatic provisioning. This is usually setup by the Kubernetes provider or by the operator when installing a CSI driver."

"Where access to persistent storage is required trusted administrators should create PersistentVolumes, and constrained users should use PersistentVolumeClaims to access that storage."

### Access to `proxy` subresource of Nodes

"Users with access to the `nodes/proxy` sub-resource have rights to the Kubelet API, which allows for command execution on every pod on the node(s) to which they have rights. This access bypasses audit logging and admission control, so care should be taken before granting any rights to this resource. These APIs can be exercised via websocket HTTP `GET` requests, which only requires authorization of the **get** verb. This means that **get** permission on `nodes/proxy` is not a read-only permission. For example, permission to **get** `nodes/proxy` provides access to privileged kubelet APIs that can retrieve container logs or execute and attach to pod processes, even when a caller does not have the equivalent permissions through the Kubernetes API."

### Escalate verb

"Generally, the RBAC system prevents users from creating clusterroles with more rights than the user possesses. The exception to this is the `escalate` verb. As noted in the RBAC documentation, users with this right can effectively escalate their privileges."

### Bind verb

"Similar to the `escalate` verb, granting users this right allows for the bypass of Kubernetes in-built protections against privilege escalation, allowing users to create bindings to roles with rights they do not already have."

### Impersonate verb

"This verb allows users to impersonate and gain the rights of other users in the cluster. Care should be taken when granting it, to ensure that excessive permissions cannot be gained via one of the impersonated accounts."

### CSRs and certificate issuing

"The CSR API allows for users with `create` rights to CSRs and `update` rights on `certificatesigningrequests/approval` where the signer is `kubernetes.io/kube-apiserver-client` to create new client certificates which allow users to authenticate to the cluster. Those client certificates can have arbitrary names including duplicates of Kubernetes system components. This will effectively allow for privilege escalation."

### Token request

"Users with `create` rights on `serviceaccounts/token` can create TokenRequests to issue tokens for existing service accounts."

### Control admission webhooks

"Users with control over `validatingwebhookconfigurations` or `mutatingwebhookconfigurations` can control webhooks that can read any object admitted to the cluster, and in the case of mutating webhooks, also mutate admitted objects."

### Namespace modification

"Users who can perform **patch** operations on Namespace objects (through a namespaced RoleBinding to a Role with that access) can modify labels on that namespace. In clusters where Pod Security Admission is used, this may allow a user to configure the namespace for a more permissive policy than intended by the administrators. For clusters where NetworkPolicy is used, users may be set labels that indirectly allow access to services that an administrator did not intend to allow."

## Kubernetes RBAC - denial of service risks

### Object creation denial-of-service

"Users who have rights to create objects in a cluster may be able to create sufficient large objects to create a denial of service condition either based on the size or number of objects, as discussed in etcd used by Kubernetes is vulnerable to OOM attack. This may be specifically relevant in multi-tenant clusters if semi-trusted or untrusted users are allowed limited access to a system."

"One option for mitigation of this issue would be to use resource quotas to limit the quantity of objects which can be created."
```

---

### A7 · `k8s-docs-rbac-depth-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/rbac/"
fetched_at: "2026-08-31T10:48:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["aggregated-clusterrole", "subjects-are-named-not-selected", "rule-verb-resource", "default-role-admin", "default-role-edit", "default-role-view", "binding-immutability", "least-privilege"]
---
# Using RBAC Authorization — depth passages (kubernetes.io/docs/reference/access-authn-authz/rbac/)

Companion to `k8s-docs-rbac-2026-08-23.md`, which carries the four API objects, the additive rule, the binding-immutability sentence and the four default roles at summary level. This snapshot carries the passages that chapter 12 §3 needs and that snapshot does not have. Transcribed from the page's markdown source; YAML examples omitted, Hugo shortcodes left in place where they sit inside a sentence.

## Referring to resources — resourceNames

"You can also refer to resources by name for certain requests through the `resourceNames` list. When specified, requests can be restricted to individual instances of a resource."

**Note:** "You cannot restrict **deletecollection** or top-level **create** requests by resource name. For **create**, this limitation is because the name of the new object may not be known at authorization time. However, the **create** limitation applies only to top-level resources, not subresources. For example, you can use the `resourceNames` field with `pods/exec`. If you restrict **list** or **watch** by `resourceName`, clients must include a `metadata.name` field selector in their **list** or **watch** request (that matches the specified `resourceName`) in order to be authorized. For example: `kubectl get configmaps --field-selector=metadata.name=my-configmap`"

## Aggregated ClusterRoles

"You can _aggregate_ several ClusterRoles into one combined ClusterRole. A controller, running as part of the cluster control plane, watches for ClusterRole objects with an `aggregationRule` set. The `aggregationRule` defines a label selector that the controller uses to match other ClusterRole objects that should be combined into the `rules` field of this one."

"If you create a new ClusterRole that matches the label selector of an existing aggregated ClusterRole, that change triggers adding the new rules into the aggregated ClusterRole."

"The default user-facing roles use ClusterRole aggregation. This lets you, as a cluster administrator, include rules for custom resources, such as those served by CustomResourceDefinitions or aggregated API servers, to extend the default roles."

"For example: the following ClusterRoles let the "admin" and "edit" default roles manage the custom resource named CronTab, whereas the "view" role can perform only read actions on CronTab resources. You can assume that CronTab objects are named `"crontabs"` in URLs as seen by the API server."

## Referring to subjects

"A RoleBinding or ClusterRoleBinding binds a role to subjects. Subjects can be group, users or ServiceAccounts."

"Kubernetes represents usernames as strings. These can be: plain names, such as "alice"; email-style names, like "bob@example.com"; or numeric user IDs represented as a string. It is up to you as a cluster administrator to configure the authentication modules so that authentication produces usernames in the format you want."

"In Kubernetes, Authenticator modules provide group information. Groups, like users, are represented as strings, and that string has no format requirements, other than that the prefix `system:` is reserved."

"ServiceAccounts have names prefixed with `system:serviceaccount:`, and belong to groups that have names prefixed with `system:serviceaccounts:`."

> NOTE FOR DRAFTING (§3, debt `chapter-04:839`): the docs state that subjects are *named strings*. They do **not** contain a sentence explaining *why* RBAC names subjects instead of selecting them. See § Gaps.

## Privilege escalation prevention and bootstrapping

"The RBAC API prevents users from escalating privileges by editing roles or role bindings. Because this is enforced at the API level, it applies even when the RBAC authorizer is not in use."

### Restrictions on role creation or update

"You can only create/update a role if at least one of the following things is true:

1. You already have all the permissions contained in the role, at the same scope as the object being modified (cluster-wide for a ClusterRole, within the same namespace or cluster-wide for a Role).
2. You are granted explicit permission to perform the `escalate` verb on the `roles` or `clusterroles` resource in the `rbac.authorization.k8s.io` API group."

"For example, if `user-1` does not have the ability to list Secrets cluster-wide, they cannot create a ClusterRole containing that permission. To allow a user to create/update roles:

1. Grant them a role that allows them to create/update Role or ClusterRole objects, as desired.
2. Grant them permission to include specific permissions in the roles they create/update:
   * implicitly, by giving them those permissions (if they attempt to create or modify a Role or ClusterRole with permissions they themselves have not been granted, the API request will be forbidden)
   * or explicitly allow specifying any permission in a `Role` or `ClusterRole` by giving them permission to perform the `escalate` verb on `roles` or `clusterroles` resources in the `rbac.authorization.k8s.io` API group"

### Restrictions on role binding creation or update

"You can only create/update a role binding if you already have all the permissions contained in the referenced role (at the same scope as the role binding) *or* if you have been authorized to perform the `bind` verb on the referenced role. For example, if `user-1` does not have the ability to list Secrets cluster-wide, they cannot create a ClusterRoleBinding to a role that grants that permission. To allow a user to create/update role bindings:

1. Grant them a role that allows them to create/update RoleBinding or ClusterRoleBinding objects, as desired.
2. Grant them permissions needed to bind a particular role:
   * implicitly, by giving them the permissions contained in the role.
   * explicitly, by giving them permission to perform the `bind` verb on the particular Role (or ClusterRole)."

"When bootstrapping the first roles and role bindings, it is necessary for the initial user to grant permissions they do not yet have. To bootstrap initial roles and role bindings:

* Use a credential with the "system:masters" group, which is bound to the "cluster-admin" super-user role by the default bindings."

## Default roles and role bindings — the `admin`, `edit` and `view` Description cells, in full

**`admin`:** "If used in a **RoleBinding**, allows read/write access to most resources in a namespace, including the ability to create roles and role bindings within the namespace. This role does not allow write access to resource quota or to the namespace itself. This role also does not allow write access to EndpointSlices in clusters created using Kubernetes v1.22+. More information is available in the "Write Access for EndpointSlices" section."

**`edit`:** "This role does not allow viewing or modifying roles or role bindings. However, this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. This role also does not allow write access to EndpointSlices in clusters created using Kubernetes v1.22+. More information is available in the "Write Access for EndpointSlices" section."

**`view`:** "Allows read-only access to see most objects in a namespace. It does not allow viewing roles or role bindings. This role does not allow viewing Secrets, since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation)."

> ⚠ FACT-CHECK FOR §3 AND B1 TRAP #58. The `edit` role **does** allow *accessing* Secrets, per the sentence above; what it does not allow is viewing or modifying roles and role bindings. The book must not state that `edit` cannot read Secrets. `view` is the role that cannot. Trap #58 as inventoried ("`edit` can manage RBAC in its namespace → it cannot; `admin` can") is correct and is directly supported.

## Bootstrapping and auto-reconciliation

Default ClusterRoles and ClusterRoleBindings are labelled `kubernetes.io/bootstrapping=rbac-defaults`. The API server reconciles the defaults at startup, restoring missing permissions and subjects. Auto-reconciliation can be disabled per object by setting the `rbac.authorization.kubernetes.io/autoupdate` annotation to `false`, which the page warns may leave a non-functional cluster.

## Discovery roles

| Default ClusterRole | Default ClusterRoleBinding | Description |
|---|---|---|
| `system:basic-user` | `system:authenticated` group | Read-only access to basic self-information |
| `system:discovery` | `system:authenticated` group | Read-only access to API discovery endpoints |
| `system:public-info-viewer` | `system:authenticated` and `system:unauthenticated` groups | Read-only access to non-sensitive cluster information |

## Command-line utilities

The page documents `kubectl create role`, `kubectl create clusterrole`, `kubectl create rolebinding`, `kubectl create clusterrolebinding` and `kubectl auth reconcile`. `kubectl create role` creates a Role within a single namespace; `kubectl create clusterrole` creates a ClusterRole, which additionally supports non-resource URLs (for example `/logs/*`) and aggregation rules; `kubectl create rolebinding` grants a Role or ClusterRole within a namespace; `kubectl create clusterrolebinding` grants a ClusterRole cluster-wide. `kubectl auth reconcile` creates or updates RBAC objects from manifest files and supports `--remove-extra-permissions` and `--remove-extra-subjects`.

> FIDELITY NOTE: the "Bootstrapping", "Discovery roles" and "Command-line utilities" paragraphs immediately above are **condensed**, not verbatim. Do not quote them as documentation sentences. Everything above them in this file is transcribed.
```

---

### A8 · `k8s-docs-authorization-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/reference/access-authn-authz/authorization/"
fetched_at: "2026-08-31T10:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["authorization-mode", "rbac", "kubectl-auth-can-i", "rule-verb-resource"]
---
# Authorization (kubernetes.io/docs/reference/access-authn-authz/authorization/)

This is the source for §3's one-clause ABAC disposal (Open question #8) — the clause that must be written before ABAC may be used as a distractor.

## Default deny

"All parts of an API request must be allowed by some authorization mechanism in order to proceed."

## How multiple authorizers combine

"[Each authorizer] is checked in sequence. If any authorizer approves or denies a request, that decision is immediately returned and no other authorizer is consulted. If all modules have no opinion on the request, then the request is denied."

## Request attributes considered

Authorization decisions consider these API request attributes: the user, group membership, extra metadata, whether the request is for an API resource, the request path, the API request verb (`get`, `list`, `create`, `update`, `patch`, `watch`, `delete`, `deletecollection`), the HTTP request verb, the resource name/ID, the subresource, the namespace, and the API group.

## Authorization modules

**Node** — "A special-purpose authorization mode that grants permissions to kubelets based on the pods they are scheduled to run."

**ABAC** — "Kubernetes ABAC mode defines an access control paradigm whereby access rights are granted to users through the use of policies which combine attributes together."

**RBAC** — "Kubernetes RBAC is a method of regulating access to computer or network resources based on the roles of individual users within an enterprise."

**Webhook** — "Kubernetes webhook mode for authorization makes a synchronous HTTP callout, blocking the request until the remote HTTP service responds to the query."

## Checking API access

Users can check their own authorization with `kubectl auth can-i`, which queries the authorization layer to determine whether an action is permitted. The `--as` flag impersonates another user or service account, so an administrator can check what another principal is permitted to do.

> FIDELITY NOTE: the "Request attributes considered" and "Checking API access" paragraphs are **condensed**, not verbatim; the four module descriptions and the two sentences above them are the page's own words. Do not quote the condensed paragraphs as documentation sentences.
```

---

### A9 · `k8s-docs-4cs-cloud-native-security-v1-22-archived-2026-08-31.md` (new)
```markdown
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
```

---

### A10 · `notary-project-signing-digest-2026-08-31.md` (new)
```markdown
---
source_url: "https://notaryproject.dev/"
secondary_source_url: "https://notaryproject.dev/docs/quickstart-guides/quickstart-sign-image-artifact/"
fetched_at: "2026-08-31T11:10:00-0400"
authority: "Notary Project (CNCF incubating)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["notary", "image-signing", "signature-binds-to-digest", "attestation", "supply-chain-security", "private-registry-restriction"]
---
# Notary Project (notaryproject.dev) — and the digest-binding fact

## What it is

"A set of specifications and tools intended to provide a cross-industry standard for securing software supply chains."

"Signing and verifying artifacts. Safeguarding the software delivery security from development to deployment."

"Signing and validating software artifacts, ensure they have not been tampered with and provide security policies to determine which validated artifacts are allowed to be used in your systems"

"Able to custom trust policy and determine if a signed artifact is considered authentic"

Tooling: **Notation** is the project's CLI. "Notary Project is a CNCF incubating project"

## ★ A signature binds to a digest, not a tag

From the project's quickstart for signing a container image artifact:

**"Notation resolves the tag to the digest before signing if a tag is used to identify the container image."**

**"Always reference and use the image digest instead of a tag since digest is immutable."**

> This is the primary-source basis for Chapter 12 §7's Fixed Point and for the Ch 2 §3 retrieval (tags are mutable pointers; digests are identity). It is a *Notary Project* statement, not a Kubernetes one — attribute it to the Notary Project. The equivalent Cosign statement could not be located on docs.sigstore.dev; see § Gaps.
```

---

### A11 · `in-toto-overview-2026-08-31.md` (new)
```markdown
---
source_url: "https://in-toto.io/"
fetched_at: "2026-08-31T11:14:00-0400"
authority: "in-toto project (CNCF graduated)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["in-toto", "provenance", "attestation", "supply-chain-security"]
---
# in-toto (in-toto.io)

"A framework to secure the integrity of software supply chains"

"in-toto is designed to ensure the integrity of a software product from initiation to end-user installation. It does so by making it transparent to the user what steps were performed, by whom and in what order."

"in-toto is a CNCF graduated project."

> NOTE FOR DRAFTING (§7, one sentence): the sentence above — *what steps were performed, by whom and in what order* — is in substance the definition of **provenance**, and is the strongest sourced statement of that concept in this corpus. The word "provenance" itself does not appear on this landing page; see § Gaps. Supply-chain layout, link metadata and steps/inspections are **not** covered on this page and must not be described.
```

---

### A12 · `tuf-overview-2026-08-31.md` (new)
```markdown
---
source_url: "https://theupdateframework.io/"
secondary_source_url: "https://theupdateframework.io/docs/overview/"
fetched_at: "2026-08-31T11:17:00-0400"
authority: "The Update Framework (CNCF graduated)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["tuf", "supply-chain-security", "image-signing"]
---
# The Update Framework — TUF (theupdateframework.io)

## What it is

"A framework for securing software update systems"

"maintains the security of software update systems, providing protection even against attackers that compromise the repository or signing keys"

"**TUF** is a CNCF graduated project."

## From the project overview

"[TUF is] a framework (a set of libraries, file formats, and utilities) that can be used to secure new and existing software update systems."

The overview lists attacks TUF is designed to withstand, in the project's own words:

- "An attacker keeps giving you the same file, so you never realize there is an update."
- "An attacker gives you an older, insecure version of a file that you already have and tricks you into thinking it's newer."
- "An attacker gives you a newer version of a file you have but it's still not the newest one."
- "An attacker compromises the key used to sign these files. Now you download a file that is properly signed, but is still malicious."

"TUF identifies the updates, downloads them, and checks them against the metadata that it also downloads from the repository. If the downloaded target files are trustworthy, TUF hands them over to your software update system."

> NOTE: TUF's role structure (root / targets / snapshot / timestamp), delegation and signing thresholds are **not** on these two pages. Do not describe them.
```

---

### A13 · `harbor-overview-2026-08-31.md` (new)
```markdown
---
source_url: "https://goharbor.io/"
fetched_at: "2026-08-31T11:20:00-0400"
authority: "Harbor project (CNCF graduated)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["harbor", "image-scanning", "image-signing", "private-registry-restriction", "rbac", "supply-chain-security"]
---
# Harbor (goharbor.io)

"Our mission is to be the trusted cloud native repository for Kubernetes"

"Harbor is an open source registry that secures artifacts with policies and role-based access control, ensures images are scanned and free from vulnerabilities, and signs images as trusted."

"Harbor, a CNCF Graduated project, delivers compliance, performance, and interoperability to help you consistently and securely manage artifacts across cloud native compute platforms like Kubernetes and Docker."

Features named on the page include: "Security and vulnerability analysis", "Content signing and validation", "Identity integration and role-based access control", "Multi-tenant", "Replication across many registries, including Harbor", and "Extensible API and web UI".

> NOTE: an explicit statement of OCI compliance is **not** on this page. §7's *restrict* checkpoint may cite Harbor as an instance of a private registry with RBAC and scanning; it may not claim OCI conformance from this source.
```

---

### A14 · `sbom-standards-spdx-cyclonedx-2026-08-31.md` (new)
```markdown
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
```

---

### A15 · `cncf-glossary-policy-as-code-2026-08-31.md` (new)
```markdown
---
source_url: "https://glossary.cncf.io/policy-as-code/"
fetched_at: "2026-08-31T11:30:00-0400"
authority: "CNCF Cloud Native Glossary — CC BY 4.0, The Linux Foundation / CNCF"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["policy-engine", "validate-mutate-generate", "opa", "kyverno", "admission-time-vs-runtime"]
---
# Policy as Code (PaC) — CNCF Cloud Native Glossary (glossary.cncf.io/policy-as-code/)

## What it is

"Policy as Code is the practice of storing the definition of policies as one or more files in machine-readable and processable form."

## Problem it addresses

Organizations implement numerous policies — for example security restrictions on secrets in source code, or on container permissions — that developers must verify. Checking policy compliance manually is resource-intensive and error-prone, and struggles to keep pace with the demands of cloud native applications.

## How it helps

Codifying policies enables consistent, automated enforcement while reducing human error. Version control systems such as Git track policy changes, creating an audit trail and allowing teams to identify who made a change and to revert it.

> FIDELITY NOTE: only the "What it is" sentence is verbatim. The "Problem it addresses" and "How it helps" paragraphs are **condensed** from the entry and must not be quoted as the glossary's own wording. The load-bearing sentence for §8 is the first one, and it is exact.
>
> The CNCF glossary index was checked on 2026-08-31 for security and supply-chain terms. The complete list of relevant entries is: Cloud Native Security, DevSecOps, Digital Certificate, Mutual Transport Layer Security (mTLS), Policy as Code (PaC), Role-Based Access Control (RBAC), Security Chaos Engineering, Transport Layer Security (TLS), Zero Trust Architecture. **There is no SBOM entry and no supply-chain-security entry.**
```

---

### A16 · `k8s-docs-secret-risks-2026-08-31.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/configuration/secret/"
fetched_at: "2026-08-31T11:36:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — CC BY 4.0, The Kubernetes Authors"
objectives_covered: ["D2 Security", "D2.2"]
concepts_covered: ["secret-storage-default-unencrypted", "secret-exposure-paths", "pod-creation-privilege-escalation", "privileged-container", "file-mount-over-env-var", "secret-hardening"]
---
# Secret — the risks and information-security sections (kubernetes.io/docs/concepts/configuration/secret/)

Companion to `k8s-docs-secret-2026-08-23.md` (which carries the object, the types, and base64) and `k8s-docs-secrets-good-practices-2026-08-24.md` (which carries the four hardening items). This snapshot carries the exposure statements §4 is built on.

## The headline caution

**"Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd."**

The recommendations that follow it: enable encryption at rest for Secrets; configure RBAC rules with least-privilege access to Secrets; restrict Secret access to specific containers; and consider using external Secret store providers.

## Information security for Secrets

Kubernetes applies protections to Secrets beyond those given to ConfigMaps:

- A Secret is only sent to a node if a Pod on that node requires it.
- The kubelet stores its copy in a temporary filesystem (tmpfs) rather than on durable storage.
- Once the Pods that depend on the Secret are deleted, the local copies are removed.

On authorization: granting `list` or `watch` on Secrets allows reading all Secret data in a namespace, not only the Secrets a caller explicitly names. Access should be restricted to the minimum necessary, and broad roles such as `cluster-admin` avoided unless administratively required.

**A container running with `privileged: true` can access all Secrets on that node.**

## Secret updates: mounted volume versus environment variable

When a Secret is mounted as a volume, updates propagate to the Pod automatically. "A container using a Secret as a subPath volume mount does not receive automated Secret updates."

## ⚠ WHAT THIS PAGE DOES *NOT* SAY — read before drafting §4's file-over-env-var argument

`chapter-11:444` promised the reader: *"File over environment variable is half an argument already, and you now hold that half."* The half the reader holds is tmpfs.

**The other half, as commonly stated in prep material — that environment variables leak into logs, `kubectl describe` output, crash reports or child processes — is NOT stated anywhere on kubernetes.io in this corpus.** It was searched for and not found.

What *is* sourced, and what §4 may therefore argue:
1. A mounted Secret's updates propagate; an environment variable is fixed at container start (this page).
2. "If you are defining multiple containers in a Pod, and only one of those containers needs access to a Secret, define the volume mount or environment variable configuration so that the other containers do not have access to that Secret" (`k8s-docs-secrets-good-practices-2026-08-24.md`).
3. "Applications still need to protect the value of confidential information after reading it from an environment variable or volume. For example, your application must avoid logging the secret data in the clear or transmitting it to an untrusted party" (same page) — note this warns about the *application's* handling, symmetrically for both mechanisms; it is **not** a claim that env vars specifically leak.

The §4 argument must be built from (1) and (2), or marked `[inferred]`. See § Gaps.
```

---

## Gaps

Flagged for the drafting stage. **Do not invent facts to fill these.**

### G-A · CVE has no primary-source definition in this corpus — **blocks one clause of §7**

`cve` is in `kb_tags.concepts` and §7's *scan* checkpoint is specified to cover "image scanning and what a CVE is."

- `cve.org/About/Overview` and `cve.org/ResourcesSupport/FAQs` are client-rendered and return no body to automated retrieval.
- `nvd.nist.gov/general/FAQ-Sections/General-FAQs` likewise returns no body.
- `cve.mitre.org/about/faqs.html` 301-redirects into the CVE Program's archived-website index, from which only two sentences survive: **"The mission of the CVE™ Program is to identify, define, and catalog publicly disclosed cybersecurity vulnerabilities."** and **"CVE Numbering Authorities (CNAs)…are essential to the CVE Program's success and every CVE Record is added to the CVE List by a CNA."**

**What §7 may say:** the mission sentence and the CNA sentence above, attributed to the CVE Program. Plus, from A2, the Kubernetes docs' own use of CVE identifiers in context (`CVE-2022-0185`, `CVE-2019-5736`), which demonstrates the form without defining it.
**What §7 may not say:** a definition of "vulnerability", the CVE ID format (`CVE-YYYY-NNNNN`), or any claim about severity scoring / CVSS. None of these is sourced.
**Recommended fix if the author wants it closed:** a manual fetch of `https://www.cve.org/About/Overview` in a browser and a hand-pasted snapshot. It is a five-minute job and it is the only fetch in this chapter that automation cannot do.

### G-B · No one-sentence definition of an SBOM — **partial, affects one §7 sentence**

Detailed in A14's caveat. SPDX and CycloneDX give standard-level statements; no source in the corpus states what an SBOM *is*. CISA and NTIA both returned HTTP 403; the CNCF glossary has no entry (index verified). Draft around it as A14 specifies.

### G-C · The file-over-env-var argument's second half is not sourced — **touches a pinned cross-bearing**

Detailed in A16's closing note. `chapter-11:444` is section-pinned at Ch 12 §4 and promised the reader the other half of an argument. The half kubernetes.io actually supplies is *update propagation* plus *per-container scoping*, not *env vars leak*. **Author's attention requested**: §4 can honour the promise with the sourced half, but it is a different argument from the one the outline's phrasing implies. If the author wants the leak argument, it needs a source this run did not find.

### G-D · Why RBAC names subjects rather than selecting them — **not sourced; §3 owes an explanation**

`chapter-04:839` promised the reader an *explanation*, and warned they would otherwise "make a specific, confident, wrong prediction in Chapter 12." A7 confirms the docs state subjects are named strings (users, groups, ServiceAccounts, with `system:` reserved). **No source states why.** The reasoning the outline sketches — that a selector is a query evaluated continuously against a changing set, and a grant that silently expands is not auditable — is sound and is the author's, exactly as §9's argument is. It must carry the same uncertainty signal, not be presented in the same register as the sourced material around it.

### G-E · §9's design rationale — **CONFIRMED unsourceable**

Searched again this run across the RBAC reference, RBAC good practices, the authorization reference and the NetworkPolicy pages already in the corpus. Every source states the additive property; none explains it. **§9's note in the outline stands unmodified.** The book is committed to an explanation by `chapter-11:1638`; it must be delivered as the author's reading, in the Simple Version / Full Picture uncertainty form.

### G-F · Orphaned identity after workload deletion — **not directly stated**

`chapter-06:486` is owed at §2: a deleted Deployment leaves behind its ServiceAccount, its Secrets and its RoleBindings. Nothing in the corpus states this in those words. It follows from owner-reference semantics (`k8s-docs-garbage-collection-2026-08-24.md` — nothing sets an owner reference from a Deployment to a ServiceAccount) and is adjacent to A6's *Periodic review* ("It is vital to periodically review the Kubernetes RBAC settings for redundant entries and possible privilege escalations"). **Draft it as `[inferred]`**, or as a derivation from garbage collection with the pointer back to Ch 6.

### G-G · Cosign's tag-to-digest behaviour — **substituted, not missing**

`docs.sigstore.dev/cosign/signing/signing_with_containers/` and `.../verifying/verify/` were both fetched; neither states that cosign resolves a tag to a digest, warns about tag mutability, or describes signature storage relative to the digest. The equivalent statement was found in the **Notary Project** docs instead (A10) and is strong. §7's Fixed Point is sourced — just attribute it to Notary, not to Sigstore.

### G-H · PodSecurityPolicy removal — **implied, not stated**

A3 records that the PSA concept page only *points at* a migration guide; it does not contain a sentence saying PodSecurityPolicy was removed. The B1 inventory carries this as a `[source]` trap. Either locate the removal statement (it lives in the v1.25 release notes / the `migrate-from-psp` task page, neither fetched this run) or downgrade the tag. **Recommend: fetch `kubernetes.io/docs/tasks/configure-pod-container/migrate-from-psp/` at drafting time, or soften to "superseded by Pod Security Admission" which A4's Policy Instantiation section supports.**

---

## Notes for the author

**1. One fact-check that changes a planned Bearings question.** A7 records the `edit` role's full description: *"this role allows accessing Secrets and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace."* Checkpoint #1 question 5 is planned as "what `view` and `edit` each cannot do" (B1 #57, #58). Both traps survive as written — `view` cannot read Secrets, `edit` cannot manage RBAC — but the drafting stage must not slide into "`edit` cannot read Secrets," which is false and which the docs contradict in one sentence. Worth an explicit warning in the draft prompt.

**2. §5 has gone from the worst-sourced section to the best.** A1 and A2 between them give the field surface, Pod-versus-container precedence in the docs' own words (*"they override settings made at the Pod level when there is overlap"*), the capabilities naming rule (`CAP_` is omitted in manifests — a nice concrete exam-shaped detail), and a *far* better ⚠ Navigational Hazard than the outline anticipated. The outline plans to quote the PSS definition of the `privileged` level; A2 gives something stronger and more specific:

> "Privileged containers override or undo many other hardening settings such as the applied seccomp profile, AppArmor profile, or SELinux constraints. Privileged containers are given all Linux capabilities, including capabilities that they don't require."

plus the three-line override table (seccomp → `Unconfined`, AppArmor → ignored, SELinux → `unconfined_t`). That is the *apparatus* `chapter-11:440` promised, shown failing all at once. **Recommend §5 use A2's framing for the Hazard and keep the PSS quote for §6.** Open question #10 (whether §5 should be 🟡) can now be answered: **keep 🔵.** The material is well-bounded and well-sourced; nothing about it is Advanced-tier.

**3. `ch12-fig04` is now buildable as specified.** A4 gives every Restricted control paired with its exact field path and allowed values, which is precisely the levels-against-fields grid the outline asked for. The natural row set for the figure — the one that also does double duty for §5 — is `privileged`, `capabilities.add` / `capabilities.drop`, `hostPath`, `allowPrivilegeEscalation`, `runAsNonRoot`, `seccompProfile.type`. Six rows, three columns, inside Part 18.12's label cap.

**4. B1 trap #61 upgrades from reasoning to quotation.** The outline's most consequential practical fact — anyone able to create a Pod in a namespace can read every Secret in it — is now available verbatim from kubernetes.io (A6, *Workload creation*), including the "either Pods, or workload resources that manage Pods" clause that covers the Deployment path. This is a genuine strengthening: §4's ⚠ Navigational Hazard and Checkpoint #2's designated challenge item can both quote the primary source rather than reason toward it.

**5. A6 also hands §6 an unplanned payoff.** Its *Namespace modification* subsection states that a user with `patch` on a Namespace can change its labels, and that "In clusters where Pod Security Admission is used, this may allow a user to configure the namespace for a more permissive policy than intended by the administrators. For clusters where NetworkPolicy is used, users may be set labels that indirectly allow access to services that an administrator did not intend to allow." That is **one sourced sentence that ties §3, §6 and Ch 10 together** — RBAC, PSA's label control surface, and NetworkPolicy's label selectors, all failing through the same hole. It is a strong candidate for an interleaved Practice Question and arguably belongs in §9's evidence. Not in the outline; offered.

**6. The 4Cs decision (Open question #1) is now a clean editorial choice.** A9 makes option (a) fully sourceable from the Kubernetes project's own archived documentation, including the load-bearing sentence *"You cannot safeguard against poor security standards in the base layers by addressing security at the Code level"* — which is the best one-line justification for the *where* map that exists anywhere in the corpus, and pairs well against the phases' *when*. The snapshot carries a prominent version-status banner so no downstream stage mistakes it for current guidance. **The research obstacle is gone; the call is still the author's.**

**7. Two sources fought the retrieval tooling and one is worth knowing about.** `cve.org` and `nvd.nist.gov` are client-rendered and yield nothing to automated fetch; `cisa.gov` and `spdx.dev/learn/faq/` returned 403/404. Where kubernetes.io's rendered pages truncated or the summarizer balked, the CC BY 4.0 markdown sources in `github.com/kubernetes/website` were used instead and gave clean transcription — that path is worth reaching for first on any future kubernetes.io fetch, and it is how A1, A2, A5, A6, A7 and A9 were obtained.

**8. Fidelity convention used in these snapshots.** Passages inside quotation marks are the source's own words, character-for-character. Anything without quotation marks is condensed and is explicitly flagged with a `FIDELITY NOTE` in the three files where condensation occurs (A7's closing paragraphs, A8's two paragraphs, A15's second and third sections). Nothing else in this delivery is paraphrased. Downstream audits should treat the flagged spans as leads, not as citable evidence.