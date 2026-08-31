---
source_url: "https://www.fluentd.org/architecture"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Fluentd project (CNCF graduated)"
objectives_covered: ["D4.1", "D2.3"]
concepts_covered: ["fluentd", "unified-logging-layer", "plugins", "log-collection", "cncf-graduated"]
---
# Fluentd — Architecture

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

The corpus had Fluent Bit but not Fluentd. Ch 18 §6 introduces both and the B7 ledger flags the
surface-form asymmetry (Fluentd one word, Fluent Bit two) as itself exam-adjacent, so the parent
project needed its own snapshot.

## Unified logging layer

> "Fluentd tries to structure data as JSON as much as possible: this allows Fluentd to unify all
> facets of processing log data"

## Sources and outputs

> Fluentd "connects dozens of data sources and data outputs"

## Plugin system

> "Fluentd has a flexible plugin system that allows the community to extend its functionality."

> "Our 500+ community-contributed plugins"

## Footprint

> "The vanilla instance runs on 30-40MB of memory and can process 13,000 events/second/core"

## CNCF status

> "Fluentd was accepted to Cloud Native Computing Foundation on November 8, 2016 and is at the
> Graduated project maturity level on 2019"

## ⚠ TWO GUARDRAILS ON THAT LAST QUOTE

1. **Do not print it as a quote.** The sentence is verbatim and it is what fluentd.org says, but the
   grammar is broken ("is at the Graduated project maturity level on 2019"). State the graduation as
   fact in the book's own voice and cite this snapshot.
2. **Trap #99 applies.** This snapshot names a current maturity level. Per B3 and the outline's
   §7 Practice constraint, **no item may be graded on a project's current CNCF maturity level.** The
   status may support prose. It may not support a question.

## Drafting note for §6

The already-cached `fluent-bit-overview-2026-08-23.md` states the relationship from the child's
side — Fluent Bit created 2014, a sub-project of Fluentd, both commonly deployed as node-level
DaemonSets. Between the two snapshots §6 has the full picture without needing a third fetch. The
footprint numbers are the sourced reason a *lightweight* agent exists at all, which is the honest
answer to "why are there two of these" — but they are detail, not surface. One clause at most.
