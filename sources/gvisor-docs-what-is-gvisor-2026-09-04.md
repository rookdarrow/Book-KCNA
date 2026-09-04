---
source_url: "https://gvisor.dev/docs/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "gVisor project documentation (gvisor.dev), 'What is gVisor?' and architecture overview — the project's own description of its mechanism"
objectives_covered: ["D1.4"]
concepts_covered: ["sandboxed-runtime", "gvisor", "runtimeclass", "user-space-kernel"]
---

# gVisor documentation — what gVisor is and how it isolates

Verbatim passages:

"gVisor provides a strong layer of isolation between running applications and the host operating system. It is an application kernel that implements a Linux-like interface."

gVisor "runs in userspace" and is "written in a memory-safe language (Go)."

"gVisor intercepts application system calls and acts as the guest kernel, without the need for translation through virtualized hardware."

On the Sentry (the kernel component): "When the application makes a system call, the Platform redirects the call to the Sentry, which will do the necessary work to service it." "The Sentry does not pass system calls through to the host kernel."

On the difference from virtual machines: rather than exposing virtualized hardware through a Virtual Machine Monitor, gVisor operates as "either a merged guest kernel and VMM, or as seccomp on steroids."

On the difference from ordinary containers: gVisor is "not a syscall filter (e.g. seccomp-bpf), nor a wrapper over Linux isolation primitives." It keeps the "lower resource footprint, fast startup, and flexibility of regular userspace applications" while providing "many security benefits of VMs."

What this supports in the book: Ch 2 §7's Closer Look on how a user-space kernel (gVisor) differs from hardware virtualization (Kata Containers): the workload's system calls are serviced by the Sentry, an application kernel running as an ordinary user-space process, and are not passed through to the host kernel. Depth beyond the exam; use in a Closer Look only.
