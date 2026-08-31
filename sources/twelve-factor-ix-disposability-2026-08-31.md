---
source_url: "https://12factor.net/disposability"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-ix-disposability"]
---
# The Twelve-Factor App — IX. Disposability

"The twelve-factor app's processes are disposable, meaning they can be started or stopped at a moment's notice."

"Processes should strive to minimize startup time. Ideally, a process takes a few seconds from the time the launch command is executed until the process is up and ready to receive requests or jobs."

"Processes shut down gracefully when they receive a SIGTERM signal from the process manager."

"Processes should also be robust against sudden death, in the case of a failure in the underlying hardware."
