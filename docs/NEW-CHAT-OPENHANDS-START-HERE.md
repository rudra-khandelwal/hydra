# New Chat / OpenHands Start Here — Hydra Launcher

**Updated:** 29 October 2026  
**Workspace repository:** https://github.com/rudra-khandelwal/hydra  
**Official upstream source:** https://github.com/hydralauncher/hydra  
**Purpose:** A portable, evidence-led continuation brief for a new ChatGPT chat, OpenHands, or another coding agent.

> Read this file and the linked canonical records before acting. This file is a practical handoff and decision log, not a verbatim export of every message or hidden system instruction. The dated checkpoint preserves the detailed pre-download plan.

## 1. The user's goal

Rudra wants to understand and test the official open-source Hydra Launcher project on Windows, build/run it from source, investigate why the app shows **“No download available”** for games, and document the findings so another AI can continue without repeating solved setup work.

The work has two separate goals:

1. **Build/runtime engineering:** get the local development build working reliably and diagnose current API/catalogue/source behavior.
2. **Defensive security research:** distinguish the Hydra client, Hydra API, configured download-source metadata, third-party delivery infrastructure, downloaded files, and any later execution. Collect evidence, not assumptions.

Do not assume Hydra is safe or malicious based on its name, open-source status, a successful build, one antivirus result, or a single network observation. The repository is an independent research workspace, not an official Hydra project.

## 2. Read these existing repository records first

1. [Project memory](../docs/PROJECT-MEMORY.md) — prior environment, solved build problems, research invariants.
2. [Master memory lane](../Hydra-Memory/README.md) — compact continuation memory and launch command.
3. [Detailed 29 October handoff and pre-download checklist](../research/checkpoints/2026-10-29-hydra-chat-handoff.md) — the detailed current plan, rationale, and checklist.
4. [Project goal](../docs/PROJECT-GOAL.md) and [Project definition](../docs/PROJECT.md) — scope and success criteria.
5. [Research agenda](../research/AGENDA.md) — unfinished work.
6. [Validation matrix](../research/VALIDATION.md) — evidence and verification status.
7. [Research diary](../research/DIARY.md) and [Findings](../research/FINDINGS.md) — chronology and conclusions already supported by evidence.
8. [Repository map](../docs/REPOSITORY-MAP.md) and [Change control](../docs/CHANGE-CONTROL.md) — where things live and how to change them.
9. [Lessons log](../research/LESSONS.md) — mistakes to avoid repeating.
10. [Upstream provenance](../upstream/UPSTREAM.md) — relationship to the official project.

Use repository records and current source as the authority. Older chat recollections are context, not proof that the local checkout has not changed.

## 3. GitHub workspace review completed for this handoff

Repository reviewed: `rudra-khandelwal/hydra`, public, default branch `main`.

What was confirmed during this review:
- The README describes this as a public research/development workspace separate from `hydralauncher/hydra`.
- The repository already has project memory, goal, map, change-control, lessons, validation, diary, agenda, security checkpoints, a public `index.html` guide, and GitHub Pages workflow.
- The dated file `research/checkpoints/2026-10-29-hydra-chat-handoff.md` already contains a detailed pre-download checklist and current next-step plan.
- The memory lane and agenda already link to the 29 October handoff.
- The repository's latest commit search showed 29 October commits including “Add Hydra controlled-download investigation plan,” “Expand Hydra handoff with pre-download research and safety plan,” and “docs: place 2026-10-29 handoff in memory body.”
- The latest known dated checkpoint states that no third-party game/software download or execution test has been completed in that checkpoint. Do not claim otherwise without newer evidence.
- Open PR #1, [docs: add complete chat continuation handoff](https://github.com/rudra-khandelwal/hydra/pull/1), was returned by the PR search; inspect its current state/diff before merging or closing it. Do not assume it is merged or current merely from its title.

