---
source_url: "https://argo-cd.readthedocs.io/en/stable/user-guide/best_practices/"
fetched_at: "2026-08-31T06:15:00-0400"
authority: "Argo project (Argo CD; CNCF graduated)"
objectives_covered: ["D3.1"]
concepts_covered: ["source-of-truth", "versioned-and-immutable-principle", "cicd", "tracking-branch-tag-commit"]
---
# Argo CD — Best Practices

## Separating config vs. source code repositories
Reasons given for keeping application configuration in a repository separate from application source:

1. "It provides a clean separation of application code vs. application config."
2. "For auditing purposes, a repo which only holds configuration will have a much cleaner Git history of what changes were made."
3. "Your application may comprise services built from multiple Git repositories, but is deployed as a single unit."
4. "The developers who are developing the application, may not necessarily be the same people who can/should push to production environments."
5. "Pushing manifest changes to the same Git repository can trigger an infinite loop of build jobs and Git commit triggers. Having a separate repo to push config changes to, prevents this from happening."

## Ensuring manifest immutability
On tracking an unstable revision such as HEAD: "Since this is not a stable target, the manifests for this kustomize application can suddenly change meaning, even without any changes to your own Git repository."

"A better version would be to use a Git tag or commit SHA."
