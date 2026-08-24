---
source_url: "https://12factor.net/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "The Twelve-Factor App (Heroku / Adam Wiggins; maintained by the community)"
objectives_covered: ["D4 Cloud Native Ecosystem and Principles", "D3 Application Delivery"]
concepts_covered: ["twelve-factor", "stateless-processes", "config-in-environment", "logs-as-event-streams", "disposability"]
---
# The Twelve-Factor App (12factor.net)

In the modern era, software is commonly delivered as a service: called web apps, or software-as-a-service. The twelve-factor app is a methodology for building software-as-a-service apps that: use declarative formats for setup automation; have a clean contract with the underlying operating system, offering maximum portability between execution environments; are suitable for deployment on modern cloud platforms; minimize divergence between development and production, enabling continuous deployment for maximum agility; and can scale up without significant changes to tooling, architecture, or development practices. The twelve-factor methodology can be applied to apps written in any programming language, and which use any combination of backing services.

I. Codebase — One codebase tracked in revision control, many deploys
II. Dependencies — Explicitly declare and isolate dependencies
III. Config — Store config in the environment
IV. Backing services — Treat backing services as attached resources
V. Build, release, run — Strictly separate build and run stages
VI. Processes — Execute the app as one or more stateless processes
VII. Port binding — Export services via port binding
VIII. Concurrency — Scale out via the process model
IX. Disposability — Maximize robustness with fast startup and graceful shutdown
X. Dev/prod parity — Keep development, staging, and production as similar as possible
XI. Logs — Treat logs as event streams
XII. Admin processes — Run admin/management tasks as one-off processes
