---
source_url: "https://argo-rollouts.readthedocs.io/en/stable/features/canary/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo Rollouts; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["canary-deployment", "progressive-delivery", "deployment-strategy-vocabulary"]
---
# Argo Rollouts — Canary Deployment Strategy

"A canary rollout is a deployment strategy where the operator releases a new version of their application to a small percentage of the production traffic."

On traffic management: "The traffic management rules to apply to control the flow of traffic between the active and canary versions. If not set, the default weighted pod replica based routing will be used."

On header-based shaping: "You wish to scale the canary stack up minimally, and use some header based traffic shaping to the canary, while setWeight is still set to 0."

CAPTURE NOTE: the string "A/B" does not appear on this page. Verified 2026-08-31.
