---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/"
fetched_at: "2026-08-31T09:32:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0"
objectives_covered: ["D3.2"]
concepts_covered: ["termination-message", "config-errors-visible-at-init", "init-container-debugging"]
transcription: "near-verbatim"
transcription_note: "Prose marked `> \"...\"` is exact. The numbered walk-through steps are lightly condensed connective text — do not cite those. All field names, defaults and numeric limits below were carried through unchanged and are safe to cite."
---
# Determine the Reason for Pod Failure

> "This page shows how to write and read a Container termination message."

> "Termination messages provide a way for containers to write information about fatal events to a location where it can be easily retrieved and surfaced by tools like dashboards and monitoring software. In most cases, information that you put in a termination message should also be written to the general Kubernetes logs."

## Writing and reading a termination message

In this exercise you create a Pod that runs one container, whose manifest specifies a command that runs when the container starts. The container sleeps for 10 seconds and then writes "Sleep expired" to the `/dev/termination-log` file, after which it terminates.
