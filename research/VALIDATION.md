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


## Official-publisher artifact-analysis preparation — 4 November 2026

| Check | Status | Evidence/limitation |
|---|---|---|
| Separate official-publisher candidate review | Documented; evidence inherited from supplied report | PuTTY 0.85, 7-Zip 26.05, and Notepad++ 8.9.8.1 recorded with unresolved fields. |
| Provisional candidate recommendation | PuTTY 0.85 (not approved) | Reported MIT licence and official GPG/Authenticode guidance; exact package size and package-specific signer/verification evidence still need confirmation. |
| 7-Zip 26.05 | Candidate; not approved | Reported 1.6 MB x64 EXE and mixed LGPL/BSD/unRAR terms; exact installer signature/checksum not verified. |
| Notepad++ 8.9.8.1 | Lead only; not approved | Reported Windows packages and SHA-256 metadata; release date/current stable status, size, and signature/publisher details unconfirmed. |
| Fresh Windows/Defender/download-directory/disk/process/network baseline | Not performed | Perform only after a specific artifact is selected and before an explicitly approved download. |
| Official-publisher artifact download | Not performed | Requires explicit approval for the exact package and URL. |
| Hash/signature/Defender/static inspection | Not performed | No artifact downloaded. |
| Hydra download-path experiment | Still blocked | No existing Hydra entry has been verified as an official or explicitly authorized distribution. |
| Install/execute analysis | Not performed | Separate explicit approval and isolated environment required. |

Direct-from-official-publisher analysis is a distinct experiment. It cannot be counted as evidence about Hydra's downloader or configured third-party sources. See [official-publisher candidate checkpoint](checkpoints/2026-11-04-official-publisher-static-analysis-candidates.md).


## Official-publisher artifact analysis — PuTTY 0.85 (4 November 2026)

| Check | Status | Evidence/limitation |
|---|---|---|
| Explicit download-only approval | Complete | User approved only the official 64-bit x86 standalone putty.exe; no install/execute approval. |
| Artifact identity and size | Reported and recorded | putty.exe, PuTTY 0.85, 1,706,136 bytes. |
| SHA-256 against official manifest | Match | d01fdb5aae8f112526040a39b0bfb9e27d813003178645e65f8d1cfdb2a26c87 matched w64/putty.exe. |
| Authenticode | Valid | Windows reported signer Simon Tatham. |
| Executable GPG signature | Good signature | PuTTY Releases key fingerprint 1A07 DAC0 F220 CF12 248E A719 5C67 D0F8 8BC3 E5B5; local GPG trust not certified. |
| sha256sums.gpg manifest signature | Good signature | Original 17,124-byte file is clear-signed PGP, not detached; verified with correct GPG method. Key trust limitation remains. |
| Windows Defender command-line scan | No threats found | Defender status cmdlet could not load; real-time protection state not independently confirmed. |
| PE static inspection | Blocked / incomplete | objdump, strings, dumpbin, llvm-readobj, sigcheck unavailable; Python inaccessible; no tool installed. No verified PE structure/import/string/dependency/packing findings. |
| Installation / execution | Not performed | Download-only approval did not authorize running or installing PuTTY. |
| Hydra app checkout/settings/sources | Untouched | No changes made. |
| Hydra download-path experiment | Still blocked | PuTTY is a direct official-publisher artifact, not an artifact obtained through Hydra. No existing Hydra source entry has verified authorization. |

See [PuTTY artifact-analysis handoff](checkpoints/2026-11-04-putty-static-analysis-handoff.md).


## PuTTY 0.85 expanded static analysis — 4 November 2026

| Check | Status | Evidence/limitation |
|---|---|---|
| PE headers/sections/imports/exports | Completed (reported) | Existing Visual Studio dumpbin; all three options exit code 0; x64 Windows GUI PE; no exports listed. |
| Printable ASCII/UTF-16LE strings | Completed (reported) | 10,241 ASCII and 1,045 UTF-16LE strings; reviewed endpoint/API indicators had plausible context; no clearly malicious string identified. |
| Section entropy | Completed (reported) | `.rsrc` 7.8331 bits/byte; entropy is not proof of packing. |
| PE resource directory | Completed (reported) | 24 resource leaves, no malformed/out-of-bounds branches reported; version and manifest identified. |
| Embedded HTML Help directory metadata | Completed (reported) | ITSF v3/ITSP v1; 561 PMGL entries, five PMGL chunks and one PMGI chunk; nine section-0 entries and 552 LZX section-1 entries. No content decompression or extraction. |
| Embedded help content/default topic | Not inspected | No internal files or #SYSTEM contents read; `/index.html` is filename-only candidate. |
| Runtime behavior/network activity | Not performed | PuTTY was never loaded, launched, installed, or executed. |
| Artifact integrity | Unchanged (reported) | 1,706,136 bytes; SHA-256 d01fdb5aae8e112526040a39b0bfb9e27d813003178645e65f8d1cfdb2a26c87. |
| Overall safety verdict | Not established | No clearly malicious indicator in inspected static evidence is not proof of safety. |
| Hydra download-path experiment | Still blocked | PuTTY came directly from official publisher, not through Hydra; authorization/provenance of an existing configured source entry remains unverified. |

See the [PuTTY embedded-help metadata checkpoint](https://github.com/rudra-khandelwal/hydra/blob/main/research/checkpoints/2026-11-04-putty-embedded-help-metadata.md).
