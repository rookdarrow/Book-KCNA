---
source_url: "https://sre.google/sre-book/embracing-risk/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Google Site Reliability Engineering book, ch. 3 'Embracing Risk' (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4.1"]
concepts_covered: ["error-budget", "reliability-vs-velocity", "slo"]
---
# Error budgets (Site Reliability Engineering, ch. 3)

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

Closes Stage 1 Open Question #1, row 5 (non-blocking). The outline's fallback was to keep error
budgets as one glossed clause after SLO. That remains the right call — this snapshot makes it a
*sourced* clause.

## The tension the budget resolves

> "Product development performance is largely evaluated on product velocity, which creates an
> incentive to push new code as quickly as possible. Meanwhile, SRE performance is evaluated based
> upon reliability of a service, which implies an incentive to push back against a high rate of
> change."

## What the budget permits

> "As long as the uptime measured is above the SLO—in other words, as long as there is error budget
> remaining—new releases can be pushed."

## Spending it

> "If a problem causes us to fail 0.0002% of the expected queries for the quarter, the problem
> spends 20% of the service's quarterly error budget."

## ⚠ ONE QUOTE WITH AN UNCAPTURED ANTECEDENT — do not paraphrase

> "The difference between these two numbers is the 'budget' of how much 'unreliability' is remaining
> for the quarter."

**"These two numbers" was not captured.** Do not write out what they refer to, and do not
reconstruct the arithmetic from memory. If §7 wants the budget-as-a-difference framing, re-fetch the
page first. Everything §7 actually needs is in the three quotes above, none of which has this
problem — in particular, **"as long as there is error budget remaining—new releases can be pushed"**
is self-contained and is the whole idea in one clause.

## Drafting note for §7

The velocity/reliability quote is the sourced answer to *why* an error budget exists, and it is the
only sentence in this chapter's whole corpus that connects observability back to how organisations
actually behave. That makes it a strong candidate for §7's one-clause treatment — better than
defining the budget mechanically, because the mechanism is exactly the part that is not KCNA
surface.

**Keep it ungraded.** B1 lists no trap for error budgets and the outline routes no item to them.
