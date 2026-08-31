---
source_url: "https://12factor.net/logs"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "The Twelve-Factor App (Adam Wiggins / Heroku; community maintained)"
objectives_covered: ["D3.1"]
concepts_covered: ["twelve-factor-app", "factor-xi-logs-as-event-streams"]
---
# The Twelve-Factor App — XI. Logs

"Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services."

"A twelve-factor app never concerns itself with routing or storage of its output stream."

"Each running process writes its event stream, unbuffered, to stdout."

"In staging or production deploys, each process' stream will be captured by the execution environment, collated together with all other streams from the app, and routed to one or more final destinations for viewing and long-term archival."
