---
source_url: "https://github.com/kubernetes/community/blob/master/community-membership.md"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes/community)"
objectives_covered: ["D4 Community and Collaboration"]
concepts_covered: ["contributor-ladder", "member", "reviewer", "approver", "subproject-owner", "owners-files"]
---
# Community membership — the Kubernetes contributor ladder (github.com/kubernetes/community/blob/master/community-membership.md)

| Role | Responsibilities | Requirements |
|---|---|---|
| Member | Active contributor in the community | Sponsored by 2 reviewers and multiple contributions to the project |
| Reviewer | Review contributions from other members | History of review and authorship in a subproject |
| Approver | Contributions acceptance approval | Highly experienced active reviewer and contributor to a subproject |
| Subproject Owner | Set direction and priorities for a subproject | Demonstrated responsibility and excellent technical judgement for the subproject |

**Member** — must have enabled two-factor authentication on their GitHub account; have made multiple contributions to the project or community, enough to demonstrate an ongoing and long-term commitment to the project; be subscribed to dev@kubernetes.io; have read the contributor guide; be sponsored by 2 reviewers (from different companies); open a membership request issue in kubernetes/org.

**Reviewer** — member for at least 3 months; primary reviewer for at least 5 PRs to the codebase; reviewed or merged at least 20 substantial PRs to the codebase; knowledgeable about the codebase; sponsored by a subproject approver. Reviewers are listed in OWNERS files.

**Approver** — reviewer for at least 3 months; primary reviewer for at least 10 substantial PRs; reviewed or merged at least 30 PRs; nominated by a subproject owner. Approvers are responsible for the holistic acceptance of a contribution — backwards/forwards compatibility, API and flag definitions, subtle performance and correctness issues, interactions with other parts of the system.

**Subproject Owner** — defined by entries in sigs.yaml and the subproject's OWNERS files; sets technical direction and makes or approves design decisions for their subproject.
