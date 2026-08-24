---
source_url: "https://falco.org/docs/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Falco project (CNCF graduated)"
objectives_covered: ["D2 Security", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["falco", "runtime-security", "kernel-events", "rules", "alerts"]
---
# Falco (falco.org/docs/)

Falco is a cloud native security tool that provides runtime security across hosts, containers, Kubernetes, and cloud environments. It is designed to detect and alert on abnormal behavior and potential security threats in real-time. Falco is a graduate Cloud Native Computing Foundation (CNCF) project; it was originally created by Sysdig and is now maintained by the open-source community. How it works: Falco observes Linux kernel events (system calls) and data from plugins, enriches them with metadata from the container runtime and Kubernetes, evaluates the event stream against a rules engine, and emits real-time alerts when rules detect violations. Typical default-rule detections include privilege escalation via privileged containers, namespace manipulation, unauthorized modifications to sensitive directories such as /etc or /usr/bin, suspicious network connections, shell or SSH binary execution inside containers, unauthorized file ownership or permission changes, and symlink creation.
