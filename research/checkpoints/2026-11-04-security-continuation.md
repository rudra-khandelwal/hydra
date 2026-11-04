# 2026-11-04 — Security Research Continuation: Controlled Download Blocker

**Purpose:** Preserve the user's latest Codex/report handoff and keep the security investigation focused on the actual unfinished experiment. This is a documentation-only checkpoint. No app, source, or system changes were made as part of recording this report.

## Project objective

Determine, with reproducible evidence, whether Hydra Launcher, its configured download sources, the download path, and content downloaded through Hydra can introduce malicious or harmful behaviour into Windows. Areas of concern include malware, spyware, credential theft, backdoors, persistence, unauthorized network activity, unexpected system/registry changes, and unwanted payloads.

The investigation must distinguish Hydra itself, Hydra's API, community source metadata, third-party download infrastructure, the downloaded artifact, its installer/runtime, bundled dependencies, and Windows behavior. A clean source URL check or antivirus scan alone is not a safety verdict.

## Existing security work — retain; do not repeat without a specific evidence gap

The existing repository records report these earlier checks:
- Windows runtime baseline collection for processes, established network connections, and repository files.
- Observation of Hydra/Electron processes and correlation with established HTTPS connections.
- Download-source synchronization and API metadata correlation, including source IDs/names and a returned download record.
- Architectural trust-boundary review separating Hydra client, API, community source records, and eventual third-party infrastructure.
- Read-only inspection of client code paths for source storage, synchronization, game-specific source requests, and URI filtering.
- Antivirus/AMSI control observation: the EICAR test string was blocked while being assigned in PowerShell.

**EICAR limitation:** a valid EICAR test file and a Defender quarantine event were not established. The previous work must not be described as a completed EICAR-file quarantine test.

Historical evidence: [Findings](../FINDINGS.md), [Validation Matrix](../VALIDATION.md), and [25 September security checkpoint](2026-09-25-security-research.md).

These earlier checks are not a comprehensive audit of every Windows persistence mechanism, every outbound connection, every file-access path, or every component. Preserve their recorded scope and limitations.

## Diversion into catalogue/source availability

Subsequent work concentrated on missing download options and catalogue/source matching:
- Hydra v4.1.4 catalogue screenshots and source counts were examined.
- Read-only code tracing covered the game-specific API request, IPC/preload/main-process path, and URI filtering.
- A Geometry Dash request returned HTTP 200 with an empty array; Schedule I returned 16 onlinefix records with magnet-scheme URIs.
- Public upstream FAQ material described title-based matching rather than exact game identity matching.
- Exact configured onlinefix and FitGirl JSON URLs were requested directly and both returned HTTP 403; no payload was parsed and no alternate host or bypass was attempted.
- The user's latest report says OpenTTD showed “No downloads available” in Hydra 4.1.4.

These are catalogue/source observations. They do not establish maliciousness or safety of Hydra or any downloaded artifact. The source/catalogue investigation should not displace the security objective unless it directly blocks a suitable controlled test.

## Latest artifact-selection result

The user's latest report states:
- OpenTTD was checked in Hydra v4.1.4 and showed “No downloads available.”
- The configured sources currently appear as OnlineFix and FitGirl.
- No specific artifact with verifiable official provenance and clear download permission has been identified within those existing sources.
- No download was started.
- Defender state, download directory, free disk space, and fresh machine baseline were not checked during this selection pass.

**Current blocker:** No suitable, clearly authorized test artifact has been established through the existing Hydra configuration.

Do not infer that no eligible artifact exists in the sources; only that none has yet been identified and verified. Do not assume any particular OnlineFix/FitGirl entry is authorized or appropriate.

## Main unfinished experiment

The next substantive experiment is a **download-only controlled test through Hydra**, using one specifically identified artifact whose publisher/provenance and permission to download are independently clear.

