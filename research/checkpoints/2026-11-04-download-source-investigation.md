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
- At the initial 4 November handoff, the three changes were user-reported because Git status failed. A subsequent read-only check succeeded and independently confirmed `M package.json`, `M yarn.lock`, and `?? security-research/`; preserve them and all other checkout contents.
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

## 4 November follow-up — live request capture remains unresolved

The current app checkout was checked read-only with git status --short --branch, git branch --show-current, git rev-parse HEAD, and git log -1 --format="%H%n%s". Results: branch main; HEAD fdbc5272720f96a634428ea47e33143fe4d4d393; message “Merge pull request #2819 from hydralauncher/release/v4.1.4”; status remains M package.json, M yarn.lock, and ?? security-research/. No checkout file was edited.

Read-only source searches used: rg -n --glob '!*.map' 'download-sources|downloadSourceIds|downloadSources' src/main src/renderer src/shared src/big-picture; and rg -n --glob '!*.map' 'MAIN_VITE_API_URL|BASE_URL' src/main electron.vite.config.ts .env.example. No test suite was run. The running Hydra UI was observed at the Schedule I page, route steam/3164500, displaying 16 download options. This is UI evidence for a nonempty entry, not the captured API response and not yet confirmation of which configured source returned it. The DevTools window was listed, but its live state could not be inspected because the UI control reported the window minimized. No status code, body, source IDs, or URI scheme/host categories were obtained. No synthetic request was issued, and no game was downloaded or run.

Finding remains unresolved. Next, restore/focus the running Hydra window, obtain the absent game's exact shop and object ID from its app page, then inspect the actual DevTools Network entries for both games. Sanitize request evidence; omit authorization/cookie headers, full download URLs, signed query strings, and personal data. Do not modify app code until this comparison identifies a concrete failing stage.


## Live API comparison — 4 November 2026

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

## Handoff counter

**User-message count since this handoff: 4/5.** Follow [HANDOFF-CADENCE.md](../../docs/HANDOFF-CADENCE.md). Update the current state and dated checkpoint at the fifth project-related user message, and sooner for meaningful state changes or before pausing. This is a documented manual checkpoint; no reliable automatic cross-chat counter or background GitHub updater has been configured.
