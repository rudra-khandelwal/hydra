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
| README live-guide link opens separately | Implemented | Deployed in run #116 | Pending live test |
| GitHub opener refreshes once | Implemented | Deployed in run #116 | Pending live test |
| Desktop/tablet sidebar stays fixed during document scroll | Implemented | Deployed in run #116 | Pending live test |
| Mobile navigation remains slide-out | Implemented | Deployed in run #116 | Pending live test |
| Overview targets hero | Implemented | Deployed in run #116 | Pending live test |
| Only one GitHub repo button beside Hydra Launcher | Implemented | Deployed in run #116 | Pending live test |
| GitHub button opens the repository directly in a new tab without opener redirect | Implemented | Deployed in run #116 | Pending live test |
| Created research notes start at section 18 | Implemented | Pending latest control-pass deploy | Pending live test |

## Current UI interaction validation — 25 September 2026

| Check | Source | Deployment | Live verification |
|---|---|---|---|
| Project Map primary sequence is Hydra Launcher → Setup → Build → Security Research → Research → Project Control → Created Notes | Implemented | Deployed in run #116 | Pending live test |
| Project Map clicks update follower sidebar and main document | Implemented | Deployed in run #116 | Pending live test |
| Detailed-sidebar navigation updates Project Map active category | Implemented | Deployed in run #116 | Pending live test |
| Project Map Hydra Launcher targets #guide-top | Implemented | Deployed in run #116 | Pending live test |
| Final detailed-sidebar item remains reachable | Implemented | Deployed in run #116 | Pending live test |
| Project Control buttons transparent by default | Implemented | Deployed in run #116 | Pending live test |
| Capitalized navigation labels | Implemented | Deployed in run #116 | Pending live test |
| Canonical original visual theme preserved for both rails | Implemented | Deployed in run #116 | Pending live test |
| Hero GitHub repo button is direct new-tab repository link | Implemented | Deployed in run #116 | Pending live test |

## Deployment snapshot — 25 September 2026

The final A-to-Z audit guide/source state was deployed successfully in **Pages run #116** for commit `3801b5411a58d8e6a17a863156907106fc3739bc`. The current commit is a documentation-only follow-up that records this deployment snapshot; it does not change the guide's functional source. Browser-level live verification remains pending.

## Layout audit — 25 September 2026

A static geometry audit found that the Project Map was previously enabled too early: at 1280px there was not enough outer margin for the 155px rail plus its 14px gap before the 250px detailed sidebar. The Project Map breakpoint was moved to **1536px** so the two rails do not overlap. Browser-level live verification remains pending.

## Security hardening audit — 25 September 2026

| Check | Status |
|---|---|
| Public maintainer page contains no repository write token field | Implemented in latest source |
| Public maintainer page performs no GitHub Contents write API calls | Implemented in latest source |
| Maintainer upload uses GitHub authenticated web flow | Implemented in latest source |
| Research-note action buttons avoid inline ID-bearing handlers | Implemented in latest source |
| Clearing an edited note exits edit mode | Implemented in latest source |
| Deleting an edited note clears edit state | Implemented in latest source |
| Cross-device/server persistence for Research Notes | Not implemented; browser-local only |

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
