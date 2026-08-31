---
source_url: "https://12factor.net/processes"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-vi-stateless-processes"]
---
# The Twelve-Factor App — VI. Processes

"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database."

"Sticky sessions are a violation of twelve-factor and should never be used or relied upon. Session state data is a good candidate for a datastore that offers time-expiration, such as Memcached or Redis."
