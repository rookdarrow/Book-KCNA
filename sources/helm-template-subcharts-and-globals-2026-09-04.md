---
source_url: "https://helm.sh/docs/chart_template_guide/subcharts_and_globals/"
fetched_at: "2026-09-04T17:20:00-0400"
authority: "Helm project (CNCF graduated project), Chart Template Developer's Guide; retrieved from the helm/helm-www source of record, docs/chart_template_guide/subcharts_and_globals.md on branch main, because helm.sh was unreachable from the fetch layer"
objectives_covered: ["D3.1"]
concepts_covered: ["subchart", "chart-dependencies-directory"]
---

# Helm — Chart Template Guide: Subcharts and Global Values (helm.sh/docs/chart_template_guide/subcharts_and_globals/)

> **Snapshot note.** Fetched 2026-09-04 to source the term "subchart", which Chapter 14 §2
> defines and the Term Ownership Ledger assigns to Ch 14 §2, and which no earlier snapshot
> defines in body text. Scope: the opening definition and the three stand-alone rules. Not
> transcribed: the `mysubchart` walkthrough and the global-values examples.

## Opening

"To this point we have been working only with one chart. But charts can have dependencies,
called _subcharts_, that also have their own values and templates."

"1. A subchart is considered "stand-alone", which means a subchart can never explicitly
depend on its parent chart.
2. For that reason, a subchart cannot access the values of its parent."

"Because every subchart is a _stand-alone chart_, we can test `mysubchart` on its own"
