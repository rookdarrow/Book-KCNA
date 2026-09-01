---
source_url: "https://kubernetes.io/docs/reference/kubectl/generated/kubectl_events/"
fetched_at: "2026-08-31T21:15:00-0400"
authority: "Kubernetes — official kubectl command reference"
objectives_covered: ["2.3"]
concepts_covered: ["kubectl-events", "kubectl-get", "kubectl-describe"]
closes_gap: "B1 gap G1 residual. k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md records 'kubectl events is NOT covered'. Now covered."
---

# kubectl events — Kubernetes command reference

## Synopsis — verbatim

"List events"

"Display events."

"Prints a table of the most important information about events. You can request events for a namespace, for all namespace, or filtered to only those pertaining to a specified resource."

```
kubectl events [(-o|--output=)json|yaml|kyaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file] [--for TYPE/NAME] [--watch] [--types=Normal,Warning]
```

## Examples — verbatim

```bash
# List recent events in the default namespace
kubectl events

# List recent events in all namespaces
kubectl events --all-namespaces

# List recent events for the specified pod, then wait for more events and list them as they arrive
kubectl events --for pod/web-pod-13je7 --watch

# List recent events in YAML format
kubectl events -oyaml

# List recent only events of type 'Warning' or 'Normal'
kubectl events --types=Warning,Normal
```

## Flags — verbatim descriptions

- `-A, --all-namespaces` — "If present, list the requested object(s) across all namespaces. Namespace in current context is ignored even if specified with --namespace."
- `--allow-missing-template-keys` (default true) — "If true, ignore any errors in templates when a field or map key is missing in the template. Only applies to golang and jsonpath output formats."
- `--chunk-size int` (default 500) — "Return large lists in chunks rather than all at once. Pass 0 to disable."
- `--for string` — "Filter events to only those pertaining to the specified resource."
- `-h, --help` — "help for events"
- `--no-headers` — "When using the default output format, don't print headers."
- `-o, --output string` — "Output format. One of: (json, yaml, kyaml, name, go-template, go-template-file, template, templatefile, jsonpath, jsonpath-as-json, jsonpath-file)."
- `--show-managed-fields` — "If true, keep the managedFields when printing objects in JSON or YAML format."
- `--template string` — "Template string or path to template file to use when -o=go-template, -o=go-template-file."
- `--types strings` — "Output only events of given types."
- `-w, --watch` — "After listing the requested events, watch for more events."

## Relationship to `kubectl get events` — NOT STATED ON PAGE

The reference page does not state how `kubectl events` relates to or differs from
`kubectl get events`. Confirmed absent 2026-08-31.

USABLE FOR A STEM: the `--for TYPE/NAME` filter and the `--types` filter are
documented and exact. A distractor turning on the CLAIM that `kubectl events`
sorts by timestamp by default, or that it replaces/deprecates `kubectl get
events`, is NOT sourced and must not be built.