Important limits:
- This is a targeted repository review, not a complete audit of every file, every historical Git object, every deployed-page behavior, or the local Windows working tree.
- The handoff itself explicitly labels older scan observations as historical and says to revalidate them before acting.
- Do not report “all GitHub checked” or “full security audit completed.”
- The repository is public; everything committed, including Git history, should be treated as public.

## 4. Local Windows build/runtime state — last known, not freshly revalidated

Local application checkout recorded: `C:\Users\rudra\Downloads\hydra`.

Previously confirmed environment:
- Windows 11, build `10.0.26200.9457`
- Node.js `24.19.0`
- Yarn `1.22.22`
- Python `3.14.6`
- Rust/Cargo `1.98.1`
- VS2022 Build Tools `17.14.41`
- MSVC `14.44.35207` / compiler `19.44.35229`
- Windows SDK `10.0.26100.0`
- VS2026 Build Tools are also installed and previously caused toolchain selection/generator mismatches.

Confirmed working native build environment:
```bat
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
```

Previously successful results:
- vcpkg/CMake selected the VS2022 x64 MSVC 14.44 toolchain.
- Native target `hydra_torrent_bridge.dll` built.
- `torrent_bridge_test.exe` built.
- Test `torrent_bridge_ownership` passed; 100% of the one registered test passed.
- `yarn install` completed successfully after the toolchain and Electron problems were resolved.
- `yarn dev` launched the Vite dev server at `http://localhost:5173/`; the app displayed catalogue/API data and Steam metadata/images.

This is historical evidence, not a guarantee that the current local checkout still has the same files or is running. First inspect the local branch, commit, `git status`, installed dependencies, and current error. Do not reinstall Rust, VS2022, vcpkg, Node, or the whole project unless a new concrete error justifies it.

### Previously encountered errors and their lessons

| Error | What fixed it / lesson |
|---|---|
| `spawn cargo ENOENT` | Install/configure Rust with rustup and ensure Cargo is on PATH. |
| `python -m pip install -r requirements.txt` could not find `libtorrent` for Python 3.14 | This was an outdated route for the native torrent bridge. Do not blindly return to Python/libtorrent. The full Windows package script also includes a separate Python RPC build, so Python may still matter for that component. |
| Node-gyp rejected Visual Studio 18 / “unsupported version” | Install/use VS2022 Build Tools for the legacy node-gyp dependency. |
| Unresolved `__std_*` linker symbols | vcpkg dependencies and final project were built with mismatched MSVC toolsets (VS2026 vs VS2022). Use a consistent VS2022 x64 toolchain. |
| CMake “Could not create named generator Visual Studio 18 18” | Environment reverted to VS2026. Run from VS2022 Developer Command Prompt and set the VS2022 generator variables. |
| Electron missing or “failed to install correctly” | Repair Electron installation only if current evidence shows it is missing/broken. Electron 40.9.3 was installed during the earlier troubleshooting session, but upstream `package.json` was later reported as using `^41.10.3`; inspect current package files before changing versions. |
| `Cannot find module 'electron'` | Electron was absent after deleting its directory; re-install dependencies based on current lockfile/package.json rather than choosing a version from old notes. |
| `TypeError: Cannot read properties of undefined (reading 'includes')` at `isStaging` | Generated output had `undefined.includes("staging")`; `src/main/constants.ts` used `import.meta.env.MAIN_VITE_API_URL`. A local `.env` with that variable resolved the immediate launch issue at the time. Verify current upstream config before assuming the old endpoint remains valid. |
| “No download available” | Catalogue display and actual download-source metadata are separate. Diagnose current API/configuration, catalogue response, source metadata and source availability before downloading. This is not automatically a native-build failure. |

### Last known launch command

Open **VS2022 x64 Native Tools Command Prompt / VS2022 Developer Command Prompt**, then:

```bat
cd /d C:\Users\rudra\Downloads\hydra
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
yarn dev
```

This is a prior working launch sequence. If it fails, preserve the exact new output and investigate that failure.

### API configuration caution

