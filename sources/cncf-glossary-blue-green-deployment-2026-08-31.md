---
source_url: "https://glossary.cncf.io/blue-green-deployment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["blue-green-deployment", "deployment-strategy-vocabulary"]
---
# CNCF Glossary — Blue Green Deployment

## What it is
"Blue-green deployment is a strategy for updating running computer systems with minimal downtime. The operator maintains two environments, dubbed 'blue' and 'green'."

One environment serves live production traffic while the other is updated; after testing on the inactive environment, traffic switches via load balancer. The entry notes this typically affects entire systems with multiple services simultaneously, and that the term is sometimes misapplied to individual services.

## Problem it addresses
"Blue-green deployments allow minimal downtime when updating software that must be changed in 'lockstep' owing to a lack of backwards compatibility."

## How it helps
"Blue-green deployment is an appropriate strategy for non-cloud native software that needs to be updated with minimal downtime. However, its use is normally a 'smell' that legacy software needs to be re-engineered so that components can be updated individually."
