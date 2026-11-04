# 4 November 2026 — Hydra Download-Source Investigation Handoff

**Prepared:** 4 November 2026 (Asia/Calcutta)  
**Documentation repository:** `rudra-khandelwal/hydra` (`main`)  
**Application checkout:** `C:\Users\rudra\Downloads\hydra`  
**App branch/HEAD reported:** `main` / `fdbc5272720f96a634428ea47e33143fe4d4d393`  
**Scope:** durable handoff and evidence-based investigation plan; no app changes, download, install, or execution.

## Read first

1. [Current project state](../../docs/CURRENT-STATE.md)
2. [AI quickstart](../../docs/AI-AGENT-QUICKSTART.md)
3. [Master memory](../../Hydra-Memory/README.md)
4. [Project memory](../../docs/PROJECT-MEMORY.md)
5. [Research agenda](../AGENDA.md), [findings](../FINDINGS.md), and [validation matrix](../VALIDATION.md)
6. [Handoff cadence](../../docs/HANDOFF-CADENCE.md)

## Project history in brief

- **21 September:** process/network baseline and trust-boundary methodology began.
- **22 September:** public research repository and Pages guide/workflow were established. The first Pages run failed because Pages was not enabled; a later run succeeded after configuration.
- **25 September:** source/API metadata and client synchronization were documented; AMSI blocked a test string at script-content stage, not a completed file-quarantine test. No broad security verdict was made. Guide, memory, security, and validation records were expanded.
- **29 October:** the earlier handoff preserved native build results, Windows toolchain setup, and a safety checklist for controlled artifact testing.
- **31 October:** AI quickstart was added and linked; workflow run #132 succeeded for documentation commit `30a74b7`.
- **4 November:** screenshot-driven source-coverage investigation below. Existing chronology remains in the linked diary and checkpoints; this summary does not replace it.

## Exact current state

### Application checkout

- The observed local directory is `C:\Users\rudra\Downloads\hydra`; it is distinct from the public docs repo and official upstream.
- The local checkout reports branch `main`, HEAD `fdbc5272720f96a634428ea47e33143fe4d4d393`, release v4.1.4.
- User reports pre-existing changes in `package.json`, `yarn.lock`, and untracked `security-research/`. The directory exists. Git status failed (“this operation must be run in a work tree”), so do not claim independent status confirmation. Preserve these changes and all other checkout contents.
- Do not switch branches, reset, clean, stash, overwrite, commit, or modify the app checkout. Do not merge, release, or tag.

### Environment and launch

The previously documented launch command is:

~~~bat
cd /d C:\Users\rudra\Downloads\hydra
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
yarn dev
~~~

Run it in the VS2022 x64 Developer Command Prompt. This sequence was not rerun for this handoff. Older Node/Yarn/Rust/VS versions and successful build/test evidence are in the master memory and 29 October checkpoint; they are historical until checked again. Do not reinstall tools without evidence.

### Screenshot evidence (user-provided; observed in the conversation attachment)

- Settings showed onlinefix with **2,784 options**, FitGirl with **7,127 options**, and both **Up to date**.
- *Granny: Escape Together* appeared as one result with the onlinefix filter.
- *Granny Remake* details showed one download option, dated 24/07/2023.
- Original *Granny* (DVloper, release 20 Nov 2018) showed **No downloads available**.
- Geometry Dash details showed **No downloads available**. Its filtered catalogue showed **0 results** for onlinefix and **0 results** for FitGirl.
- These are separate game entries. The screenshots do not include raw API payloads or request status. Counts are source options, not complete game coverage.

Screenshots are not copied into the public repository. The observations above are the sanitized record.

## Code and API facts inspected locally

- Local `.env` value observed: `MAIN_VITE_API_URL=https://hydra-api-us-east-1.losbroxas.org` (no trailing slash). `.env.example` has an empty value. Keep local env files and credentials private.
- The app reads `MAIN_VITE_API_URL`; relevant files include `src/main/constants.ts`, `src/main/services/hydra-api.ts`, and `src/main/services/game-executables.ts`.
- Main game details request: `GET /games/{shop}/{objectId}/download-sources`, with paging `take=100`, `skip=0`, and configured source IDs.
- Big Picture uses the same endpoint in `src/big-picture/src/hooks/queries/use-game-download-options.hook.ts`.
- `filterDownloadableRepacks` in `src/shared/index.ts` retains a repack only if some URI matches a supported downloader: recognized HTTPS host prefixes or `magnet:`.
- Big Picture catches request errors and assigns the same `no-download-options` category used for an empty/unsupported response. This reduces diagnostic detail in the UI.
- No game-specific request or API response was captured. No evidence yet shows that a returned valid source record was incorrectly rejected.

## Finding status and decisions

**Finding:** the two configured sources do not show every tested game; the screenshots support coverage limitations for original Granny and Geometry Dash. **Unproven:** a URI matching/filter defect. Do not diagnose a code bug from 0 source-filter results or an empty-state label. Do not add untrusted source URLs. Do not download or execute a game as part of the next diagnostic step.

## Safe next action

Perform a read-only comparison using one exact game/source entry that the UI lists and one exact game it does not. Record the actual `shop` and `objectId`; do not guess them. Capture, locally and safely sanitized:

- request endpoint and HTTP status;
- response type and number of returned records;
- whether configured source IDs are present in request/response metadata;
- for each URI, only scheme and recognized-host category (omit full path, query, signed URL, and credentials);
- count before and after `filterDownloadableRepacks`;
- whether request failed, response was empty, or nonempty records were filtered out.

If a record is returned with an otherwise valid URI and gets filtered out, preserve a minimal sanitized fixture and investigate a targeted regression test. If response is empty, record a source/API coverage limitation. If request fails, record the status/error separately from source absence. Do not make app edits until the evidence supports a defect and the user approves the change.

## Handoff counter

**User-message count since this handoff: 0/5.** Follow [HANDOFF-CADENCE.md](../../docs/HANDOFF-CADENCE.md). Update the current state and dated checkpoint at the fifth project-related user message, and sooner for meaningful state changes or before pausing. This is a documented manual checkpoint; no reliable automatic cross-chat counter or background GitHub updater has been configured.
