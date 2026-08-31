---
source_url: "https://glossary.cncf.io/immutable-infrastructure/"
fetched_at: "2026-08-31T09:42:00-0400"
authority: "Cloud Native Computing Foundation — Cloud Native Glossary (CC BY 4.0)"
objectives_covered: ["D4.2"]
concepts_covered: ["immutable-infrastructure", "declarative-api-as-a-characteristic"]
---
# CNCF Cloud Native Glossary — Immutable Infrastructure

Tags: Infrastructure, Property

Definition, verbatim:

> "Immutable Infrastructure refers to computer infrastructure (virtual machines,
> containers, network appliances) that cannot be changed once deployed."

[Paraphrase, NOT verbatim: the entry states this enforcement occurs either
through automated processes that overwrite unauthorized modifications, or through
systems that prevent changes altogether. Containers exemplify the concept —
persistent alterations require creating new container versions or recreating from
images.]

## Security and operational benefits

Verbatim:

> "Operating such a system becomes a lot more straightforward because
> administrators can make assumptions about it."

[Paraphrase, NOT verbatim: by blocking or detecting unauthorized modifications,
immutable systems help organizations identify and address security
vulnerabilities more effectively.]

## Integration with infrastructure as code

Verbatim:

> "This combination of immutability and version control means that there is a
> durable audit log of every authorized change to a system."

[Paraphrase, NOT verbatim: the approach complements infrastructure-as-code
practices, where automation scripts reside in version control systems like Git.]

---
DRAFTING NOTE (not from source): this entry's "cannot be changed once deployed"
is infrastructure immutability. It is a DIFFERENT immutability from the image
immutability Ch 2 §2 owns. B7's canonical-forms ruling requires the full two-word
phrase "immutable infrastructure" and a back-bearing to Ch 2 §2 rather than a
re-derivation.
