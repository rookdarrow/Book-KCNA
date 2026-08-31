---
source_url: "https://glossary.cncf.io/serverless/"
fetched_at: "2026-08-31T09:42:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["serverless", "scale-to-zero"]
---
# CNCF Cloud Native Glossary — Serverless

The vendor-neutral definition of serverless, which the cached
`knative-overview-2026-08-23.md` does not supply. Delivered as direct quotations;
the upstream fetch declined full-body reproduction.

## Definition — verbatim quotations

> "Serverless Computing abstracts servers away from the user."

> "Charges are based on a pay-per-use model."

> "Scaling and resource provisioning for computing, storage, or networking are
> automatically adjusted based on application demand without user intervention."

> "A serverless platform provider consolidates resources to serve multiple users
> on a single physical machine, ensuring isolation through virtualization."

## Problem it addresses — verbatim quotations

> "Users commit to a predefined capacity, resulting in charges for continuous
> server availability regardless of actual use."

> "Responsibility for adjusting server capacity to meet fluctuating demands falls
> on the user, maintaining active infrastructure even during idle periods."

## How it helps — verbatim quotations

> "Serverless architecture introduces a more efficient approach, activating
> services solely upon demand."

> "Serverless technology relieves developers of the burdens of scaling
> applications and managing server infrastructure."

> "Tasks such as operating system maintenance, security updates, load balancing,
> capacity planning, and monitoring are delegated to the cloud provider."

---
DRAFTING NOTE (not from source): "abstracts servers away from the USER" — not
"eliminates servers". Combined with `knative-overview-2026-08-23.md`'s statement
that Knative "builds on the Kubernetes Pod abstraction" and that Serving and
Eventing "are implemented as Kubernetes Custom Resource Definitions (CRDs)", this
is the full sourced refutation of trap #84. Note that trap #84 remains
`[inferred]` as a FREQUENCY claim; the factual half is now `[source]`-backed
twice over.
