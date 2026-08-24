---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Troubleshooting", "D3 Debugging"]
concepts_covered: ["kubectl-describe", "pending", "waiting", "image-pull-failure", "validate", "endpointslices"]
---
# Debug Pods (kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

## Debugging Pods
The first step in debugging a Pod is taking a look at it. Check the current state of the Pod and recent events with `kubectl describe pods ${POD_NAME}`. Look at the state of the containers in the pod. Are they all Running? Have there been recent restarts? Continue debugging depending on the state of the pods.

**My pod stays pending.** If a Pod is stuck in Pending it means that it can not be scheduled onto a node. Generally this is because there are insufficient resources of one type or another that prevent scheduling. Look at the output of the kubectl describe command; there should be messages from the scheduler about why it can not schedule your pod. Reasons include: you don't have enough resources — you may have exhausted the supply of CPU or Memory in your cluster, in this case you need to delete Pods, adjust resource requests, or add new nodes to your cluster; you are using hostPort — when you bind a Pod to a hostPort there are a limited number of places that pod can be scheduled; in most cases hostPort is unnecessary, try using a Service object to expose your Pod.

**My pod stays waiting.** If a Pod is stuck in the Waiting state, then it has been scheduled to a worker node, but it can't run on that machine. The most common cause of Waiting pods is a failure to pull the image. Three things to check: make sure that you have the name of the image correct; have you pushed the image to the registry?; try to manually pull the image to see if the image can be pulled.

**My pod is crashing or otherwise unhealthy.** Once your pod has been scheduled, the methods described in Debug Running Pods are available for debugging (kubectl logs, kubectl logs --previous, kubectl exec, kubectl debug with ephemeral containers).

**My pod is running but not doing what I told it to do.** If your pod is not behaving as you expected, it may be that there was an error in your pod description, and that the error was silently ignored when you created the pod. Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored. Delete your pod and try creating it again with `kubectl apply --validate -f mypod.yaml`; then compare `kubectl get pods/mypod -o yaml` against the original.

## Debugging Services
Services provide load balancing across a set of pods. First, verify that there are endpoints for the service: `kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}`. Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect to be members of your service. If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready.
