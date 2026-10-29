# 2026-10-29 — Hydra Chat Handoff, Research Plan, and Pre-Download Checklist

**Date:** 29 October 2026  
**Purpose:** Provide a self-contained handoff so a new ChatGPT chat, OpenHands, or another maintainer can understand the project, why it exists, what has been completed, what remains, and what must happen before any game download is attempted.

## 1. Project identity and objective

- Research/workspace repository: https://github.com/rudra-khandelwal/hydra
- Official Hydra source repository: https://github.com/hydralauncher/hydra
- Local Hydra application checkout recorded in prior work: `C:\Users\rudra\Downloads\hydra`
- The GitHub repository `rudra-khandelwal/hydra` is a **public documentation/research workspace**, not the Hydra application source tree.
- Overall objective: understand Hydra's build/runtime behavior and assess the application/API/download-source/content trust boundaries using repeatable, evidence-based tests. Do not declare something safe or malicious without evidence.
- The next practical goal is to resolve the “No download available” issue and perform a controlled, low-risk download experiment only after the prerequisites and safety checks below are satisfied.

## 2. What we are trying to answer — and why

We need to keep the following layers separate because a failure or risk at one layer does not prove the same thing about another:

1. **Hydra application/source code:** What the client does, which APIs it calls, how it handles source metadata, and how it launches/installs content.
2. **Build and native dependencies:** Whether the locally built app and native torrent bridge compile and pass their tests.
3. **Hydra API/catalogue:** Whether the client reaches the expected API endpoint and receives catalogue/executable/source metadata.
4. **Download-source configuration/metadata:** Which source is configured, where the metadata came from, and whether it is reachable and trustworthy.
5. **Network/content delivery:** Which domains, processes, peers, trackers, or servers are contacted during a test.
6. **Downloaded artifact:** What exact file was obtained, its hash/type/signature, and whether static inspection/Defender checks reveal anything concerning.
7. **Installation/execution:** What the installer or executable does when run. This is a separate, higher-risk step and must not be inferred from a successful download.

**Why this separation matters:** “No download available” may be caused by API configuration, catalogue responses, source configuration, or source availability; it does not automatically mean the native build is broken. Likewise, a source listing or network connection does not prove that a downloaded executable is safe or malicious.

## 3. Last known build/runtime state (historical; not re-run for this checkpoint)

The prior project memory records:
- Windows 11 build 10.0.26200.9457.
- Node.js 24.19.0; Yarn 1.22.22.
- Rust: rustc 1.98.1 and cargo 1.98.1, host `x86_64-pc-windows-msvc`.
- VS2022 Build Tools at `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools`, version 17.14.41, MSVC 14.44.35207, Windows SDK 10.0.26100.0.
- VS2026 Build Tools are also installed and previously caused toolchain-selection/generator issues. The confirmed native setup used VS2022.
- The Rust/CMake/vcpkg native build succeeded using VS2022 x64.
- Build outputs included `hydra-native/hydra-native.node`, `hydra_torrent_bridge.dll`, and `torrent_bridge_test.exe`.
- The `torrent_bridge_ownership` test passed (100% of one test).
- Hydra had been launched previously.
- The unresolved runtime issue was **“No download available.”**

These are prior confirmed observations, not proof that the current local checkout is unchanged or the application is running right now. Inspect the current local state before altering it. Do not reinstall the toolchain or entire project without a new error that justifies it.

## 4. Exact launch prompt supplied by the user

Run in a **VS2022 Developer Command Prompt** (or a terminal where the VS2022 toolchain is properly initialized):

```bat
cd /d C:\Users\rudra\Downloads\hydra
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
yarn dev
```

This is the preserved development-launch command. It was not re-run as part of creating this handoff. If `yarn dev` fails, capture the full error and diagnose that error rather than repeating installation steps blindly.

## 5. API/catalogue investigation already identified

Earlier source inspection found `MAIN_VITE_API_URL` referenced in:
- `src/main/constants.ts`
- `src/main/services/game-executables.ts`
- `src/main/services/hydra-api.ts`
- `src/main/vite-env.d.ts`

An earlier generated output contained:

```js
const isStaging = undefined.includes("staging");
```

That was evidence that `MAIN_VITE_API_URL` was undefined in that particular generated output and could break API-related behavior. A previous configuration used `https://hydra-api-us-east-1.losbroxas.org`, but that endpoint must be verified against current official source/configuration before use; do not assume it remains correct and do not invent endpoints.

## 6. Required pre-download checklist — do not skip

