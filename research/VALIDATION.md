# Validation Matrix

This file separates source implementation from deployment and live behavior.

## Status meanings

- **Implemented** — present in repository source.
- **Deployed** — GitHub Pages deployment succeeded for the relevant commit.
- **Live-verified** — exercised against the published guide.
- **Pending** — still needs user/browser verification.

## Live guide

| Check | Source | Deployment | Live verification |
|---|---|---|---|
| README live-guide link opens separately | Implemented | Deployed in control-pass run #66 | Pending live test |
| GitHub opener refreshes once | Implemented | Deployed in control-pass run #66 | Pending live test |
| Desktop/tablet sidebar stays fixed during document scroll | Implemented | Deployed in control-pass run #66 | Pending live test |
| Mobile navigation remains slide-out | Implemented | Deployed in control-pass run #66 | Pending live test |
| Overview targets hero | Implemented | Deployed in control-pass run #66 | Pending live test |
| Only one GitHub repo button beside Hydra Launcher | Implemented | Deployed in control-pass run #66 | Pending live test |
| GitHub button focuses originating GitHub tab when available | Implemented | Deployed in control-pass run #66 | Pending live test |
| Direct-open GitHub button fallback opens repository separately | Implemented | Deployed in control-pass run #66 | Pending live test |
| Created research notes start at section 18 | Implemented | Pending latest control-pass deploy | Pending live test |

## Repository integrity

| Check | Status |
|---|---|
| Repository is public | Verified |
| No secrets intentionally committed | Ongoing public-release review |
| Research findings state uncertainty | Verified by current FINDINGS.md |
| Canonical checkpoint directory is lowercase | Verified |
| README/repository map is current | Implemented; final tree review still required |

## Security research

| Check | Status |
|---|---|
| Runtime baseline | Complete |
| API/download-source correlation | Complete |
| AV/AMSI control observation | Complete |
| Legitimate controlled download | Next major experiment |
| Downloaded-artifact static analysis | Pending |
| Download-time process/network/filesystem differential | Pending |
| Source correlation for controlled download | Pending |
| Final security verdict | Not established |

## Rule

Never mark a live-browser behavior “verified” from source inspection alone.
