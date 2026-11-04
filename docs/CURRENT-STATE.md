# Hydra Project Current State

**Reviewed:** 4 November 2026 (Asia/Calcutta)  
**Documentation repository:** [rudra-khandelwal/hydra](https://github.com/rudra-khandelwal/hydra), public, default branch `main`  
**Application checkout:** `C:\Users\rudra\Downloads\hydra`  
**Official upstream:** [hydralauncher/hydra](https://github.com/hydralauncher/hydra)

This is the current-state companion to the historical project memory and diary. Treat it as a dated snapshot; inspect the repositories again before acting.

## Repository identity and authority

These are three different locations:

1. `rudra-khandelwal/hydra` is the public research, documentation, and GitHub Pages repository. It is not the app source checkout.
2. `C:\Users\rudra\Downloads\hydra` is the local Hydra app checkout.
3. `hydralauncher/hydra` is the upstream app repository.

At the initial 4 November handoff, Git status had failed and the three changes were user-reported. A later read-only check succeeded: branch `main`, HEAD `fdbc5272720f96a634428ea47e33143fe4d4d393`, with modified `package.json` and `yarn.lock` and untracked `security-research/`. These are independently confirmed pre-existing changes; preserve them. No Git metadata repair was attempted.

**Hard boundary:** do not switch branches, reset, overwrite, stash, clean, commit, or otherwise modify the app checkout. All requested changes belong in this documentation repository. Do not merge, release, or tag.

## Project history and durable records

The project began as a public, independent research workspace in September 2026. Its existing chronology and evidence remain authoritative for earlier work:

- [Project master memory](../Hydra-Memory/README.md) — build history, environment, solved setup problems, and earlier AI context.
- [Project memory](PROJECT-MEMORY.md) — research invariants and control structure.
- [Research diary](../research/DIARY.md) — dated chronology; preserve old entries.
- [Findings](../research/FINDINGS.md) — evidence-qualified conclusions; no overall safety verdict.
- [Research agenda](../research/AGENDA.md) — outstanding work.
- [29 October handoff](../research/checkpoints/2026-10-29-hydra-chat-handoff.md) — previous build/runtime and safe-download plan.
- [AI quickstart](AI-AGENT-QUICKSTART.md) — how to resume and launch locally.
- [Repository map](REPOSITORY-MAP.md), [change control](CHANGE-CONTROL.md), and [validation matrix](../research/VALIDATION.md).

Verified repository history shows the first Pages workflow failure on 22 September 2026 because Pages was not enabled, followed by successful deployment after configuration. Later work established the project-memory/control center, research methods, and AI quickstart. The latest run observed before this update was Pages workflow run #132 for commit `30a74b7149a93e00c25ecd8c5cd6d9a88ff85933`, completed successfully on 31 October 2026. The deployment workflow is `.github/workflows/pages.yml`: push to `main` or manual dispatch, GitHub Pages artifact from repository root, deploy with `actions/deploy-pages@v5`. This workflow status verifies deployment action completion, not a browser-level content check.

## Historical work and current environment

Earlier documented work includes Windows 11 setup, successful VS2022 x64 native build, Rust/CMake/vcpkg troubleshooting, test `torrent_bridge_ownership`, runtime/process/network observations, API-mediated source metadata, and an AMSI interception observation. See the dated records; those old successes do not prove the current checkout still builds or runs.

Preserved launch sequence (not rerun on 4 November):

~~~bat
cd /d C:\Users\rudra\Downloads\hydra
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
yarn dev
~~~

Use a VS2022 x64 Developer Command Prompt. The persisted environment inventory is in [the master memory](../Hydra-Memory/README.md); version numbers there are historical unless rechecked. Do not reinstall tools without a new, captured failure.

## Download-source investigation — 4 November 2026

### Screenshot evidence supplied by the user

Hydra v4.1.4 showed these configured source counts and statuses in Settings: **onlinefix — 2,784 download options — Up to date** and **FitGirl — 7,127 download options — Up to date**. These are counts of options, not distinct games or proof of complete catalogue coverage.

| Game/search | Screenshot observation | What it supports |
|---|---|---|
| Granny: Escape Together | One result while onlinefix filter is active | That source list includes this separate game entry |
| Granny Remake | Game details show one download option, updated 24/07/2023 | A source option exists for this different game entry |
| Original Granny (DVloper) | Game details show “No downloads available,” release 20 Nov 2018 | No option appeared in the shown app state |
| Geometry Dash | Big Picture details show “No downloads available”; catalogue filtering shows 0 results for onlinefix and 0 for FitGirl | The tested source lists did not show a matching Geometry Dash entry |

The screenshots do **not** expose an API response, HTTP status, raw source metadata, or download URI. The Geometry Dash catalogue-filter result is source-list evidence, not proof that the API request was made or that app matching is wrong. Granny, Granny Remake, and Granny: Escape Together are distinct entries; one cannot stand in for another.

### Checkout code inspected

- Local `.env` currently contains `MAIN_VITE_API_URL=https://hydra-api-us-east-1.losbroxas.org` (no trailing slash in the observed value). `.env.example` leaves it blank. This value is local configuration and should not be copied into a secret-bearing log; never publish tokens or headers.
- Main game-details context calls `GET /games/{shop}/{objectId}/download-sources` with `take: 100`, `skip: 0`, and locally configured `downloadSourceIds`.
- Big Picture uses the same endpoint in `src/big-picture/src/hooks/queries/use-game-download-options.hook.ts`.
- `filterDownloadableRepacks` retains records only when at least one URI maps to a supported downloader: recognized HTTPS host prefixes or `magnet:`. Unsupported schemes/hosts are discarded.
- In the Big Picture hook, an empty/unsupported filtered result sets `no-download-options`. The request catch also maps failure to `no-download-options`; thus the user-facing category alone cannot distinguish backend failure from no matching/usable records. The desktop context logs failures and has no game-specific response captured here.

No app code was changed and no game was downloaded. **Current conclusion:** the screenshots establish limited coverage in the two configured sources for these examples. They do not establish a Hydra matching bug. The exact API response remains unknown.

## Next safe investigation

1. Reopen the app checkout without changing it; inspect `git status` with care, current `HEAD`, and existing changes. If Git status still errors, stop before any write operation on that checkout.
2. Use the existing build only if necessary; launch through the preserved VS2022 x64 command. Do not reinstall or alter dependencies.
3. Choose one exact catalogue entry that appears in a configured source list and record its store/shop and object ID from the app/API evidence; choose a comparison entry absent from the source list. Do not guess IDs.
4. Observe the read-only request for each: endpoint, HTTP status, response shape/count, and whether records are returned for the configured source IDs. Sanitize logs: record URI scheme and hostname class only, not complete download URLs, query strings, tokens, cookies, or authorization headers.
5. Compare the API response with `filterDownloadableRepacks` classifications. A nonempty API response containing a URI that the app drops would justify a focused matching investigation; an empty response is source/API coverage evidence. A request failure should be recorded separately even if the UI uses the same empty-state label.
6. Capture reproducible sanitized evidence before proposing code changes. If a defect is confirmed, then add a minimal regression test and request approval before changing the app checkout.
7. Do not add untrusted sources, download commercial games, install, or execute downloaded content. The immediate task is metadata diagnosis only.

## Live app follow-up — 4 November 2026

- Read-only checks succeeded: git status --short --branch returned branch main, with package.json and yarn.lock modified and security-research/ untracked. git rev-parse HEAD returned fdbc5272720f96a634428ea47e33143fe4d4d393; git log -1 --format="%H%n%s" identified “Merge pull request #2819 from hydralauncher/release/v4.1.4”. These pre-existing changes were preserved.
- Read-only code searches were run with: rg -n --glob '!*.map' 'download-sources|downloadSourceIds|downloadSources' src/main src/renderer src/shared src/big-picture; and rg -n --glob '!*.map' 'MAIN_VITE_API_URL|BASE_URL' src/main electron.vite.config.ts .env.example. Relevant source files already identified in this handoff remain the main API service, game-details context, Big Picture download-options hook, and shared URI filter.
- The running app UI showed the Schedule I game page at the Steam route with object ID 3164500 and displayed 16 download options. This identifies a candidate nonempty game entry; the exact configured source membership and underlying API payload were not captured.
- The Hydra and DevTools windows appeared in the app inventory, but the computer-use interface reported the target windows as minimized and did not expose their live state. No game-specific request status, response body, source IDs, or URI formats were captured. No direct API request was substituted, since configured source IDs and a comparison game's exact ID were not established from live evidence.
- No game was downloaded, installed, or executed. No app files were changed. The UI still needs a fresh live capture with the exact absent-game ID taken from the app, followed by the listed-game comparison; record status, response shape/count, configured source IDs, and URI scheme/host category only.


## Live API capture — 4 November 2026

### Evidence

Hydra was open on Geometry Dash at route `/game/steam/322170`. Developer Tools Network had Preserve log enabled, Fetch/XHR selected, and the page was refreshed with a `download-sources` filter. No matching renderer Fetch/XHR appeared. This is consistent with the implementation: renderer `window.electron.hydraApi.get` crosses preload IPC and the main process performs Axios. The actual request and response were verified in the app's sanitized main-process network log. Full download URIs, credentials, cookies, authorization headers, and personal data were not copied.

| Game | API path | HTTP response | Source IDs/names | URI scheme/category |
|---|---|---|---|---|
| Geometry Dash | `/games/steam/322170/download-sources` | 200; JSON `[]`; 0 records | Request included `BVnaGLvo` and `w4nVajB6`; no response records to identify a source | None |
| Schedule I | `/games/steam/3164500/download-sources` | 200; JSON array; 16 records | All 16 response records identify `onlinefix` / `BVnaGLvo` | All 16 `magnet:`; full URIs redacted |

Each page produced two identical logged calls. Settings showed source names onlinefix and FitGirl. The pairing `w4nVajB6` = FitGirl is inferred from the two-source list and the directly observed `onlinefix` ID; it was not independently confirmed from a response record.

### Code trace and assessment

1. `src/renderer/src/context/game-details/game-details.context.tsx` reads local source IDs and requests `/games/${shop}/${objectId}/download-sources` with `take: 100`, `skip: 0`; then `ensureArray`, `filterDownloadableRepacks`, and `setRepacks` process the response.
2. `src/preload/index.ts` bridges `hydraApi.get` through IPC. `src/main/events/misc/hydra-api-call.ts` dispatches to `HydraApi.get`; `src/main/services/hydra-api.ts` performs Axios and logs network events.
3. `src/shared/index.ts` filters repacks to those containing at least one URI recognized by a supported downloader. The successful empty Geometry Dash array means URI filtering did not cause its empty options. Schedule I's magnet URIs are accepted by the shared filter.
4. `src/renderer/src/pages/game-details/modals/repacks-modal.tsx` renders the generic no-results state when filtered repacks are empty.

**Confirmed immediate cause:** Geometry Dash's correctly routed Steam request returned HTTP 200 with an empty array. There was no request failure, response-shape mismatch, or URI filtering for those records (there were none). The response proves no matching source records were returned for this request; it does not establish whether the backend lacks coverage or applies a different server-side mapping/indexing rule.

**Working comparison:** Schedule I returned 16 records from onlinefix, all magnet-scheme, which the app can display.

### Commands and preservation

Read-only commands included `git status --short`, `git rev-parse HEAD`, `git branch --show-current`, targeted `rg -n` searches, and focused `Get-Content` reads of request, filtering, and modal code. App checkout remains branch `main`, HEAD `fdbc5272720f96a634428ea47e33143fe4d4d393`; status remains `M package.json`, `M yarn.lock`, `?? security-research/`. No app files changed. No tests were run. No game was downloaded, installed, or executed.

### Next step

Check backend/source catalogue coverage and matching for Steam ID 322170 against the Schedule I record, using a documented read-only path. Do not change frontend filtering based on this evidence. Separately, the UI could report request errors, successful empty results, and all-filtered results distinctly; that UX improvement is not needed to explain this captured empty response.

## Five-message handoff checkpoint

**Counter after this handoff: 2 of 5 user messages.** Each AI continuing the project must read [handoff cadence](HANDOFF-CADENCE.md), increment the counter for each new user message about this project, and update the current handoff plus diary/agenda when message 5 is reached. Record the new counter in the replacement handoff. Also update immediately for any material change or when work pauses. There is no verified background counter or automatic GitHub writer; do not claim that this cadence runs automatically.

## Public-repository review

This repository is public, and its full history remains public. Before each write, inspect the complete diff/content for credentials, personal data, raw logs, signed URLs, copyrighted files, or other material that should not be published. Keep screenshots local unless separately reviewed and intentionally approved for publication.
