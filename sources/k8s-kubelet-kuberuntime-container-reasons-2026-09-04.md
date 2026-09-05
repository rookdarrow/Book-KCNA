---
source_url: "https://github.com/kubernetes/kubernetes/blob/master/pkg/kubelet/kuberuntime/kuberuntime_container.go"
source_raw: "https://raw.githubusercontent.com/kubernetes/kubernetes/master/pkg/kubelet/kuberuntime/kuberuntime_container.go"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project source code (kubernetes/kubernetes, Apache-2.0) — the kubelet's container-runtime manager, which is the component that emits the container-state reason strings. Primary source, not documentation: kubernetes.io does not document the string CreateContainerConfigError on any page (searched 2026-09-04)."
objectives_covered: ["D2.3"]
concepts_covered: ["createcontainerconfigerror", "createcontainererror", "container-state-reason-strings", "kubelet-container-start-sequence"]
closes_gap: "ch-13 sec.2 RESEARCH GAP (highest severity): CreateContainerConfigError appears in no cached snapshot and on no kubernetes.io page. This file defines the string and shows that it is returned when the kubelet cannot assemble the container's configuration, after the image is already available and before the container is created."
---

# kubelet — the container-start reason strings, from the source

> All passages below are **[VERBATIM]** from `pkg/kubelet/kuberuntime/kuberuntime_container.go` (file header: "Copyright 2016 The Kubernetes Authors.").

## The reason strings

```
var (
	// ErrCreateContainerConfig - failed to create container config
	ErrCreateContainerConfig = errors.New("CreateContainerConfigError")
	// ErrPreCreateHook - failed to execute PreCreateHook
	ErrPreCreateHook = errors.New("PreCreateHookError")
	// ErrCreateContainer - failed to create container
	ErrCreateContainer = errors.New("CreateContainerError")
	// ErrPreStartHook - failed to execute PreStartHook
	ErrPreStartHook = errors.New("PreStartHookError")
	// ErrPostStartHook - failed to execute PostStartHook
	ErrPostStartHook = errors.New("PostStartHookError")
)
```

## Where `CreateContainerConfigError` is returned — inside `startContainer`, "Step 2: create the container."

```
	containerConfig, cleanupAction, err := m.generateContainerConfig(ctx, container, pod, restartCount, podIP, imageRef, podIPs, target, imageVolumes)
	if cleanupAction != nil {
		defer cleanupAction()
	}
	if err != nil {
		s, _ := grpcstatus.FromError(err)
		m.recordContainerEvent(ctx, pod, container, "", v1.EventTypeWarning, events.FailedToCreateContainer, "Error: %v", s.Message())
		return s.Message(), ErrCreateContainerConfig
	}
```

## What this supports

- The string `CreateContainerConfigError` is the kubelet's own name for "failed to create container config": the kubelet could not generate the container's configuration (`generateContainerConfig`), which is the step that resolves environment variables, volumes, and the ConfigMap and Secret data the Pod references.
- It is emitted *after* the image reference (`imageRef`) is already in hand — the pull step precedes this step in `startContainer` — and *before* any container is created. So it belongs to the never-started family: a container carrying this reason has not executed.
- When it happens the kubelet also records a Warning Event on the Pod (`events.FailedToCreateContainer`) carrying the underlying message, which is why `kubectl describe pod` names the missing object.
- The sibling `CreateContainerError` is a different string for a different step (the runtime failed to create the container after a valid config was assembled). This chapter does not teach it.
