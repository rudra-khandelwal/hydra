# Repository Map

This is the canonical map of the public research workspace.

## Top level

```
.
├── .github/
│   └── workflows/
│       └── pages.yml                 GitHub Pages deployment
├── docs/                             Stable project/methodology documentation
├── research/                         Chronology, findings, validation and checkpoints
├── security-research/                Sanitized evidence organization
├── upstream/                         Upstream provenance and synchronization notes
├── index.html                        Public live guide
├── favicon.svg                       Public guide favicon
├── README.md                         Public repository entry point
├── SECURITY.md                       Security/research handling rules
└── CONTRIBUTING.md                   Change discipline
```

## docs/

- `PROJECT.md` — project definition and scope
- `PROJECT-GOAL.md` — goal, phases, success criteria
- `PROJECT-MEMORY.md` — canonical AI/maintainer handoff memory
- `REPOSITORY-MAP.md` — this repository map
- `CHANGE-CONTROL.md` — required modification and verification process
- `ARCHITECTURE.md` — source/runtime architecture research
- `NETWORK-ANALYSIS.md` — network-analysis documentation
- `SECURITY-METHODOLOGY.md` — research methodology
- `THREAT-MODEL.md` — trust boundaries and threat categories
- `PUBLICATION-CHECKLIST.md` — ongoing public-repository safety checklist
- `WINDOWS-BUILD.md` — Windows build notes

## research/

- `DIARY.md` — chronological record
- `AGENDA.md` — active backlog and next work
- `FINDINGS.md` — supported findings only
- `LESSONS.md` — mistake/correction/prevention log
- `VALIDATION.md` — current verification matrix
- `TEMPLATE.md` — checkpoint template
- `checkpoints/` — dated standalone research checkpoints

**Path rule:** use the lowercase `research/checkpoints/` directory only. Do not create a second `CHECKPOINTS/` directory because Windows filesystems are commonly case-insensitive.

## security-research/

Current tracked files:

- `README.md` — evidence-area rules and sensitive-data handling
- `evidence-template.md` — compact template for recording sanitized evidence

The evidence-area subdirectories `baseline/`, `network/`, `processes/`, `filesystem/`, `hashes/`, and `reports/` are reserved for future material; they are not currently present in the repository tree. Create them when the corresponding sanitized evidence is actually added.

Raw credential-bearing or sensitive material stays outside Git or in ignored local paths.

## upstream/

- `UPSTREAM.md` — provenance and synchronization rules
- `README.md` — upstream workspace notes

## Generated/public site

- `index.html` is the GitHub Pages entry point.
- `favicon.svg` is the public favicon.
- `.github/workflows/pages.yml` deploys the repository root to GitHub Pages.

## Design rule

Documentation should point to stable canonical files rather than duplicating the same operational state in multiple places.
