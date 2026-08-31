---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/diffing/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["synced-outofsync", "drift-detection"]
---
# Argo CD — Diffing Customization

"It is possible for an application to be `OutOfSync` even immediately after a successful Sync operation."

CAPTURE NOTE: this snapshot deliberately carries a single sentence. The remainder of
the page enumerates causes (unknown fields in manifests, pruning disabled, mutating
controllers and webhooks, Helm template functions generating differing data, HPA
metric reordering) but the fetch returned those as summary rather than quotation, so
they are not reproduced here. Do not attribute any specific cause to this snapshot.
