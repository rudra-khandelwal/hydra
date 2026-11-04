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


## Public backend and matching investigation — 4 November 2026

### Confirmed public evidence

- The official upstream [FAQ](https://github.com/hydralauncher/hydra/wiki/FAQ) says Hydra cannot exactly match a game to a download option and instead matches by title; it notes title-match inconsistencies. This is upstream documentation, edited 22 April 2025. It supports title-based matching as the intended behavior, but does not specify current matching normalization, aliases, or backend query rules.
- The public client schema in `src/types/index.ts` defines source JSON records (`DownloadSourceDownload`) with `title`, `uris`, `uploadDate`, and `fileSize`; there is no Steam ID, shop ID, or alias field in that shape. API-returned `GameRepack` adds `downloadSourceId` and `downloadSourceName`, also without a game ID.
- The client calls `/games/${shop}/${objectId}/download-sources` and passes the locally configured source IDs. Source sync sends those IDs to `/download-sources/sync`; adding a source registers its public URL at `/download-sources`. These client requests confirm the two configured IDs are sent, not how the service indexes source contents.
- In the captured Schedule I response, all 16 records directly associate `onlinefix` with `BVnaGLvo`. `w4nVajB6` remains only an inferred FitGirl ID based on the settings names. Geometry Dash returned no records, so that response cannot associate either ID with an entry.
- In public upstream issue [#2381](https://github.com/hydralauncher/hydra/issues/2381#issuecomment-4761820746), a maintainer states the production backend and infrastructure will not be open-sourced or self-hostable. This is evidence that the matching implementation cannot be audited in the public app repo; it is not a statement about this particular game.

### What remains unknown

No public source JSON URL for the two configured local source records is present in this documentation or the captured API response, and no source metadata file was inspected. Therefore we cannot confirm whether Geometry Dash appears under an alternate title in either source, whether a title alias exists, or whether the private service maps titles to Steam 322170. The source IDs were sent in the request; the empty response does not reveal per-source indexing or exclusion reasons. No alternate Geometry Dash ID mapping was found in the inspected client-side types or request path, but that does not rule out private backend aliases.

### Assessment and next action

The best supported explanation class is source-title matching/coverage: upstream documentation confirms title matching rather than exact identity matching, and the source JSON shape provides a title but no game identifier. This is explanatory context, not a confirmed root cause for Geometry Dash. The confirmed immediate cause remains the successful empty API response.

Next, compare the exact public JSON metadata files referenced by the two configured sources for titles/aliases corresponding to Geometry Dash and Schedule I. This requires the exact source URLs (or the user providing them); do not substitute similarly named community URLs. Inspect only title and source identifiers, redact all URIs. If the entries do not explain the difference, the remaining step requires a documented service response or maintainer clarification; do not probe private endpoints or bypass access controls. Keep frontend filtering unchanged.

Read-only inspection in this pass: `rg` targeted searches in `src/main`, `src/types`, and renderer source; `Get-Content` of `src/main/events/download-sources/{add-download-source,sync-download-sources}.ts`, `src/main/services/user/sync-download-sources.ts`, `src/types/index.ts`, and the game-details request block; public upstream FAQ and issue #2381/comment review; and `git status --short`, `git rev-parse HEAD`, `git branch --show-current`. No tests were run; no app files were changed; the working-tree changes remain preserved.


## Source collections and settings clarification — 4 November 2026

### Clarification

The user confirmed Hydra does not offer an edit-in-place action for a configured source URL: Settings displays the URL read-only and offers removal. Do not remove, replace, or otherwise disturb the existing onlinefix or FitGirl sources. This is a constraint for future guidance; no source action was taken.

### Collection, storage, and synchronization behavior in the app client

- `src/renderer/src/pages/settings/add-download-source-modal.tsx` accepts a syntactically valid URL and invokes `addDownloadSource`; the Settings row shows the URL read-only and a Remove action.
- `src/main/events/download-sources/add-download-source.ts` posts the supplied URL to `/download-sources`; the API response is a `DownloadSource` object and is saved locally in the LevelDB `downloadSources` sublevel keyed by its ID. For signed-in users with active subscription, the URL is also posted to `/profile/download-sources`.
- `src/main/events/download-sources/sync-download-sources.ts` sends locally stored IDs to `/download-sources/sync`, merges returned `DownloadSource` objects into the local records, and stores them by ID. `src/main/services/user/sync-download-sources.ts` reads `/profile/download-sources` and adds returned objects when their URL is not already stored.
- Thus source records and URLs are persisted locally, and the API also returns source objects containing the URL. The app's client-side source metadata includes `id`, `name`, `url`, `status`, `downloadCount`, optional `fingerprint`, and timestamps.
- The UI text and input placeholder describe a direct URL to a `.json` file. The client source type `DownloadSourceDownload` defines per-entry `title`, `uris: string[]`, `uploadDate`, and `fileSize`. The likely collection shape is a JSON list of these entries; the client checkout does not contain the private service's validation/parser, so exact root-shape and server-side constraints are not independently verified here.

The code establishes a source URL pointing to a remote JSON collection. It does not establish that every collection is curated, has a fixed/limited game set, or contains one record per game. No source JSON URLs or contents were exposed or fetched in this investigation.

### Counts and title visibility

Settings renders `DownloadSource.downloadCount` with localized wording for **download options**, not unique games. Clicking that row navigates to the Catalogue with the source fingerprint filter. Catalogue search sends configured source IDs and the fingerprint filters to `/catalogue/search`, then renders matching catalogue records/titles. This existing path can show catalogue titles attributed to a source, subject to the backend's title-matching behavior documented in the prior checkpoint.

A unique-game count should not reuse `downloadCount`: a source may have multiple options per game, and title matching is not exact identity matching. A separately labeled count could use the source-filtered catalogue result count if the API defines it as distinct games; that backend semantic is not exposed in the public client. Any title list should be labeled as catalogue matches for that source, not a guaranteed exact Steam-ID mapping.

### Adding another source safely

Hydra's UI flow is Settings → Download Sources → Add source. The user supplies a URL that points directly to a JSON file; the client checks URL syntax, then asks the Hydra API to register it; the private endpoint's validation details are not present in the client code. The record format described by the client is one entry with `title`, `uris` (string array), `uploadDate`, and `fileSize`; the UI expects the service to accept the collection. Use only a source URL published by a maintainer you trust, preferably HTTPS, and content you are legally authorized to access. Do not add a source merely because its name resembles a known publisher, and do not remove onlinefix or FitGirl to try another URL.

### Evidence and limitations

Read-only source files: `src/types/index.ts`; `src/renderer/src/pages/settings/{settings-download-sources.tsx,add-download-source-modal.tsx}`; `src/main/events/download-sources/{add-download-source.ts,sync-download-sources.ts,get-download-sources.ts,remove-download-source.ts}`; `src/main/services/user/sync-download-sources.ts`; `src/main/level/sublevels/download-sources.ts`; and `src/renderer/src/pages/catalogue/catalogue.tsx`. Public upstream source FAQ and the maintainer statement about the closed production backend remain linked in the previous section. No source URL was fetched, no source was added/removed, no application file changed, and no test ran. Checkout status remains `M package.json`, `M yarn.lock`, and `?? security-research/` at app HEAD `fdbc5272720f96a634428ea47e33143fe4d4d393`.

Next step, if source-by-source title coverage is needed: obtain the exact public JSON URLs from the user or source publishers, then inspect only record titles and counts with all URI values redacted. Do not infer or guess URLs.


## Source collection inventory attempt — 4 November 2026

Hydra Settings exposed the exact configured JSON URLs in the local source records (the URLs are intentionally omitted from this public checkpoint). Both records were named onlinefix and FitGirl and showed status Up to date. The displayed `downloadCount` values were 2,843 and 7,210 respectively; these are **download-option counts**, not unique-title counts.

Read-only GET requests were made to the exact URLs shown in Settings. Both returned HTTP 403 Forbidden. No response body or source JSON was retained or parsed, and no alternate host, mirror, endpoint, or access path was tried. The cause of the 403 (access policy, anti-automation, or another server rule) is unknown.

Consequently, total source JSON records, unique titles, duplicate titles, titles shared by sources, and exact source-level inclusion of Geometry Dash, Schedule I, original Granny, Granny Remake, and Granny: Escape Together could not be computed from the files. Earlier per-game API evidence remains: Schedule I returned 16 onlinefix options; Geometry Dash returned an empty array. Those API results do not establish whether either title is present in the underlying JSON collection.

Relevant client code reviewed read-only: `src/types/index.ts`; `src/main/events/download-sources/add-download-source.ts`; `src/main/events/download-sources/sync-download-sources.ts`; `src/main/events/download-sources/get-download-sources.ts`; `src/main/events/download-sources/remove-download-source.ts`; `src/main/services/user/sync-download-sources.ts`; `src/main/level/sublevels/download-sources.ts`; `src/renderer/src/pages/settings/add-download-source-modal.tsx`; `src/renderer/src/pages/settings/settings-download-sources.tsx`; `src/renderer/src/pages/catalogue/catalogue.tsx`.

Next step: obtain read-only access to the same two source JSON files from their publishers (for example, a publisher-provided export or permissioned access). Then compute counts and target-title matches locally while retaining only title/count metadata. Do not guess URLs, use third-party mirrors, or change the configured sources.

No source was added, removed, or replaced. No application file, dependency, or existing working-tree change was modified. No tests were run or game content downloaded.
## Five-message handoff checkpoint

**Counter after this handoff: 0 of 5 user messages.** Each AI continuing the project must read [handoff cadence](HANDOFF-CADENCE.md), increment the counter for each new user message about this project, and update the current handoff plus diary/agenda when message 5 is reached. Record the new counter in the replacement handoff. Also update immediately for any material change or when work pauses. There is no verified background counter or automatic GitHub writer; do not claim that this cadence runs automatically.

## Public-repository review

This repository is public, and its full history remains public. Before each write, inspect the complete diff/content for credentials, personal data, raw logs, signed URLs, copyrighted files, or other material that should not be published. Keep screenshots local unless separately reviewed and intentionally approved for publication.