The following checklist must be completed before starting a game download for research. It is intended to reduce risk and make the result reproducible. A checked item means there is evidence recorded, not merely that someone believes it is done.

### A. Confirm the test scope and authorization
- [ ] State the research question and expected result.
- [ ] Use only content the user is authorized to access and download. Prefer a legitimate, free/open-source test artifact for the first controlled experiment rather than an unknown commercial game installer.
- [ ] Decide whether this experiment is download-only or includes installation/execution. Default to **download-only**.
- [ ] Do not use pirated content or untrusted cracks/keygens as a test sample.

**Why:** Keeps the test lawful, bounded, and focused; download and execution have different risk profiles.

### B. Establish a clean baseline
- [ ] Record date/time and local timezone.
- [ ] Record current Hydra version/source commit and whether it is a local dev build or official release.
- [ ] Record the current Git working-tree state and relevant config filenames (redact secrets).
- [ ] Record the current process list relevant to Hydra and baseline network connections.
- [ ] Record baseline filesystem state for the intended download directory.
- [ ] Confirm sufficient free disk space.
- [ ] Confirm Windows Defender/antivirus is enabled and record its current status; do not disable protection to make a test work.

**Why:** A before/after comparison helps attribute changes to the test rather than pre-existing activity.

### C. Verify build and launch health
- [ ] Confirm the current source checkout matches the intended branch/commit.
- [ ] Confirm the VS2022 x64 environment and required variables if building native code.
- [ ] If rebuilding is necessary, capture build output and test results.
- [ ] Confirm Hydra starts and record any startup/API errors.
- [ ] Do not treat old successful build logs as proof the current checkout is healthy.

**Why:** Prevents confusing a build failure with an API, catalogue, or download-source issue.

### D. Verify API/catalogue behavior
- [ ] Inspect the current official source for the expected `MAIN_VITE_API_URL` and how it is injected into dev/build.
- [ ] Verify the endpoint from current trusted project source/docs, not from an unverified chat snippet.
- [ ] Check whether API requests succeed and record status codes and sanitized response metadata.
- [ ] Check whether the catalogue returns a result for the selected test artifact.
- [ ] Check whether executable/source metadata is present and how Hydra selects/uses it.
- [ ] Redact authorization headers, cookies, tokens, personal data, and signed URLs before committing logs.

**Why:** “No download available” may arise before any download begins. This step helps isolate API/configuration from source availability.

### E. Verify and assess the source
- [ ] Identify the exact configured source and its origin (official project, community provider, or unknown third party).
- [ ] Review the source's repository/domain, maintainer, recent activity, documentation, and relevant security reports.
- [ ] Inspect source metadata and the relevant client code path; do not equate a display name with verified provenance.
- [ ] Verify the destination domain(s) and HTTPS behavior where applicable.
- [ ] Do not add random URLs, run source-provided scripts, or trust a source solely because Hydra lists it.
- [ ] Record uncertainty explicitly; if provenance is unclear, stop and choose a safer test artifact/source.

**Why:** Hydra, its API, source metadata, and the host serving content are distinct trust boundaries.

### F. Prepare monitoring and containment
- [ ] Use a dedicated test directory with a clear name.
- [ ] Record baseline process/network/filesystem observations before starting.
- [ ] Plan to monitor Hydra and child processes, DNS/HTTPS endpoints, new files, and file writes during the test.
- [ ] Do not grant unnecessary Windows Firewall permissions; do not enable Public-network access without a demonstrated need.
- [ ] Do not run as Administrator unless a specific, justified test requires it.
- [ ] Keep downloaded files unopened and unexecuted until inspection is complete.

**Why:** This helps determine what actually occurred and avoids giving a test process unnecessary privileges.

### G. Download-only procedure
- [ ] Start the test and record exact start/end time.
- [ ] Capture relevant process/network/filesystem changes during the download.
- [ ] Save logs in a sanitized form.
- [ ] Record exact file names, sizes, timestamps, and SHA-256 hashes.
- [ ] Preserve the original file unchanged for analysis.
- [ ] Do not execute installers, scripts, cracks, keygens, or unknown binaries as part of the initial test.

**Why:** Hashes and before/after observations make the experiment repeatable and support later comparison.

### H. Inspect the artifact before any execution
- [ ] Identify file type independently of its extension.
- [ ] Compute SHA-256 and record it.
- [ ] Inspect digital signature and publisher if the file format supports signing.
- [ ] Scan with Windows Defender/installed antivirus and record the result without treating one clean scan as proof of safety.
- [ ] Perform static inspection appropriate to the file type.
- [ ] Correlate findings with the source, download URL, and observed process/network activity.
- [ ] If suspicious, quarantined, unsigned in an unexpected context, or provenance cannot be established, do not execute it.

