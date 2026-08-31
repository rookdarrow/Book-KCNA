---
source_url: "https://grafana.com/blog/the-red-method-how-to-instrument-your-services/"
fetched_at: "2026-08-31T15:00:00-0400"
authority: "Grafana Labs, article by Tom Wilkie — the method's originator. TIER-4 CAVEAT: vendor blog, not official documentation. See guardrail below."
objectives_covered: ["D4.1"]
concepts_covered: ["red-method", "rate", "errors", "duration", "use-method"]
---
# The RED Method

> Lines beginning `> "` are **[VERBATIM]**. Anything else is an editorial note from the
> research stage and must not be quoted as source text.

## ⚠ AUTHORITY GUARDRAIL — READ FIRST

**This is the weakest citation in Chapter 18's corpus.** RED's original publication was on the
Weaveworks blog; Weaveworks is defunct and the CNCF TAG Observability whitepaper's RED link now
points to a dead host. What survives is Grafana Labs' republication, **written by Tom Wilkie, who
created the method**. That clears the stage's "not a third-party tutorial" bar — it is the
originating author — but it does **not** clear "official documentation," and no CNCF or Linux
Foundation source defines RED.

**Consequence, per the outline's stated fallback posture:** name RED, do not build teaching weight
on it, and **let no Practice question, Taking Your Bearings item, or Soundings question depend on
it.** If §7 keeps only one of the two methods in prose, keep USE — it is better sourced.

## The three metrics

> **Rate** — "the number of requests per second"

> **Errors** — "the number of those requests that are failing"

> **Duration** — "the amount of time those requests take"

## Why it exists alongside USE

> "The USE Method doesn't really apply to services; it applies to hardware, network disks, things
> like this. We really wanted a microservices-oriented monitoring philosophy, so we came up with
> the RED Method."

## Origin

Tom Wilkie "created [the RED Method] in 2015" after "a new employee asked what his monitoring
philosophy was."

## Drafting note for §7

The USE/RED contrast quote is the most useful thing on this page and it is the one that justifies
mentioning both at all: **USE is for resources, RED is for services.** That is a one-sentence
complementarity the outline asks §7 to convey, and it comes from the person who drew the line. It
also lands the Ch 17 §3 microservices anchor a second time — RED exists *because* one service became
twenty.

B1 gap **G21** named golden signals and RED/USE together. Golden signals were closed on 2026-08-23;
USE closed cleanly this run; **RED is closed only at tier 4.** G21 should be recorded as
substantially-but-not-fully closed rather than closed.
