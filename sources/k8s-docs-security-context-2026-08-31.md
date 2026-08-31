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
