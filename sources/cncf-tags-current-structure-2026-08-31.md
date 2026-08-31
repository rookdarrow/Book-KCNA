---
source_url: "https://contribute.cncf.io/community/tags/"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Contributors site + CNCF blog)"
objectives_covered: ["D4.3"]
concepts_covered: ["cncf-tags", "cncf-toc", "kubernetes-sig"]
---
# CNCF Technical Advisory Groups — current structure, verified 2026-08-31

CONFIRMS `cncf-toc-and-tags-2026-08-23.md`. Trap #111 is live and the cached list
is correct. Note: **cncf.io/tags/ now returns HTTP 404**; the authoritative
current home is contribute.cncf.io/community/tags/.

## Source A — contribute.cncf.io/community/tags/ (verbatim)

> "Technical Advisory Groups (TAGs) are the primary organizational units within
> the CNCF that oversee and coordinate interests across projects, working groups,
> and the broader cloud native community."

> They "serve as bridges between CNCF projects, end users, and the Technical
> Oversight Committee (TOC)."

> "The current TAG structure was established in 2025 to better align with cloud
> native ecosystem needs."

### The five current TAGs, with the scopes this page states — verbatim

> "TAG Developer Experience" — "Databases, Microservices, Streaming, Messaging,
> API Management, Developer Frameworks"

> "TAG Infrastructure" — "Data, Storage, Network, DNS, Compute, Service Mesh,
> Infrastructure-as-Code, Edge, Sovereignty, Load Balancing"

> "TAG Operational Resilience" — "Observability, Management, Business Continuity,
> Resource Optimization, Cost Efficiency, Energy, Performance, Troubleshooting,
> Reliability, Day 2 Operations"

> "TAG Security and Compliance" — "Security Hygiene, Policy-as-Code, Compliance,
> Auditing, Threat Modeling, Secure Software Supply Chain"

> "TAG Workloads Foundation" — "Fundamental cloud native workload execution
> environments and lifecycle management"

## Source B — cncf.io/blog/2025/05/07/10-years-in-cloud-native-toc-restructures-technical-groups/ (verbatim)

> "In order to grow with the ecosystem, the TOC has approved a restructuring of
> the Technical Advisory Groups"

> "The TOC has been working with the existing TAGs for two years to identify
> these opportunities for improvement in the TAG structure"

On the origin of the groups — verbatim:

> "By June 2019, this number had grown to 37 projects and the TOC approved the
> creation of SIGs, later to be renamed Technical Advisory Groups."

[Paraphrase, NOT verbatim: the post frames the change against CNCF's growth from
4 projects in 2015–2016 to 223 contributed projects by 2025.]

---
DRAFTING NOTES (not from source), two of them, and both matter:

**1. Trap #111 is confirmed and dated.** Restructuring approved by the TOC,
announced 2025-05-07. The pre-2025 list (App Delivery, Contributor Strategy,
Environmental Sustainability, Network, Observability, Runtime, Security, Storage)
is in `cncf-toc-and-tags-2026-08-23.md`. Both lists are now sourced, the current
one twice.

**2. This is an unexpectedly good gift for trap #112 (TAGs vs SIGs) — and a
hazard.** The blog states that CNCF's groups were originally CALLED SIGs and were
"later renamed Technical Advisory Groups." That is the historical reason the two
are confusable, told in CNCF's own words, and it is far better teaching than a
warning. The hazard: #112 is `[inferred]` and Ethical Guardrail #8 bars framing it
as frequently tested. Naming the shared origin is a *causal explanation*, not a
frequency claim, so it stays inside the guardrail — but the sentence must not
drift into "which is why it's such a common exam trap."
