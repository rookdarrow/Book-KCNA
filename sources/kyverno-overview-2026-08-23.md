---
source_url: "https://kyverno.io/docs/introduction/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kyverno project (CNCF)"
objectives_covered: ["D2 Security"]
concepts_covered: ["kyverno", "policy-engine", "admission-controller", "validate", "mutate", "generate", "image-verification", "opa-gatekeeper"]
---
# Kyverno (kyverno.io/docs/introduction/)

Kyverno (Greek for "govern") is a cloud native policy engine. It was originally built for Kubernetes and now can also be used outside of Kubernetes clusters as a unified policy language. Kyverno allows platform engineers to automate security, compliance, and best practices validation and deliver secure self-service to application teams. Policies can validate, mutate, generate, or clean up Kubernetes resources; verify container images and metadata for software supply chain security; and be applied as a Kubernetes admission controller (webhook) or as a CLI-based scanner. Policies are written in YAML using declarative rules and CEL (Common Expression Language), managed as Kubernetes resources, and version-controlled with tools such as Git. The other widely used Kubernetes policy engine is Open Policy Agent (OPA, a CNCF graduated project) with its Gatekeeper admission controller, which expresses policy in the Rego language.
