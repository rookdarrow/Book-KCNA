---
source_url: "https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/"
fetched_at: "2026-09-04T18:00:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC BY 4.0 — fetched as the raw CC BY 4.0 markdown source from kubernetes/website, main branch (content/en/docs/tasks/debug/debug-application/debug-service.md)"
objectives_covered: ["D3.2", "D2.3"]
concepts_covered: ["service-selector-mismatch", "empty-endpointslice-as-symptom", "port-versus-targetport", "service-dns-name-shape", "kubectl-get-endpointslices", "kubectl-describe-service"]
---

# Debug Services

> Supersedes `k8s-docs-debug-service-2026-08-31.md`, whose body was truncated at the page's first code fence. All passages are verbatim from the markdown source. Section headings are the page's own.

## Running commands in a Pod

"For many steps here you will want to see what a Pod running in the cluster sees. The simplest way is to run an interactive busybox Pod:"

## Does the Service work by DNS name?

"One of the most common ways that clients consume a Service is through a DNS name."

## Is the Service defined correctly?

The page prints the Service with `kubectl get service hostnames -o json` and then asks:

- "Is the Service port you are trying to access listed in `spec.ports[]`?"
- "Is the `targetPort` correct for your Pods (some Pods use a different port than the Service)?"
- "If you meant to use a numeric port, is it a number (9376) or a string "9376"?"
- "If you meant to use a named port, do your Pods expose a port with the same name?"
- "Is the port's `protocol` correct for your Pods?"

## Does the Service have any EndpointSlices?

"If you got this far, you have confirmed that your Service is correctly defined and is resolved by DNS. Now let's check that the Pods you ran are actually being selected by the Service."

"The `-l app=hostnames` argument is a label selector configured on the Service."

"Inside the Kubernetes system is a control loop which evaluates the selector of every Service and saves the results into one or more EndpointSlice objects."

```shell
kubectl get endpointslices -l kubernetes.io/service-name=hostnames

NAME              ADDRESSTYPE   PORTS   ENDPOINTS
hostnames-ytpni   IPv4          9376    10.244.0.5,10.244.0.6,10.244.0.7
```

"This confirms that the EndpointSlice controller has found the correct Pods for your Service. If the `ENDPOINTS` column is `<none>`, you should check that the `spec.selector` field of your Service actually selects for `metadata.labels` values on your Pods. A common mistake is to have a typo or other error, such as the Service selecting for `app=hostnames`, but the Deployment specifying `run=hostnames`, as in versions previous to 1.18, where the `kubectl run` command could have been also used to create a Deployment."
