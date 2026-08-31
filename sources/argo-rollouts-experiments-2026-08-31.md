---
source_url: "https://argo-rollouts.readthedocs.io/en/stable/features/experiment/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo Rollouts; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["progressive-delivery", "canary-deployment", "deployment-strategy-vocabulary"]
---
# Argo Rollouts — Experiments (and A/B testing)

"The Experiment CRD allows users to have ephemeral runs of one or more ReplicaSets."

On A/B testing: "A user can use experiments to enable A/B/C testing by launching multiple experiments with a different version of their application for a long duration."

On use within a canary rollout: "The experiment step serves as a blocking step for the Rollout, and a Rollout will not continue until the Experiment succeeds."

On traffic: "When Traffic Routing is enabled, the Rollout Experiment step allows traffic to be shifted to experiment pods."

CAPTURE NOTE — resolves the outline's Open Question 2. A/B testing is documented
here as a use of the Experiment resource, NOT as a rollout/deployment strategy
alongside RollingUpdate, Recreate, Blue-Green and Canary. The Canary strategy page
(https://argo-rollouts.readthedocs.io/en/stable/features/canary/) was checked
directly on 2026-08-31 and does not contain the string "A/B".
