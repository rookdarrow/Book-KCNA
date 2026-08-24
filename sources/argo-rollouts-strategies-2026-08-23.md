---
source_url: "https://argo-rollouts.readthedocs.io/en/stable/concepts/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Argo project (CNCF graduated)"
objectives_covered: ["D3 Application Delivery"]
concepts_covered: ["rolling-update", "recreate", "blue-green", "canary", "progressive-delivery"]
---
# Deployment strategies (argo-rollouts.readthedocs.io/en/stable/concepts/)

Progressive delivery is the process of releasing updates of a product in a controlled and gradual manner, thereby reducing the risk of the release, typically coupling automation and metric analysis to drive the automated promotion or rollback of the update.

- **Rolling Update** — a RollingUpdate slowly replaces the old version with the new version. As the new version comes up, the old version is scaled down in order to maintain the overall count of the application. This is the default strategy of the Deployment object.
- **Recreate** — a Recreate deployment deletes the old version of the application before bringing up the new version. As a result, this ensures that two versions of the application never run at the same time, but there is downtime during the deployment.
- **Blue-Green** — a Blue-Green deployment (sometimes referred to as a Red-Black) has both the new and old version of the application deployed at the same time. During this time, only the old version of the application will receive production traffic. This allows the developers to run tests against the new version before switching the live traffic to the new version.
- **Canary** — a Canary deployment exposes a subset of users to the new version of the application while serving the rest of the traffic to the old version. Once the new version is verified to be correct, the new version can gradually replace the old version. Canary strategies offer greater flexibility but demand more infrastructure (traffic-splitting via a service mesh or ingress controller) and metric analysis; Blue/Green needs no traffic provider and suits workloads such as queue workers.