### Gate 1 — Identify and verify the exact artifact
- Check the existing Hydra catalogue and configured sources without changing them.
- Identify a specific candidate and its exact game/software identity.
- Independently verify the official publisher/project, its licensing/download terms, and whether the source entry actually points to an authorized distribution.
- Prefer a small free/open-source artifact whose publisher clearly authorizes the distribution route.
- If no suitable artifact exists in the currently configured sources, stop and report that Hydra-path testing is blocked. Do not substitute a direct official download and claim it tests Hydra.

### Gate 2 — Prepare a baseline (after a candidate is identified, before download)
- Record date/time, Hydra version/build, and app checkout branch/HEAD/status.
- Preserve all existing app checkout modifications; do not reset, clean, stash, overwrite, branch-switch, commit, or otherwise modify the app checkout.
- Check and record Windows Defender real-time protection/status without disabling it.
- Record configured download location, free space, and its pre-test contents.
- Capture a bounded baseline of relevant processes/process tree, network connections/DNS activity, and filesystem state.
- Use least privilege; do not run Hydra or a downloader as Administrator without a separately justified need.
- Do not change sources, application settings, or firewall permissions.

### Gate 3 — Download-only experiment
Only after the user approves the named artifact and plan:
- Download through the existing Hydra configuration.
- Record the start/end time and Hydra/downloader process tree.
- Capture relevant network destinations and filesystem changes, distinguishing expected from unexplained activity.
- Record resulting file names, sizes, timestamps, SHA-256 hashes, signatures/publishers where available, and file types.
- Scan with Defender and available security tools; preserve exact result and timestamp.
- Perform static inspection appropriate to the artifact type and dependencies.
- Keep the file unexecuted. Do not install, open, or launch it.

### Gate 4 — Report before execution
Report the download-stage observations, evidence, attribution, uncertainties, and limitations. A separate explicit decision is required before installing or executing anything. If later approved, use an isolated disposable Windows Sandbox/VM with a snapshot and no sensitive accounts or data, then monitor child processes, persistence locations, filesystem/registry changes, outbound network activity, and security alerts.

## Direct download vs Hydra download

A direct download from an official publisher can support a separate artifact provenance/static-analysis exercise, but it does **not** test Hydra's download path. Keep these experiment types clearly labeled and do not conflate their results.

## Secondary settings research — lower priority

Review without changing settings:
1. Settings → Integrations → Steam: permissions, token handling, and data shared.
2. Settings → Integrations → RetroAchievements: account/API credential handling, storage, and data shared.
3. Settings → Compatibility → Common Redistributables: identify components, publishers, download locations, signatures, and expected system changes.
4. Account & Privacy → Hydra Cloud: data uploaded/stored, access controls, encryption claims, and third-party sharing.
5. Hydra Cloud Gifts: implications of “Allow other users to gift to me Hydra Cloud,” including what other users can see and what disabling it changes. Do not toggle the setting.

## Non-negotiable preservation and safety constraints

- Do not modify Hydra application source code or dependencies.
- Do not change application settings or configured sources.
- Do not add, remove, replace, or bypass configured sources.
- Do not download, install, or execute any artifact until the exact candidate and plan are presented and approved.
- Do not disable Defender or other protections.
- Do not expose .env contents, tokens, passwords, cookies, authorization headers, complete signed URLs, or personal data.
- Do not publish copyrighted game files or raw sensitive logs.
- Do not declare Hydra or its sources safe based on absence of detections in limited checks.
- Record facts separately from interpretation and hypotheses.

## Current status and next action

**Completed earlier:** runtime baseline, Hydra/Electron process and HTTPS observations, source/API metadata correlation, trust-boundary review, client-code inspection, and EICAR/AMSI interception observation (with the limitation above).

**Not yet completed:** an authorized controlled Hydra download, downloaded-artifact hash/signature/AV/static examination, download-time process/network/filesystem differential, and any separately approved isolated execution test.

**Next action:** identify one exact, clearly authorized free/open-source artifact actually available through the existing Hydra configuration. Do not begin downloading or change any settings/sources while this remains unresolved.

**Latest report:** OpenTTD was unavailable; no alternative was established; no download or system preparation checks were performed in that pass.
