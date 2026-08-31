Research complete. The PDF extraction is gated behind a permission this non-interactive stage can't obtain, so that gap persists — I'll record it precisely. Emitting the manifest as raw markdown per the stage-hygiene convention.

# Research Manifest — KCNA Chapter 19

Chapter 19 is a synthesis chapter with `domain_weight_pct: 0` and no new objectives. Its technical content is entirely retrieval from Chapters 2–18, whose sources are already cached — **295 snapshots** exist in `sources/`. I verified coverage for §2's confusion-pair inventory rather than re-fetching it, and spent the stage's effort on the one area Ch 19 genuinely opens: **exam-day mechanics** (§3, §5, §6), which no prior chapter needed.

That produced a correction with shipped-chapter consequences. See **Notes for the author, finding 1** — it is the most important output of this stage.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `lf-mc-exam-important-instructions-2026-08-31.md` | Linux Foundation (T&C DOCS) | — | exam-pacing, published-vs-commonly-reported, kcna-exam-format |
| `lf-mc-exam-faq-2026-08-31.md` | Linux Foundation (T&C DOCS) | — | exam-pacing, kcna-exam-format, cncf-certification-ladder |
| `lf-certification-resources-allowed-2026-08-31.md` | Linux Foundation (T&C DOCS) | — | the-lodestar, exam-pacing |
| `lf-exam-rules-and-policies-2026-08-31.md` | Linux Foundation (PSI Bridge candidate handbook) | — | exam-pacing, the-lodestar |
| `lf-handbook2-candidate-requirements-2026-08-31.md` | Linux Foundation (PSI Bridge candidate handbook) | — | exam-pacing |
| `lf-handbook2-taking-the-exam-2026-08-31.md` | Linux Foundation (PSI Bridge candidate handbook) | — | exam-pacing |
| `provenance-kcna-60-questions-2026-08-31.md` | Correction record (supersedes 08-23 file) | — | published-vs-commonly-reported |
| `cncf-curriculum-kcna-readme-2026-08-31.md` | CNCF (cncf/curriculum repo) | D1, D2, D3, D4 | domain-weight-allocation |

### Coverage verified, not re-fetched

§2's pair matrix is the chapter's centre of mass and draws on ~60 discriminations. I confirmed each has a cached authoritative source rather than duplicating snapshots:

- **Storage pairs** — `ReadWriteOncePod` present in 3 snapshots; `Recycle` in 3; access modes and reclaim policies in `k8s-docs-persistent-volumes-depth-2026-08-25.md` and `k8s-api-ref-persistentvolume-v1-2026-08-25.md`.
- **D4 governance** (TAG vs SIG, TOC vs Governing Board, SIG/WG/Committee) — `cncf-tags-current-structure-2026-08-31.md`, `cncf-charter-governance-bodies-2026-08-31.md`, `k8s-sig-list-and-groups-2026-08-31.md`, `k8s-community-governance-2026-08-23.md`.
- **D4 observability** (span vs trace, SLI/SLO/SLA, Prometheus pull vs Pushgateway) — `opentelemetry-signals-2026-08-23.md`, `sre-book-service-level-objectives-2026-08-31.md`, `prometheus-pushgateway-practices-2026-08-31.md`.
- **Mesh / serverless / autoscaling** — `istio-ambient-mode-2026-08-31.md`, `knative-overview-2026-08-23.md`, `k8s-docs-autoscaling-and-vpa-2026-08-31.md`, `k8s-docs-node-autoscaling-2026-08-31.md`.
- **D3 rollback homonym** — `k8s-docs-kubectl-rollout-2026-08-24.md` (Deployment) and `helm-rollback-cli-2026-08-31.md` (Helm) are distinct sources, which is exactly what the term-ledger homonym needs.
- **Version skew** — `k8s-version-skew-policy-2026-08-31.md`.

No gaps found in §2's technical substrate.

---

### A1 · `lf-mc-exam-important-instructions-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/important-instructions-mc"
fetched_at: "2026-08-31T18:36:00-0400"
authority: "The Linux Foundation — official candidate-facing T&C DOCS, 'Multiple Choice Exams: Important Instructions'"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "exam-pacing", "published-vs-commonly-reported"]
---

# Multiple Choice Exams: Important Instructions — Linux Foundation T&C DOCS

> THIS SNAPSHOT OVERTURNS A LOAD-BEARING CHAPTER 1 CLAIM AND A BOOK-LEVEL
> DO-NOT-RETRIEVE RULE. See the Ch 19 research manifest, "Notes for the author",
> finding 1. This page was NOT among the pages checked by the Ch 1 research.

