---
source_url: "https://kubernetes.io/blog/2023/08/29/gateway-api-v0-8/"
fetched_at: "2026-08-24T14:42:00-0400"
authority: "Kubernetes project (official kubernetes.io blog), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["north-south-traffic", "east-west-traffic", "gateway-api"]
---
# "Gateway API v0.8.0: Introducing Service Mesh Support" — kubernetes.io blog

Title: Gateway API v0.8.0: Introducing Service Mesh Support
Authors: Flynn (Buoyant), John Howard (Google), Keith Mattix (Microsoft), Michael Beaumont (Kong), Mike Morris (independent), Rob Scott (Google)
Published: Tuesday, August 29, 2023

(Fetched to resolve Ch 10 §1's SOURCE NOTE, which recorded that "north-south" and "east-west" appear
nowhere in the cached set and would have to be introduced as unsourced industry vocabulary. They are
in fact used on the official Kubernetes blog, and used in exactly the pairing §1 wants: ingress with
north-south, service mesh with east-west. This is a blog post, not the documentation — it is
authoritative as a Kubernetes-project publication but is NOT normative reference documentation. See
the manifest's Notes for the author, item 6.)

## Relevant passage

"While the initial focus of Gateway API was always ingress (north-south) traffic, it was clear almost from the beginning that the same basic routing concepts should also be applicable to service mesh (east-west) traffic."

"In 2022, the Gateway API subproject started the GAMMA initiative, a dedicated vendor-neutral workstream, specifically to examine how best to fit service mesh support into the framework of the Gateway API resources, without requiring users of Gateway API to relearn everything they understand about the API."