The source previously referenced `MAIN_VITE_API_URL` in:
- `src/main/constants.ts`
- `src/main/services/game-executables.ts`
- `src/main/services/hydra-api.ts`
- `src/main/vite-env.d.ts`

The endpoint previously used in a local `.env` was `https://hydra-api-us-east-1.losbroxas.org`. Treat this as historical, **not automatically authoritative**. Check the current official upstream branch/tag and its env examples/build configuration before using or documenting an endpoint. Never commit a real `.env` file or credentials; use a sanitized `.env.example` if needed.

## 5. Why we are not downloading a game yet

The current unresolved issue is **“No download available.”** First determine where the flow fails. The layers are distinct:

1. Hydra client/source code
2. Native dependencies/build
3. Hydra API and catalogue
4. Download-source configuration and metadata
5. Third-party delivery servers, peers, trackers, and domains
6. The actual downloaded file
7. Installation or execution behavior

A successful build proves only that the relevant build steps completed. Catalogue artwork does not prove a source exists. A source name does not prove provenance. A successful download does not prove a file is safe. A clean antivirus scan is not a safety guarantee. Execution is a separate, higher-risk decision.

Do not use an unknown commercial-game package, crack, keygen, or random source as the first test. Prefer a small, legitimate free/open-source artifact that the user is authorized to obtain. Do not recommend random Telegram/Reddit/GitHub-fork URLs or treat a community source directory as official Hydra.

## 6. Pre-download checklist — evidence required, not a tick-box assumption

Before any controlled test download, record evidence for each applicable item. The full version with rationale is in the [dated handoff](../research/checkpoints/2026-10-29-hydra-chat-handoff.md).

### Scope and baseline
- [ ] State the research question, expected outcome, and download-only scope.
- [ ] Confirm authorization and select a lawful, legitimate free/open-source test artifact.
- [ ] Record local date/time and timezone, Hydra version/commit, build type, branch, and `git status`.
- [ ] Record relevant Hydra processes and baseline network connections.
- [ ] Record the target download folder's baseline state and free disk space.
- [ ] Confirm Windows Defender/antivirus is enabled; never disable it to make the test work.

### Build and API/source diagnostics
- [ ] Inspect current local source and exact checkout before changing files.
- [ ] Confirm the app starts and capture current startup errors.
- [ ] Verify `MAIN_VITE_API_URL` against current official source/configuration.
- [ ] Check API request status codes and sanitized response metadata.
- [ ] Check whether the selected catalogue entry returns executable/source metadata.
- [ ] Identify the exact configured source, its origin, maintainers, domain, documentation, and any relevant security reports.
- [ ] Distinguish source display names from verified provenance.
- [ ] If the source's provenance or destination is unclear, stop and choose another test.

### Monitoring and download-only test
- [ ] Use a dedicated test directory.
- [ ] Record baseline process/network/filesystem observations.
- [ ] Plan to observe Hydra and child processes, DNS/HTTPS destinations, and new/modified files.
- [ ] Avoid Administrator privileges unless specifically justified.
- [ ] Do not grant unnecessary firewall access; do not enable Public-network access without a demonstrated need.
- [ ] Record exact test start/end time and relevant deltas.
- [ ] Record file names, sizes, timestamps, types, and SHA-256 hashes.
- [ ] Preserve the original downloaded artifact unchanged.
- [ ] Do not open or execute the artifact yet.

### Artifact review and execution gate
- [ ] Identify the actual file type independently of its extension.
- [ ] Compute and record SHA-256.
- [ ] Inspect signature/publisher where applicable.
- [ ] Scan with Defender/installed antivirus and record results with limitations.
- [ ] Perform appropriate static inspection and correlate with source, URL and observed activity.
- [ ] If suspicious or provenance cannot be established, do not execute.
- [ ] Installation/execution requires a separate explicit user decision after reviewing the download evidence.
- [ ] If justified, use a disposable VM/Windows Sandbox with a snapshot, no sensitive accounts/files, and process/network/filesystem/registry/persistence monitoring.

