---
source_url: "https://sre.google/sre-book/monitoring-distributed-systems/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Google Site Reliability Engineering book (O'Reilly, CC BY-NC-ND)"
objectives_covered: ["D4 Observability"]
concepts_covered: ["golden-signals", "latency", "traffic", "errors", "saturation"]
---
# The Four Golden Signals (Site Reliability Engineering, ch. 6 "Monitoring Distributed Systems")

The four golden signals of monitoring are latency, traffic, errors, and saturation. If you can only measure four metrics of your user-facing system, focus on these four.

- **Latency** — The time it takes to service a request. It's important to distinguish between the latency of successful requests and the latency of failed requests. For example, an HTTP 500 error triggered due to loss of connection to a database or other critical backend might be served very quickly; however, as an HTTP 500 error indicates a failed request, factoring 500s into your overall latency might result in misleading calculations. On the other hand, a slow error is even worse than a fast error! Therefore, it's important to track error latency, as opposed to just filtering out errors.
- **Traffic** — A measure of how much demand is being placed on your system, measured in a high-level system-specific metric. For a web service, this measurement is usually HTTP requests per second, perhaps broken out by the nature of the requests (e.g., static versus dynamic content). For an audio streaming system, this measurement might focus on network I/O rate or concurrent sessions. For a key-value storage system, this measurement might be transactions and retrievals per second.
- **Errors** — The rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, "If you committed to one-second response times, any request over one second is an error").
- **Saturation** — How "full" your service is. A measure of your system fraction, emphasizing the resources that are most constrained (e.g., in a memory-constrained system, show memory; in an I/O-constrained system, show I/O). Note that many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential. Latency increases are often a leading indicator of saturation.