**Why:** Download success only proves data was received. It does not establish integrity, provenance, or safe behavior.

### I. Installation/execution gate (separate explicit decision)
- [ ] Do not proceed unless the user explicitly agrees after reviewing download-stage evidence.
- [ ] Prefer a disposable Windows Sandbox/VM with snapshots and no sensitive accounts/files.
- [ ] Record the clean VM baseline and revert afterward.
- [ ] Monitor child processes, persistence locations, filesystem writes, registry changes, outbound network activity, and security alerts.
- [ ] Stop and preserve evidence if unexpected behavior occurs.

**Why:** Running a downloaded executable is substantially riskier than downloading and hashing it. A VM reduces but does not eliminate risk.

### J. Publish evidence safely
- [ ] Create a dated checkpoint with hypothesis, setup, steps, results, hashes, and limitations.
- [ ] Separate observed facts from interpretation and speculation.
- [ ] Redact credentials, cookies, authorization headers, personal paths where unnecessary, private data, and signed download URLs.
- [ ] Never commit API keys, tokens, passwords, private keys, cookies, recovery codes, or proprietary downloaded game files.
- [ ] Update `research/DIARY.md`, `research/FINDINGS.md`, `research/VALIDATION.md`, and `research/AGENDA.md` where appropriate.
- [ ] Update this handoff/memory after material decisions or confirmed results.

**Why:** The public repository must preserve useful evidence without exposing secrets or making unsupported security claims.

## 7. Recommended order of work from this checkpoint

1. Read `Hydra-Memory/README.md`, `docs/PROJECT-MEMORY.md`, `research/VALIDATION.md`, `research/AGENDA.md`, and this handoff.
2. Inspect the current local checkout and Git status; do not assume old logs match current source.
3. Launch Hydra with the exact command above and capture any current error.
4. Resolve `MAIN_VITE_API_URL` using current official source/configuration.
5. Test API/catalogue behavior without downloading anything.
6. Identify why “No download available” occurs and classify the cause (API config, catalogue response, source metadata, or source availability).
7. Choose a lawful, legitimate free/open-source test artifact.
8. Complete checklist sections A–F before downloading.
9. Conduct a download-only experiment, then hash and inspect the artifact (G–H).
10. Only consider execution after a separate explicit decision and the containment plan (I).
11. Publish sanitized evidence and update the research records (J).

## 8. Repository review findings from the earlier scan (revalidate before acting)

The earlier scan of the public research workspace reported:
- No obvious malicious payload, embedded credential, suspicious executable, or third-party JavaScript dependency in the reviewed current tree.
- No complete scan of every historical Git object; historical secret exposure was not ruled out.
- No direct live-browser exercise of the deployed guide.
- Guide instructions mentioning Electron 40.9.3 were stale relative to the checked upstream `package.json` using Electron `^41.10.3`.
- `Hydra-Memory/README.md` and `docs/PROJECT-MEMORY.md` both claimed canonical-memory status, creating ambiguity.
- Research notes claimed live GitHub data fetching, but inspected `index.html` had no `fetch()`/XHR implementation.
- `research/LESSONS.md` was reported to contain duplicate `L-019` numbering.
- Open PR #1, “docs: add complete chat continuation handoff,” was reported to contain older Electron/build assumptions.
- `main` was unprotected and the Pages workflow published the repository root; SHA-pinning Actions was suggested as a hardening measure.

These are earlier scan observations, not a fresh scan performed while preparing this document. Confirm current repository state before taking action.

## 9. Operating rules for future ChatGPT/OpenHands sessions

- Read this file and the canonical memory before acting.
- Inspect current source, current local state, and relevant current evidence first.
- Do not reinstall tools or the whole project without evidence of a specific failure.
- Do not change API endpoints or add download sources based on guesswork.
- Do not declare the application or downloaded content safe/malicious based on a single signal.
- Do not download or execute an unknown game artifact merely to test whether Hydra works.
- Keep download and execution as separate decisions.
- Ask the user before moving from a download-only test to running an installer/executable.
- When uncertain, state exactly what is known, what is inferred, and what remains unverified.
- Record new confirmed outcomes in dated checkpoint(s) and update the memory, diary, agenda, findings, and validation matrix as appropriate.

## 10. Immediate next action

**Do not download a game yet.** First launch the local development build, verify the current API endpoint/configuration and catalogue responses, and explain the “No download available” result. Once that path is understood, use a legitimate free/open-source test artifact and follow the checklist above.

End of handoff.
