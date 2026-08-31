---
source_url: "https://sre.google/sre-book/service-level-objectives/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 4 'Service Level Objectives' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["sli", "slo", "sla", "reliability"]
---
# SLI, SLO, SLA — definitions (Site Reliability Engineering, ch. 4)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Stage 1 **Open Question #2**: SLA had no cached source, and the B7 ledger rules it
"not glossary-only" precisely because it will appear as a distractor — a distractor the reader
cannot look up is a badly built distractor. It can now be looked up.

## The three terms

> **SLI** — "An SLI is a service level indicator—a carefully defined quantitative measure of some
> aspect of the level of service that is provided."

> **SLO** — "An SLO is a service level objective: a target value or range of values for a service
> level that is measured by an SLI."

> **SLA** — "Finally, SLAs are service level agreements: an explicit or implicit contract with your
> users that includes consequences of meeting (or missing) the SLOs they contain."

## The discriminating test — trap #92's answer, in one sentence

> "An easy way to tell the difference between an SLO and an SLA is to ask 'what happens if the SLOs
> aren't met?': if there is no explicit consequence, then you are almost certainly looking at an
> SLO."

## Drafting note for §7

**Use the OTel primer for SLI and SLO; use this page for SLA and for the discrimination.** The
primer's definitions are the ones §7 is built on ("a good SLI measures your service from the
perspective of your users"; an SLO is "the means by which reliability is communicated to an
organization") and they carry the user-perspective framing the section needs. This page's SLI/SLO
definitions are cached alongside them for cross-checking, not to replace them — the two sources
agree in substance and differ in emphasis, and mixing the wording mid-section would muddy both.

The consequence test is the single best asset here. It gives §7 a *procedure* for the SLO/SLA
distinction rather than two definitions to hold side by side, and it converts trap #92 from a
memory item into a reasoning item. The outline gives SLA "one clause, by contrast" — this sentence
is that clause.

Note that the SLA definition contains "the SLOs they contain," which makes the dependency direction
explicit: an SLA is built out of SLOs, which are built out of SLIs. §7's stated dependency order is
correct and now sourced end to end.
