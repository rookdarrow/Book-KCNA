---
source_url: "https://raw.githubusercontent.com/kubernetes/kubernetes/master/pkg/printers/internalversion/printers.go"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project source code (kubernetes/kubernetes, master branch), the human-readable table printer that kubectl uses for `kubectl get endpointslice`"
objectives_covered: ["D3.2", "D2.1"]
concepts_covered: ["kubectl-get-endpointslices", "endpointslice-table-columns", "unset-placeholder"]
closes_gap: "Ch 20 item 59 stem — the simulated `kubectl get endpointslice` output omitted the PORTS column and printed `<none>` for an empty endpoint list. No cached kubernetes.io page shows EndpointSlice table output."
---

# kubectl table printer for EndpointSlice — column order and the empty-list placeholder

Fetched 2026-09-04 to make a simulated console listing in Chapter 20 match what
kubectl actually prints. Source code is the project's own; quoted verbatim.

## Column definitions

The EndpointSlice column definitions name, in order:

"Name", "AddressType", "Ports", "Endpoints", "Age"

kubectl upper-cases these as the table header: `NAME  ADDRESSTYPE  PORTS  ENDPOINTS  AGE`.

## Row construction — verbatim

```go
func printEndpointSlice(obj *discovery.EndpointSlice, options printers.GenerateOptions) ([]metav1.TableRow, error) {
	row := metav1.TableRow{
		Object: runtime.RawExtension{Object: obj},
	}
	row.Cells = append(row.Cells, obj.Name, string(obj.AddressType), formatDiscoveryPorts(obj.Ports), formatDiscoveryEndpoints(obj.Endpoints), translateTimestampSince(obj.CreationTimestamp))
	return []metav1.TableRow{row}, nil
}
```

## Empty-list rendering — verbatim

Both the PORTS and ENDPOINTS cells are produced through `listWithMoreString`:

```go
func listWithMoreString(list []string, more bool, count, max int) string {
	ret := strings.Join(list, ",")
	if more {
		return fmt.Sprintf("%s + %d more...", ret, count-max)
	}
	if ret == "" {
		ret = "<unset>"
	}
	return ret
}
```

## What this establishes

- An EndpointSlice with no endpoints prints `<unset>` in the ENDPOINTS column, not `<none>`.
- An EndpointSlice with no ports prints `<unset>` in the PORTS column. (The EndpointSlice controller's placeholder slice for a Service whose selector matches nothing carries an empty port list.)
- More than three addresses or ports print as the first three followed by ` + N more...`.
- The PORTS column sits between ADDRESSTYPE and ENDPOINTS; a listing without it is not kubectl's.
