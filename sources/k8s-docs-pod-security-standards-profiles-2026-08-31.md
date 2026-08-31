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