Official Linux Foundation candidate-facing documentation, in the same T&C DOCS
family as the Multiple Choice FAQ. Governs the LF's multiple-choice exams as a
class. The KCNA exam page calls KCNA "an online, proctored, multiple-choice
exam", placing it in this class.

## Question count — PUBLISHED

"The multiple-choice exam is delivered online and consists of 60* multiple-choice questions."

The asterisk resolves to a footnote on the same page:

"* CNPA exam consists of 85 multiple-choice questions."

The asterisk is a CNPA carve-out. It is NOT a "subject to change" hedge and NOT
a statement that the count varies by exam generally.

## Duration — PUBLISHED

"Candidates have 90* minutes to complete the multiple-choice exam."

Footnote: "* CNPA candidates have 120 minutes to complete the exam."

## Results timing

"within 24 hours from the time that the exam is completed"

## Applications and windows during the exam

"Candidates are not allowed to have other applications or browser windows running except the one on which the Exam is being shown."

## Machine constraints

"You cannot take an exam using a virtual machine."

"One active monitor (either built in or external)" — "Dual Monitors are NOT supported"

"Latest version of Google Chrome" recommended. Personal devices preferred over
"work-provided devices".

## Testing location

Acceptable spaces must be "Clutter-free" with "No objects such as paper, writing
implements, electronic devices" visible. The space must be "well lit so that
proctor is able to see candidate's face, hands, and surrounding work area."
Public locations — "coffee shops, stores, open office environments" — are
prohibited.

## Identification

Valid government-issued photo ID with signature is mandatory. "The first and last
name on the ID must exactly match" the registered information. Acceptable
documents include passports, driver's licenses, and national identity cards.

## Sanctioned countries

Testing is permitted for sanctioned-country citizens only "OUTSIDE the sanctioned
country" with matching address documentation.

## Scope caveat — READ BEFORE CITING

The page is titled for multiple-choice exams generally and DOES NOT NAME KCNA.
This is the identical scope situation as the 75% passing score in
lf-mc-exam-faq-*.md, and the same phrasing discipline applies.

- CORRECT: "The Linux Foundation publishes a 60-question format for its
  multiple-choice exams, of which the KCNA is one."
- FALSE, do not write: "The Linux Foundation does not publish a question count."
- FALSE, do not write: "The KCNA exam page states the exam has 60 questions."
  (It is in the candidate handbook, not on the exam page. The exam page omits it —
  that remains confirmed by lf-kcna-exam-page-2026-08-23.md.)

## Question navigation — NOT PRESENT ON PAGE

No statement about skipping, flagging, marking for review, returning to previous
questions, changing an answer, a review screen, or how the exam is submitted.
Confirmed absent on targeted fetch 2026-08-31.
```

### A2 · `lf-mc-exam-faq-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/faq-mc"
fetched_at: "2026-08-31T18:38:00-0400"
authority: "The Linux Foundation — official candidate-facing T&C DOCS, 'Multiple Choice Exams: Frequently Asked Questions'"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "exam-pacing", "cncf-certification-ladder"]
---

# Multiple Choice Exams: FAQ — Linux Foundation T&C DOCS (full re-fetch)

Re-fetched in full for Ch 19. Supersedes the narrow 2026-08-23 capture, which
recorded only duration, passing score, and two absences. The 08-23 file's
statement that the question count is absent FROM THIS PAGE remains correct; the
count is published on a different page (see
lf-mc-exam-important-instructions-2026-08-31.md).

## How long will the exam take?

"Candidates are allowed 90 minutes to complete Multiple Choice Exams, with the exception of CNPA. CNPA candidates are allowed 120 minutes to complete the exam."

## What score is needed to pass the exam?

"A score of 75% or above must be earned to pass the Multiple Choice Exam."

## How is my exam scored?

"Upon completion, exams are scored automatically and barring any exceptions or technical difficulties, a score report will be sent to the candidate via email within 24 hours from the time that the exam was completed."

## How long is my certification valid for?

"Certifications are valid for 2 years."

## How do I renew my certification?

"Candidates have the option to retake and pass the exam to renew their certification. Certification Renewal must be completed prior to the certification expiration date. The renewed certification will remain current for a further 2 years effective from the date the exam is passed."

"Under the CARE program, passing a higher-level exam will automatically renew Associate-level certifications listed below."

- "KCNA: Passing the Certified Kubernetes Administrator (CKA) or Certified Kubernetes Application Developer (CKAD) exam will automatically renew your KCNA."
- "KCSA: Passing the Certified Kubernetes Security Specialist (CKS) exam will automatically renew your KCSA."

NOTE: this is the one place in the MC FAQ that NAMES KCNA, which anchors KCNA in
the multiple-choice exam class this page governs.

