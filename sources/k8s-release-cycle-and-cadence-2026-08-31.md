---
source_url: "https://kubernetes.io/releases/release/"
fetched_at: "2026-08-31T09:56:00-0400"
authority: "Kubernetes project (kubernetes.io/releases + kubernetes/community sig-release charter)"
objectives_covered: ["D4.3"]
concepts_covered: ["sig-release-and-release-cadence", "kubernetes-enhancement-proposal", "subproject"]
---
# The Kubernetes release cycle and cadence — refreshed 2026-08-31

**This snapshot exists to source §8's Fixed Point** — that three minor releases a
year and three supported minor versions are one fact stated twice. Chapter 13
removed the cadence clause for want of a tag (recorded at chapter-13:1255). This
is that tag.

## Source A — kubernetes.io/releases/release/ (verbatim)

### Cadence

> "Kubernetes releases currently happen approximately three times per year."

### The three phases

> "The release process can be thought of as having three main phases:
> Enhancement Definition, Implementation, Stabilization"

### The cycle, in weeks

> "Normal Dev (Weeks 1-11)"

> "Code Freeze (Weeks 12-14)"

> "Post-Release (Weeks 14+)"

> "**Enhancements Freeze** starts ~4 weeks into release cycle."

> "**Code Freeze** starts in week ~12 and continues for ~2 weeks. Only critical
> bug fixes are accepted into the release codebase during this time."

### Who runs it

> "The process for shepherding enhancements, issues, and pull requests into a
> Kubernetes release spans multiple stakeholders: the enhancement, issue, and
> pull request owner(s); SIG leadership; the Release Team"

## Source B — kubernetes.io/releases/ (verbatim), refreshed

> "The Kubernetes project maintains release branches for the most recent three
> minor releases (1.37, 1.36, 1.35)."

> "Kubernetes 1.19 and newer receive approximately 1 year of patch support.
> Kubernetes 1.18 and older received approximately 9 months of patch support."

Supported releases and end-of-life dates as of this snapshot:
1.37 — End of Life 2027-10-28 · 1.36 — End of Life 2027-06-28 ·
1.35 — End of Life 2027-02-28

*(Supersedes the version list in `k8s-releases-cadence-2026-08-23.md`, which
recorded 1.36/1.35/1.34. See manifest Notes 2. The durable facts — three branches,
~1 year of patch support — are unchanged.)*

## Source C — kubernetes/community sig-release charter (verbatim)

> "Production of Kubernetes releases on a reliable schedule"

> "Ensure there is a consistent group of community members in place to support
> the release process across time."

> "Defining and staffing release roles to manage the resolution of release
> blocking criteria"

> "Defining and driving development processes (e.g. merge queues, cherrypicks)
> and release processes (e.g. burndown meetings, cutting pre-releases)"

> "Managing the creation of release specific artifacts, including: Code branches,
> Binary artifacts, Container Images, Release notes."

> the "Release Engineering subproject", which is "dedicated to the technical
> aspects of Kubernetes releases, for example its tooling and source code
> ownership"

---
DRAFTING NOTE (not from source): the arithmetic §8 needs is now fully sourced and
lands cleanly. Three releases a year × three maintained branches ≈ one year of
patch support — and "approximately 1 year of patch support" is stated
independently on the same page, so the reader's derivation is CONFIRMED by the
source rather than merely permitted by it. That is exactly the "one fact stated
twice" the outline asks for, and it can be shown rather than asserted.

⚠ ONE CAUTION: the "approximately every 15 weeks" figure lives ONLY in
`k8s-releases-cadence-2026-08-23.md`. Today's pages state "approximately three
times per year" and a cycle whose code freeze starts in week ~12 and whose
post-release phase begins at week 14+. If §8 wants a week count, "roughly
fourteen weeks" is what the live release-cycle page supports; "fifteen" must
carry the 08-23 tag. Simplest safe course: teach "three times a year", which is
current, sourced, and the half the exam would test.

The sig-release charter also gives §8 its "subproject" example for free — Release
Engineering — which the reader can hold next to the SIG/subproject definition in
`k8s-community-governance-2026-08-23.md`.
