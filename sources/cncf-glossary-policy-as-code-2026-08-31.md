---
source_url: "https://glossary.cncf.io/policy-as-code/"
fetched_at: "2026-08-31T11:30:00-0400"
authority: "CNCF Cloud Native Glossary — CC BY 4.0, The Linux Foundation / CNCF"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem and Principles"]
concepts_covered: ["policy-engine", "validate-mutate-generate", "opa", "kyverno", "admission-time-vs-runtime"]
---
# Policy as Code (PaC) — CNCF Cloud Native Glossary (glossary.cncf.io/policy-as-code/)

## What it is

"Policy as Code is the practice of storing the definition of policies as one or more files in machine-readable and processable form."

## Problem it addresses

Organizations implement numerous policies — for example security restrictions on secrets in source code, or on container permissions — that developers must verify. Checking policy compliance manually is resource-intensive and error-prone, and struggles to keep pace with the demands of cloud native applications.

## How it helps

Codifying policies enables consistent, automated enforcement while reducing human error. Version control systems such as Git track policy changes, creating an audit trail and allowing teams to identify who made a change and to revert it.

> FIDELITY NOTE: only the "What it is" sentence is verbatim. The "Problem it addresses" and "How it helps" paragraphs are **condensed** from the entry and must not be quoted as the glossary's own wording. The load-bearing sentence for §8 is the first one, and it is exact.
>
> The CNCF glossary index was checked on 2026-08-31 for security and supply-chain terms. The complete list of relevant entries is: Cloud Native Security, DevSecOps, Digital Certificate, Mutual Transport Layer Security (mTLS), Policy as Code (PaC), Role-Based Access Control (RBAC), Security Chaos Engineering, Transport Layer Security (TLS), Zero Trust Architecture. **There is no SBOM entry and no supply-chain-security entry.**