## How is the exam proctored?

"The certification exam is proctored remotely via streaming audio, video, and screen sharing feeds. The screensharing feed allows proctors to view candidates' desktops (including all monitors). The audio, video, and screen sharing feeds will be stored for a limited period of time in the event that there is a subsequent need for review."

"The main function of the proctors during the exam is to facilitate the check-in process and to monitor the session. They do not, nor are they expected to, have the technical expertise to weigh in or provide insight on the exam servers or exam content."

## What are the system requirements to take the exam?

"The online proctored exam is taken on PSI's Proctoring Platform 'Bridge', using the PSI Secure Browser (a web browser created to guarantee a secure exam delivery over a virtual connection)."

Candidates must provide their own computer with:

- "Supported OS: Please review the System Requirements, published by PSI, in particular the supported Operating System Information."
- "All browsers are supported, however PSI highly recommends using the latest version of Google Chrome for the best exam scheduling experience, and because the secure browser is Chrome-based and will give a more accurate experience."
- "One active monitor (either built in or external) (NOTE: Dual Monitors are NOT supported)"
- "Reliable internet access"
  - "Ensure others on the same internet connection are not performing activities that use excessive bandwidth (i.e. holding conference calls, streaming content, gaming, etc.)"
  - "A wired connection is often more stable and robust than a wireless connection"
  - "Turn off bandwidth-intensive services (e.g. file sync, dropbox, BitTorrent)"
- "Microphone" — "Please check to make sure it is working before you start your exam session."
- "Webcam" — "Ensure the webcam is capable of being moved as you will have to pan your surroundings to check for potential violations of exam policy."
- "We strongly advise test takers to avoid using work-provided devices for their exams, as this practice can result in technical challenges."

"Candidates are not allowed to have other applications or browser windows running except the one on which the Exam is being shown."

## What are the Testing Environment requirements to take the exam?

- "Clutter-free work area"
  - "No objects such as paper, writing implements, electronic devices, or other objects on top of surface"
  - "No objects such as paper, trash bins, or other objects below the testing surface"
- "Clear walls"
  - "No paper/print outs hanging on walls"
  - "Paintings and other wall décor is acceptable"
  - "Candidates will be asked to remove non-décor items prior to the exam being released"
- "Lighting"
  - "Space must be well lit so that proctor is able to see candidate's face, hands, and surrounding work area"
  - "No bright lights or windows behind the examinee"
- "Other"
  - "Candidate must remain within the camera frame during the examination"
  - "Space must be private where there is no excessive noise. Public spaces such as coffee shops, stores, open office environments, etc. are not allowed."

## What are the ID requirements to take the exam?

- "All IDs must be a valid (unexpired) Government-issued original, physical document (not photocopied or electronic)"
- "IDs must include the candidate's name, photo, and signature*" — "*Government-issued biometric IDs that do not contain signature will be accepted"
- "The first and last name on the ID must exactly match the verified name entered on your exam checklist"

Acceptable forms include: "International travel passport", "Government-issued
driver's license/permit", "Government-Issued local language ID (with photo and
signature)", "National identity card State or province-issued identity card",
"Alien registration card (green card or permanent resident/visa)".

## Question count — NOT PRESENT ON PAGE

Confirmed absent on full re-fetch 2026-08-31. The count IS published, on
important-instructions-mc. Absence here is a property of this page only.

## Question navigation — NOT PRESENT ON PAGE

No statement about skipping, flagging, or reviewing questions.
```

### A3 · `lf-certification-resources-allowed-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed"
fetched_at: "2026-08-31T18:37:00-0400"
authority: "The Linux Foundation — official candidate-facing T&C DOCS, 'Resources Allowed: All LF Certification Programs'"
objectives_covered: []
concepts_covered: ["the-lodestar", "exam-pacing", "kcna-exam-format"]
---

# Resources Allowed: All LF Certification Programs — Linux Foundation T&C DOCS

Directly load-bearing for Ch 19 §5. The Lodestar is a BEFORE-the-exam instrument.
Nothing may be consulted during a KCNA sitting.

## Multiple Choice and SkillCred exams — the governing sentence

"Candidates are NOT PERMITTED to access tools, resources or external sites when taking the Linux Foundation Multiple Choice OR SkillCred Exams."

## The contrast — performance-based exams DO allow documentation

This contrast is what makes the KCNA rule worth stating to a reader who has read
about CKA preparation, where open-documentation advice is ubiquitous.

### CKA and CKAD

Browser access permitted to:
- "Kubernetes Documentation https://kubernetes.io/docs/"
- "Kubernetes Blog https://kubernetes.io/blog/"
- "Helm Documentation https://helm.sh/docs/"
- Task-specific Quick Reference documentation
- CKA only: Gateway API Documentation

