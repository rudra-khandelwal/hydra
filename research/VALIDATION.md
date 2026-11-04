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
| README live-guide link opens separately | Implemented | Deployed | Pending live test |
| GitHub opener refreshes once | Implemented | Deployed | Pending live test |
| Desktop/tablet sidebar stays fixed during document scroll | Implemented | Deployed | Pending live test |
| Mobile navigation remains slide-out | Implemented | Deployed | Pending live test |
| Overview targets hero | Implemented | Deployed | Pending live test |
| Only one GitHub repo button beside Hydra Launcher | Implemented | Deployed | Pending live test |
| GitHub button opens repository directly in a new tab | Implemented | Deployed | Pending live test |

## Repository integrity

| Check | Status |
|---|---|
| Repository is public | Verified |
| No secrets intentionally committed | Ongoing public-release review |
| Research findings state uncertainty | Verified by current FINDINGS.md |
| Canonical checkpoint directory is lowercase | Verified |
| README/repository map is current | Final tree review still required |

## Security research status — 4 November 2026 (updated after second candidate search)

| Check | Status | Evidence/limitation |
|---|---|---|
| Windows runtime baseline | Complete (historical) | Processes, established network connections, and repository files were recorded. Re-capture only when a new controlled experiment needs a fresh baseline. |
| Hydra/Electron process and HTTPS observations | Observed (historical) | Process-to-HTTPS association recorded; not a complete endpoint-purpose/security verdict. |
| Source/API metadata correlation | Complete (historical) | Source IDs and an API-returned record were observed and correlated with client code. Does not establish tracker/peer transfer or artifact behavior. |
| Trust-boundary review | Complete (architectural) | Hydra client, API, community metadata, and third-party infrastructure distinguished. |
| Client-code inspection | Complete for prior scope | Relevant source storage, sync, request, and URI-filter paths inspected; not a full code security audit. |
| EICAR/AMSI interception | Observed with limitation | EICAR string blocked during PowerShell assignment. No valid EICAR file or quarantine event established. |
| Second focused authorized-artifact candidate search | Complete for reported scope; no candidate approved | Mindustry, OpenTTD, Hedgewars, Battle for Wesnoth, and SuperTuxKart checked. Mindustry had one OnlineFix option but its specific payload/release and authorization were not verified. OpenTTD showed “No downloads available”; the other three had no current downloadable entry established. Not an exhaustive catalogue enumeration. See [second candidate search](checkpoints/2026-11-04-second-candidate-search.md). |
| Authorized artifact available through existing Hydra sources | Blocked / not established | No exact candidate is currently evidenced as an official release or explicitly authorized distribution. |
| Fresh pre-download Defender/directory/disk/baseline preparation | Not performed | Do only after a candidate is identified and before download. |
| Controlled download through Hydra | Pending | No download started. |
| Download-time process/network/filesystem differential | Pending | No controlled download experiment. |
| Artifact hash/signature/Defender/static inspection | Pending | No test artifact downloaded. |
| Isolated installation/execution behavior | Not performed | Requires separate explicit approval and isolated environment. |
| Final security verdict | Not established | Existing observations do not prove overall safety or maliciousness. |

## Security experiment gate

Do not open download links or expose download URIs during candidate discovery. A candidate must be tied to its exact official project/release or an explicitly authorized distributor, not merely share a project name or licence. Once that condition is evidenced, prepare a fresh read-only baseline and request explicit approval for the exact download-only action. Installation or execution is a separate decision requiring explicit approval and an isolated environment.

Direct download from an official publisher may be used for a separate artifact-analysis exercise, but it must not be counted as a Hydra download-path test.

## Rule

Never mark a live-browser behavior “verified” from source inspection alone.