### Publish safely
- [ ] Write a dated checkpoint separating fact, observation, hypothesis, finding, and next action.
- [ ] Update diary, findings, validation matrix, agenda, and memory as appropriate.
- [ ] Redact tokens, passwords, cookies, auth headers, personal data and signed URLs.
- [ ] Never commit secrets, proprietary downloaded game files, or raw sensitive logs.
- [ ] Do not claim a malware verdict unless evidence supports it.

## 7. Immediate work order

1. Read the project memory and the dated handoff.
2. Inspect the **current** local checkout, branch, commit and Git status.
3. Launch with the preserved VS2022 command; do not reinstall solved tools.
4. Inspect current official source for API/env configuration.
5. Test API/catalogue behavior without downloading anything.
6. Classify “No download available” as a configuration/API, catalogue, source-metadata or source-availability issue.
7. Choose an authorized free/open-source test artifact.
8. Complete the pre-download checklist and record baseline evidence.
9. Run a **download-only** experiment, capture deltas, hash and inspect the file.
10. Stop before executing anything; ask the user to review evidence and make a separate decision.
11. Update research docs with sanitized results and uncertainty.

## 8. Copy/paste prompt for the next AI or OpenHands

```text
Continue the Hydra Launcher research project in https://github.com/rudra-khandelwal/hydra.

Before doing anything, read:
- docs/NEW-CHAT-OPENHANDS-START-HERE.md
- docs/PROJECT-MEMORY.md
- Hydra-Memory/README.md
- research/checkpoints/2026-10-29-hydra-chat-handoff.md
- research/AGENDA.md
- research/VALIDATION.md
- research/DIARY.md
- research/FINDINGS.md
- docs/CHANGE-CONTROL.md
- research/LESSONS.md

Inspect current GitHub state and the current local checkout before changing anything. Report the branch, commit, working-tree state, relevant open PRs, and which observations are historical versus freshly verified. Do not repeat setup steps that are already confirmed working without a new error.

The local checkout previously used C:\Users\rudra\Downloads\hydra. A successful native build used VS2022 Build Tools/MSVC v143 and these variables:
CMAKE_GENERATOR=Visual Studio 17 2022
CMAKE_GENERATOR_PLATFORM=x64
VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
VCPKG_PLATFORM_TOOLSET=v143

The app previously launched with yarn dev and loaded catalogue data, but showed “No download available” for every game. Diagnose the current API/env/catalogue/source metadata path before downloading anything. Verify MAIN_VITE_API_URL against current official source/configuration; do not blindly reuse a historical endpoint.

Do not download a game yet. First use evidence to isolate the cause. If a controlled download is justified, choose a legitimate free/open-source artifact the user is authorized to obtain, complete the documented pre-download checklist, and keep the first test download-only. Record process/network/filesystem changes, file metadata, SHA-256 and antivirus/static-inspection results. Do not execute installers/binaries without a separate explicit user decision and a containment plan.

Keep facts separate from hypotheses; do not declare Hydra or an artifact safe/malicious without sufficient evidence. Do not use pirated games, cracks, keygens, random community URLs, or unknown executables as test material. Do not disable Defender. Do not commit credentials, raw sensitive logs, signed URLs, or copyrighted game files. After each material finding, update the dated checkpoint, diary, findings, validation, agenda and project memory as appropriate. Follow docs/CHANGE-CONTROL.md.
```

## 9. Public repository hygiene

This repository is public. Treat all committed content and history as public. Never commit:
- passwords, API keys, tokens, cookies, private keys, recovery codes, or auth headers
- raw logs containing credentials or unnecessary personal data
- proprietary/copyrighted game or software files
- unredacted signed download URLs or tracker/magnet metadata that is unnecessary to the finding

## 10. Accuracy note

This file is a handoff summary, not a literal transcript of every chat message. It preserves the user's objective, known build history, solved errors, unresolved issue, repository links, safety requirements, and next actions. If a claim is not backed by current evidence, label it historical or unverified instead of filling gaps with guesses.