Search restriction: "using the search function on https://kubernetes.io/docs/ is allowed, but you must not open external search results."

### CKS

Kubernetes documentation plus Falco, etcd, NGINX Ingress Controller, Cilium, and
Istio documentation. Same external-search restriction.

### ICA (Istio Certified Associate)

"Istio Documentation https://istio.io/docs/", Istio Blog, Kubernetes Documentation,
and task-specific Quick Reference materials.

### CNPE

Kubernetes Documentation and Blog, plus task-specific Quick Reference documentation.

### LFCS

Terminal only: man pages, "Documents installed by the distribution (i.e.
/usr/share and its subdirectories)", and distribution packages.

## Universal requirement for the performance exams

Resources must be "used by candidates to work independently on exam tasks (i.e. not used for 3rd party assistance or research)."

## Supported phrasing for Ch 19 §5

- CORRECT: "KCNA is closed-book. The Linux Foundation permits no tools, resources
  or external sites during its multiple-choice exams."
- CORRECT: "The open-documentation advice you have read about CKA does not
  transfer to KCNA — that allowance is specific to the performance-based exams."
```

### A4 · `lf-exam-rules-and-policies-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-rules-and-policies"
fetched_at: "2026-08-31T18:37:00-0400"
authority: "The Linux Foundation — 'Exam Rules and Policies', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["exam-pacing", "the-lodestar"]
---

# Exam Rules and Policies — Linux Foundation Candidate Handbook (PSI BRIDGE)

## Conduct during the exam — verbatim

- "Candidate is not allowed to communicate with anyone other than the Proctor during the Exam"
- "Candidate is not allowed to read the questions out loud, to themselves during the exam"
- "Candidate is not allowed to leave their desk or step out of view of the webcam, unless they have been granted specific permission by the Proctor"
- "Candidate is not allowed to eat, drink (except clear liquids as per rule below), or chew gum"
- "Candidate is not allowed to wear any electronic device in their ears, on their face or on their body unless medically necessary"
- "Candidate must refrain from making excessive and/or repetitive noise"
- "Candidate must refrain from covering their mouth and/or face"

## Desk and room — verbatim

- "Desk must be clear of all notes and electronics"
- "Room must be quiet, private, and well-lit"
- "No one other than the Candidate can be present in the room"

## Scratch paper and note-taking — verbatim

"Candidate is not allowed to write or enter input on anything (whether paper, electronic device, etc.) outside of the Exam console screen"

CONSEQUENCE FOR CH 19 §3, worth stating plainly to the reader: there is no
scratch paper. A pacing plan cannot be written down at the start of the exam.
Whatever pacing rule the reader uses must be executable from memory. This is the
strongest available justification for the ★ Fixed Point the outline places on
the pacing rule.

## Score revocation

"Any suspicious activity will be addressed and will result in consequences including, but not limited to, revoking a passing score"

## Breaks — NOT PRESENT ON PAGE

No statement about whether breaks are permitted during a multiple-choice exam.

## Question navigation — NOT PRESENT ON PAGE

No statement about skipping, flagging, or reviewing questions.
```

### A5 · `lf-handbook2-candidate-requirements-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/candidate-requirements"
fetched_at: "2026-08-31T18:37:00-0400"
authority: "The Linux Foundation — 'Candidate Requirements', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["exam-pacing"]
---

# Candidate Requirements — Linux Foundation Candidate Handbook (PSI BRIDGE)

Supports Ch 19 §6 ("The Week Before") — these are the checks that belong on a
final-week list rather than on exam morning.

## System and hardware — verbatim

- "Supported OS: Please review the System Requirements, published by PSI, in particular the supported Operating System Information."
- "One active monitor (either built in or external) (NOTE: Dual Monitors are NOT supported)"
- "The Linux Foundation recommends a screen size of 15\" or higher to support the ExamUI."
- "The Linux Foundation recommends a screen resolution of 1080p."
- "Reliable internet access"
- "Microphone"
- "Webcam"

## Internet — verbatim

- "Ensure others on the same internet connection are not performing activities that use excessive bandwidth"
- "A wired connection is often more stable and robust than a wireless connection"
- "Turn off bandwidth-intensive services (e.g. file sync, dropbox, BitTorrent)"
- "HTTPS connectivity to AWS S3 endpoints like https://*.s3.amazonaws.com/* is required"

## Room and workspace — verbatim

- "Clutter-free work area"
- "No objects such as paper, writing implements, electronic devices, or other objects on top of surface"
- "Clear walls" with "No paper/print outs hanging on walls"
- "Space must be well lit so that proctor is able to see candidate's face, hands, and surrounding work area"
- "Space must be private where there is no excessive noise."
- "If the room in which the Candidate is taking a test has a door, it must be kept closed."

