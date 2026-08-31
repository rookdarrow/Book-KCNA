---
source_url: "https://glossary.cncf.io/canary-deployment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Cloud Native Computing Foundation (CNCF Cloud Native Glossary)"
objectives_covered: ["D3.1"]
concepts_covered: ["canary-deployment", "deployment-strategy-vocabulary", "progressive-delivery"]
---
# CNCF Glossary — Canary Deployment

## What it is
"Canary deployments is a deployment strategy that starts with two environments: one with live traffic and the other containing the updated code without live traffic. The traffic is gradually moved from the original version of the application to the updated version."

## Problem it addresses
"No matter how thorough the testing strategy, there are always some bugs discovered in production. Shifting 100% of traffic from one version of an app to another can lead to more impactful failures."

## How it helps
"Canary deployments allow organizations to see how new software behaves in real-world scenarios before moving significant traffic to the new version. This strategy enables organizations to minimize downtime and quickly rollback in case of issues with the new deployment."
