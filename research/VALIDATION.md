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
| README live-guide link opens separately | Implemented | Pending latest control-pass deploy | Pending |
| GitHub opener refreshes once | Implemented | Pending latest control-pass deploy | Pending |
| Desktop/tablet sidebar stays fixed during document scroll | Implemented | Pending latest control-pass deploy | Pending |
| Mobile navigation remains slide-out | Implemented | Pending latest control-pass deploy | Pending |
| Overview targets hero | Implemented | Pending latest control-pass deploy | Pending |
| Only one GitHub repo button beside Hydra Launcher | Implemented | Pending latest control-pass deploy | Pending |
| GitHub button focuses originating GitHub tab when available | Implemented | Pending latest control-pass deploy | Pending |
| Direct-open GitHub button fallback opens repository separately | Implemented | Pending latest control-pass deploy | Pending |
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
