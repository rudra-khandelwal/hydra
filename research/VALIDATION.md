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
| GitHub button opens the repository directly in a new tab without opener redirect | Implemented | Deployed in run #86 | Pending live test |
| Created research notes start at section 18 | Implemented | Pending latest control-pass deploy | Pending live test |

## Current UI interaction validation — 25 September 2026

| Check | Source | Deployment | Live verification |
|---|---|---|---|
| Project Map primary sequence is Hydra Launcher → Setup → Build → Security Research → Research → Project Control → Created Notes | Implemented | Deployed in run #86 | Pending live test |
| Project Map clicks update follower sidebar and main document | Implemented | Deployed in run #86 | Pending live test |
| Detailed-sidebar navigation updates Project Map active category | Implemented | Deployed in run #86 | Pending live test |
| Project Map Hydra Launcher targets #guide-top | Implemented | Deployed in run #86 | Pending live test |
| Final detailed-sidebar item remains reachable | Implemented | Deployed in run #86 | Pending live test |
| Project Control buttons transparent by default | Implemented | Deployed in run #86 | Pending live test |
| Capitalized navigation labels | Implemented | Deployed in run #86 | Pending live test |
| Canonical original visual theme preserved for both rails | Implemented | Deployed in run #86 | Pending live test |
| Hero GitHub repo button is direct new-tab repository link | Implemented | Deployed in run #86 | Pending live test |

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