## ID and check-in — NOT PRESENT ON THIS PAGE

Covered on the sibling "Taking the Exam" page — see
lf-handbook2-taking-the-exam-2026-08-31.md.
```

### A6 · `lf-handbook2-taking-the-exam-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/taking-the-exam"
fetched_at: "2026-08-31T18:38:00-0400"
authority: "The Linux Foundation — 'Taking the Exam', Candidate Handbook (PSI BRIDGE Proctoring platform)"
objectives_covered: []
concepts_covered: ["exam-pacing"]
---

# Taking the Exam — Linux Foundation Candidate Handbook (PSI BRIDGE)

## Check-in window — verbatim

- "Candidates can click on the 'Take Exam' button, located in My Portal, up to 30 minutes before the scheduled exam time."
- "Candidates must start their exam no later than 30 minutes after the scheduled start time."
- "The wait time to get assigned to a Check-In Specialist should not exceed 15 minutes."

## Identity verification — verbatim

- "First and Last Name listed on their Linux Foundation ID account exactly matches the First and Last name displayed on the government-issued photo ID."
- "If the name on the ID is written in another language (e.g. Chinese, Korean, Japanese, Arabic, etc.), the name used for the exam must also be spelled in that language."
- "You will be prompted to upload a picture of a valid government-issued ID, with a signature."
- "You will be prompted to take a 'selfie' which will be used to compare with the photo shown on your Government issued ID."

## The timer cannot be paused — verbatim

"The system does not offer a way to pause the exam timer or to add time back to the exam during connection loss events."

DIRECTLY RELEVANT TO §3. The ninety minutes is a hard, unrecoverable budget even
across a technical fault. This is the sourced basis for the section's insistence
that the reader bank the first pass rather than spend the clock early.

## Whether check-in consumes exam time — NOT PRESENT ON PAGE

The page does not state whether check-in time counts against the 90 minutes.
DO NOT ASSERT EITHER WAY. See the Ch 19 manifest, Gaps.

## Question navigation — NOT PRESENT ON PAGE

No statement about the exam interface, flagging, or reviewing answers.
```

### A7 · `provenance-kcna-60-questions-2026-08-31.md` (new)
```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/important-instructions-mc"
fetched_at: "2026-08-31T18:40:00-0400"
authority: "Correction record. Primary evidence is the Linux Foundation T&C DOCS page cited above."
objectives_covered: []
concepts_covered: ["published-vs-commonly-reported"]
---

# CORRECTION — the 60-question figure IS published

> SUPERSEDES provenance-kcna-60-questions-2026-08-23.md. That file states
> "60 questions — NOT FOUND in any authoritative source." THAT STATEMENT IS
> FALSE and must not be relied on by any drafting or revision stage.

## What the 08-23 file got right

It correctly identified that the figure is repeated by third parties, and
correctly documented the CNCF-blog community post as one vector. That analysis
stands.

## What it got wrong

It generalised from a bounded search to an unbounded claim. It listed the pages
checked:

  "the LF KCNA exam page; the LF MC exam FAQ; the LF general certification FAQ;
   the LF exam-results handbook page; the CNCF KCNA page; the LFS250 outline"

The Linux Foundation T&C DOCS page "Multiple Choice Exams: Important
Instructions" was NOT among them. That page publishes the figure:

"The multiple-choice exam is delivered online and consists of 60* multiple-choice questions."

with the footnote "* CNPA exam consists of 85 multiple-choice questions."

## Current, accurate status of both figures

| Figure | Status | Where published |
|---|---|---|
| 90 minutes | PUBLISHED | LF KCNA exam page; MC FAQ; MC Important Instructions |
| 75% to pass | PUBLISHED | MC FAQ (for MC exams as a class) |
| 60 questions | PUBLISHED | MC Important Instructions (for MC exams as a class) |

