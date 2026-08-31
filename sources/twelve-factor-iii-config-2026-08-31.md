---
source_url: "https://12factor.net/config"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-iii-config-in-environment"]
---
# The Twelve-Factor App — III. Config

"An app's config is everything that is likely to vary between deploys (staging, production, developer environments, etc)."

"A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials."

On config files: "This is a huge improvement over using constants which are checked into the code repo, but still has weaknesses: it's easy to mistakenly check in a config file to the repo."

"The twelve-factor app stores config in environment variables (often shortened to env vars or env). Env vars are easy to change between deploys without changing any code; unlike config files, there is little chance of them being checked into the code repo accidentally."

On grouping into named environments: "This method does not scale cleanly: as more deploys of the app are created, new environment names are necessary, such as staging or qa."

"In a twelve-factor app, env vars are granular controls, each fully orthogonal to other env vars. They are never grouped together as 'environments', but instead are independently managed for each deploy."
