---
source_url: "https://kubernetes.io/docs/concepts/workloads/pods/probes/"
source_raw: "https://raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/workloads/pods/probes.md"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0. Fetched from the kubernetes/website source markdown; the probes material formerly lived on the Pod Lifecycle page and now has its own page."
objectives_covered: ["D1.1"]
concepts_covered: ["probe", "probe-exec", "probe-httpget", "probe-tcpsocket", "probe-grpc", "liveness-probe", "readiness-probe", "startup-probe", "probe-mechanism-orthogonality"]
closes_gap: "Ch 5 §7 AUTHOR-REVIEW: (a) the gRPC success criterion, which the 2026-08-23 pod-lifecycle snapshot did not give; (b) the orthogonality of probe type and check mechanism, which Practice Q17 rests on and which no cached snapshot asserted."
---

# Liveness, Readiness, and Startup Probes

> All passages below are **[VERBATIM]** from the kubernetes/website source markdown. Where the transcription omitted text between two quoted sentences, the gap is marked `[…]`.

## What a probe is

> "Kubernetes lets you define _probes_ to continuously monitor the health of containers in a Pod. A probe is a diagnostic performed periodically by the kubelet on a container."

## Check mechanisms

> "Each probe must define exactly one of these four mechanisms"

- `exec` — > "The diagnostic is considered successful if the command exits with a status code of 0."
- `grpc` — > "The diagnostic is considered successful if the `status` of the response is `SERVING`."
- `httpGet` — > "The diagnostic is considered successful if the response has a status code greater than or equal to 200 and less than 400."
- `tcpSocket` — > "The diagnostic is considered successful if the port is open."

## Types of probe

> "Startup probes verify whether the application within a container is started. If a startup probe is configured, Kubernetes does not execute liveness or readiness probes until the startup probe succeeds, allowing the application time to finish its initialization."

> "Liveness probes determine when to restart a container […] If a container fails its liveness probe more times than the configured tolerance, the kubelet restarts that container."

> "Readiness probes determine when a container is ready to accept traffic […] If the readiness probe returns a failed state, the EndpointSlice controller removes the Pod's IP address from the EndpointSlices."

## Notes for the author

- The orthogonality claim the chapter makes ("any probe type can use any mechanism") rests on the sentence "Each probe must define exactly one of these four mechanisms": the rule is stated for every probe, independent of its type.
- The current page names the **EndpointSlice controller** where the 2026-08-23 pod-lifecycle snapshot said "the endpoints controller … the endpoints of all Services that match the Pod." The two describe the same removal; Ch 9 §4 reconciles the controller's two names.