Both the 75% and the 60 are published for MULTIPLE-CHOICE EXAMS AS A CLASS, in
the candidate handbook, and neither appears on the KCNA product page. KCNA is
placed in that class by its own exam page ("an online, proctored, multiple-choice
exam") and by the MC FAQ's CARE section, which names KCNA explicitly.

## The distinction that survives

The "published vs commonly reported" lesson is NOT dead — it changes shape. The
honest version is about WHERE an authority publishes a fact, not whether it does:

- The figures are real and published, in the candidate handbook.
- The product page a candidate is most likely to read omits them.
- Third parties repeat them without ever citing the handbook, which is why the
  claim LOOKS unsourced and why its provenance is worth teaching.

## Phrasings

- CORRECT: "The Linux Foundation publishes both figures in its candidate
  handbook, for multiple-choice exams as a class; neither appears on the KCNA
  exam page itself."
- FALSE, do not write: "The question count travels on repetition alone."
- FALSE, do not write: "The question count is not anywhere the certifying body writes."
```

### A8 · `cncf-curriculum-kcna-readme-2026-08-31.md` (new)
```markdown
---
source_url: "https://github.com/cncf/curriculum/blob/master/kcna/README.md"
fetched_at: "2026-08-31T18:39:00-0400"
authority: "Cloud Native Computing Foundation — cncf/curriculum repository, KCNA README"
objectives_covered: ["D1", "D2", "D3", "D4"]
concepts_covered: ["domain-weight-allocation"]
---

# KCNA curriculum README — CNCF publication channel

Primary-source corroboration of the current four-domain weights, in the
authority's own repository rather than on a marketing page. Supports Ch 19 §4's
— Dead Reckoning block.

## Description — verbatim

"The Kubernetes and Cloud Native Associate (KCNA) certification provides a beginner friendly option to learn about the Kubernetes community and vast cloud native ecosystem of projects."

## Domains and weightings — verbatim

- Kubernetes Fundamentals: 44%
- Container Orchestration: 28%
- Cloud Native Application Delivery: 16%
- Cloud Native Architecture: 12%

Agrees exactly with cncf-kcna-certification-page-2026-08-23.md,
lf-kcna-exam-page-2026-08-23.md, lf-kcna-program-changes-2026-08-23.md, and
cncf-kcna-curriculum-pdf-2026-08-23.md. Four independent CNCF/LF surfaces now
agree; the 44/28/16/12 split can be stated flatly.

## Version and status — NOT STATED

The README contains no curriculum version number, effective date, or statement of
current-vs-retired status. The effective date (2025-11-24) comes from the repo's
commit history — see cncf-curriculum-repo-kcna-versions-2026-08-23.md.

## Competency detail — NOT PRESENT

This README lists the four domains and their weights only. It does NOT enumerate
the competencies beneath each domain. For those, use
cncf-kcna-curriculum-pdf-2026-08-23.md or lf-kcna-program-changes-2026-08-23.md.
```

---

## Gaps

Flagged for the drafting stage. **Do not invent facts to fill these.**

### G1 — Question navigation, flagging, and skipping is UNPUBLISHED · blocks part of §3

This is the most consequential gap. The §4 section plan for §3 specifies "the first pass, **flagging and skipping**, the second pass" as the chapter's pacing method, and places a ★ Fixed Point on it. **No Linux Foundation or PSI page I could reach states that the multiple-choice exam interface supports flagging a question, skipping a question, returning to a previous question, or reviewing answers before submission.**

Confirmed absent on targeted fetch across six official pages: `faq-mc`, `important-instructions-mc`, `lf-handbook2`, `lf-handbook2/exam-rules-and-policies`, `lf-handbook2/candidate-requirements`, `lf-handbook2/taking-the-exam`.

The negative result is well-established, not a thin search. Two viable responses, author's call:

- **(a)** Write the pacing rule in terms the interface cannot invalidate — budget the clock, do not spend disproportionate time on any single item, answer everything since there is no penalty for a wrong answer — and drop the specific flag/skip mechanic.
- **(b)** Keep flag-and-skip but frame it conditionally ("if the interface offers a way to mark a question and return to it, use it"), which is honest but weak for a ★ Fixed Point.

I'd recommend **(a)**. A Fixed Point should not rest on an unverified interface affordance, and A4's sourced "no writing outside the Exam console screen" already gives §3 a stronger, fully-sourced spine.

### G2 — Retired five-domain weights still unextracted · affects §4

The §4 plan asserts "D3 doubled from **8% to 16%**". The 16% is sourced four ways. **The 8% is not sourced at all.**

The retired PDF is at `https://raw.githubusercontent.com/cncf/curriculum/master/old-versions/KCNA_Curriculum%20old.pdf` (151.9 KB, confirmed reachable this stage — the earlier 404/blob-viewer problem recorded in `cncf-curriculum-repo-kcna-versions-2026-08-23.md` is resolved; the correct URL is the `raw.githubusercontent.com` host, not `github.com/.../raw/...`, which 302s). WebFetch returns it as binary and cannot decode it. I attempted local text extraction; the sandbox denied both the file write and the inline Python, so this stage could not close it.

**Route to close:** the binary is already on disk at
`C:\Users\user1\.claude\projects\C--dev-lodestar-certcomp\d388d963-c143-4111-9729-fe2603d659a3\tool-results\webfetch-1788215712852-wdpszt.bin`
A stage or session with write/execute permission can extract it with `pypdf`/`pdftotext` in under a minute.

Until then: §4 may state the **qualitative** change, which IS sourced — "observability will be rolled under Cloud Native Architecture" (`lf-kcna-program-changes-2026-08-23.md`) — and must not state the retired percentages. A web search surfaced 46/22/16/8/8, but only from third-party study repos and the non-authoritative CNCF community blog post; per the priority order those are not acceptable sources, and `cncf-curriculum-repo-kcna-versions-2026-08-23.md` already carries a standing instruction not to draft these from third-party guides.

### G3 — Whether check-in time counts against the 90 minutes · minor, §3/§6

Not stated on any page. The 30-minutes-early access and the ≤15-minute specialist wait are sourced (A6), so §6 can tell the reader to start check-in early without claiming what it costs them.

### G4 — Sub-objective identifiers `D1.1`–`D4.3` are not published

CNCF/LF publish **domains with named competencies, unnumbered**. The outline's `kb_tags` identifiers are a book-internal positional index. They happen to map cleanly — see Notes finding 3 — but no source states "D4.3". Ch 19 must not present these codes as the authority's own numbering.

### G5 — No external source for the chapter's pedagogical constructs

`cross-cutting-themes`, `absent-component-pattern`, `confusion-pair-matrix`, `discriminating-question`, and `the-lodestar` are Lodestar-authored constructs. This is expected for a synthesis chapter, not a defect — but it means §1, §2, §5, and §6 are **entirely internal-retrieval sections**, and their factual content must be traceable to shipped Chapters 2–18 and their existing snapshots, never to new external claims.

### G6 — `the-lodestar.md` does not exist · blocks §5 · not resolvable by research

Confirmed: the Book-KCNA root contains only `chapter-01` … `chapter-18`, `README.md`, and `sources/`. No `the-lodestar.md`, no `glossary.md`, no front matter, no `00-table-of-contents.md`. This is the outline's Open Question #1 and it stands. Research cannot close it — it needs authoring. §5 is pinned by a published pointer at `chapter-01-taking-departure.md:452`.

---

## Notes for the author

### 1. The book teaches, in a shipped chapter, a fact that is wrong — and it is one of the book's signature epistemics lessons

This is the finding that matters most from this stage. Please read before Ch 19 drafts.

`chapter-01-taking-departure.md` builds a teaching moment around the claim that the 60-question figure is unpublished. Three shipped passages:

- **line 204** — "It is two facts with two pedigrees: a passing standard the certifying body publishes, and **a question count that travels on repetition alone.**"
- **line 211** — a ⚠ hazard warning the reader that a 90-second-per-question rule may be built on sand.
- **line 341** — an **answer key**: "**A is wrong.** The question count is not on the exam page — **or anywhere else the certifying body writes.** '60 questions' is a third-party report, repeated so consistently that it reads as official. It isn't."

The certifying body does write it, in its candidate handbook. Line 341 is the worst placement for the error: it is the explanation of why a reader's answer was wrong, on a point the chapter uses to establish its own credibility about sourcing.

The root cause is visible and benign — `provenance-kcna-60-questions-2026-08-23.md` enumerated six pages it checked and then generalised to "any authoritative source." `important-instructions-mc` was not among the six. The reasoning was sound; the search was one page short.

**Blast radius, measured:** contained to Chapter 1. A targeted grep for `commonly reported|60 question|60 multiple` across `chapter-*.md` returns hits only in `chapter-01`. Other chapters' bare "60" matches are incidental (ports, values).

**Three downstream artifacts also encode the false premise:**

- `arc-outline.md:396` — do-not-retrieve item 3, "**The 60-question and 75% figures.** Unpublished and commonly-reported."
- `retrieval-architecture.md:19` — "the **unpublished** 60-question/75% figures".
- `arc-outline.md:368` — the Ch 20 mock disclosure: "60 questions is *commonly reported* and must be framed as a calibrated instrument sized to the commonly reported format, **never as a match to a published count.**"

Note that the **75% figure was already known to be published** — `lf-mc-exam-faq-2026-08-23.md` says so explicitly and even warns "FALSE, do not write: 'The Linux Foundation does not publish a passing score.'" So item 3 was half-wrong the day it was written, and is now fully wrong. That inconsistency between the Ch 1 snapshot and the book-level do-not-retrieve list has been sitting unreconciled since B3.

**The good news for Ch 20:** the mock is 60 questions and the published format is 60 questions. The disclosure at `arc-outline.md:368` can be simplified from an apology into a straightforward statement that the instrument matches the published format.

**My recommendation, briefly:** the lesson is worth saving, not deleting. Rewrite Ch 1 around *where* an authority publishes rather than *whether* it does — the product page a candidate actually reads omits both figures; the candidate handbook carries both; third parties repeat them without ever citing the handbook. That is a truer and more useful lesson about sourcing than the current one, it preserves the ⚠ and the practice question with modest surgery, and it keeps line 211's pacing caution intact because the handbook page scopes to MC exams generally, carves out CNPA, and never names KCNA.

This is a Chapter 1 revision decision, outside Ch 19's scope. Flagging it here because Ch 19 §3 cannot be drafted coherently until it is settled — §3 either inherits Ch 1's claim and repeats an error, or contradicts a shipped chapter.

### 2. §3's design survives the correction, and improves

The outline built §3 around "the pacing arithmetic cannot be a fixed seconds-per-question number." That instinct is still right, for a better reason: the count is published for *multiple-choice exams as a class*, with a CNPA exception, and the page never names KCNA. So "read the count off the screen and divide" remains correct practice — but §3 can now offer 60 ÷ 90 minutes = 90 seconds per question as a **published** worked example rather than a hedged third-party one. The section gets stronger and more concrete.

Two newly sourced facts materially strengthen it:

- **There is no scratch paper** (A4: "not allowed to write or enter input on anything … outside of the Exam console screen"). The pacing rule must be executable from memory. This is the best available justification for the ★ the outline places there.
- **The timer cannot be paused or recovered**, even across a connection loss (A6). That is the sourced spine for "bank the first pass."

### 3. The `D1.1`–`D4.3` numbering maps cleanly, and D4.3 checks out

Worth recording because §4 makes a specific call about D4.3. The published curriculum lists competencies in order under each domain, and the outline's codes are a positional index into those lists:

| Domain | Published competencies, in order | Codes |
|---|---|---|
| D1 Kubernetes Fundamentals 44% | Core Concepts · Administration · Scheduling · Containerization | D1.1–D1.4 |
| D2 Container Orchestration 28% | Networking · Security · Troubleshooting · Storage | D2.1–D2.4 |
| D3 Cloud Native Application Delivery 16% | Application Delivery · Debugging | D3.1–D3.2 |
| D4 Cloud Native Architecture 12% | Observability · Cloud Native Ecosystem and Principles · **Cloud Native Community and Collaboration** | D4.1–D4.3 |

The counts match the outline's `kb_tags` exactly (4/4/2/3), and **D4.3 does resolve to "Cloud Native Community and Collaboration"** — so §4's under-studied-competency call is correctly targeted. Per G4, treat the codes as internal shorthand only.

Minor curiosity, already recorded in `cncf-kcna-curriculum-pdf-2026-08-23.md`: the official PDF contains the typo "Could Native Community and Collaboration". The README (A8) and the LF program-changes page spell it correctly. Nothing to do; noted so nobody "fixes" a correct quotation.

### 4. A newly sourced discrimination that §2 may want, and §5 needs

A3 establishes that **KCNA is closed-book** while CKA/CKAD/CKS/ICA/CNPE explicitly permit browser access to documentation. Readers preparing for KCNA are swimming in CKA advice, where "know how to search the docs fast" is standard guidance. That advice actively misleads a KCNA candidate.

This is arguably a genuine confusion pair for §2's D3/D4 group — *closed-book multiple-choice vs open-documentation performance-based* — and it is fully sourced. It is not in B1's 114-trap inventory, so adding it is an author's call, not something drafting should do unilaterally. It is unambiguously required in §5, since "how to use the Lodestar in the last hour" only makes sense once the reader knows it cannot come into the exam with them.

### 5. Sources agree; no conflicts found

No disagreement between the Linux Foundation and CNCF surfaces on anything Ch 19 touches. The 44/28/16/12 split now has four independent CNCF/LF confirmations. Duration is consistent across three pages. The only tension in the research record was internal to the book's own artifacts — the do-not-retrieve list versus the Ch 1 FAQ snapshot on the 75% figure — described in finding 1.

### 6. Two stage-mechanics notes

- **The 08-23 provenance file must not be left as-is.** A7 supersedes it, but the old file remains on disk and asserts "NOT FOUND in any authoritative source." A Ch 1 revision stage that reads `sources/` will find both and may trust the older one. Recommend the author either delete `provenance-kcna-60-questions-2026-08-23.md` or prepend a pointer to A7.
- **`cncf-curriculum-repo-kcna-versions-2026-08-23.md` contains a stale URL.** Its recorded retrieval URL 302-redirects; the working host is `raw.githubusercontent.com`. Worth patching when G2 is closed, so the next attempt does not re-lose the time.