---
source_url: "https://theupdateframework.io/"
secondary_source_url: "https://theupdateframework.io/docs/overview/"
fetched_at: "2026-08-31T11:17:00-0400"
authority: "The Update Framework (CNCF graduated)"
objectives_covered: ["D2 Security", "D2.2", "D4 Cloud Native Ecosystem"]
concepts_covered: ["tuf", "supply-chain-security", "image-signing"]
---
# The Update Framework — TUF (theupdateframework.io)

## What it is

"A framework for securing software update systems"

"maintains the security of software update systems, providing protection even against attackers that compromise the repository or signing keys"

"**TUF** is a CNCF graduated project."

## From the project overview

"[TUF is] a framework (a set of libraries, file formats, and utilities) that can be used to secure new and existing software update systems."

The overview lists attacks TUF is designed to withstand, in the project's own words:

- "An attacker keeps giving you the same file, so you never realize there is an update."
- "An attacker gives you an older, insecure version of a file that you already have and tricks you into thinking it's newer."
- "An attacker gives you a newer version of a file you have but it's still not the newest one."
- "An attacker compromises the key used to sign these files. Now you download a file that is properly signed, but is still malicious."

"TUF identifies the updates, downloads them, and checks them against the metadata that it also downloads from the repository. If the downloaded target files are trustworthy, TUF hands them over to your software update system."

> NOTE: TUF's role structure (root / targets / snapshot / timestamp), delegation and signing thresholds are **not** on these two pages. Do not describe them.
