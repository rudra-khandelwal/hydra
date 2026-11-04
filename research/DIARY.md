# Research Diary

This is the chronological project record. Historical entries are preserved rather than rewritten.

## 21 September 2026

### [CLAUDE] Security-plan checkpoint
A structured security research workflow was established: baseline → controlled operation → differential analysis → validation → finding.

### [CHATGPT] Runtime baseline
A Windows baseline was collected for processes, established network connections, and repository files before controlled testing.

### [CHATGPT] Hydra-owned HTTPS
Hydra/Electron processes were correlated with established HTTPS connections. The observation was recorded as runtime evidence, not as a security conclusion.

### [CHATGPT] Third-party source boundary
The configured community download source was treated separately from Hydra itself and from the final downloaded software.

## 22 September 2026

### [CHATGPT] Repository structure checkpoint
The research workspace was organized in GitHub with documentation, research diary/agenda/findings, security-research guidance, upstream notes, a sanitized public HTML guide, and a GitHub Pages workflow.

### [RUDRA] Public-repository decision
The project owner decided that the GitHub research repository should be public rather than private, with the expectation that all committed material is suitable for public inspection.

### [CHATGPT] Public-repository verification
The GitHub repository `rudra-khandelwal/hydra` was verified as **public** after the visibility change.

### [CHATGPT] Public HTML publication
The sanitized `index.html` research guide is present in the public repository. The separate offline/private vault file was not added to the repository.

### [CHATGPT] GitHub Pages deployment attempt
A GitHub Actions workflow named `Deploy GitHub Pages` was triggered after adding the Pages workflow.

### [CHATGPT] Pages failure diagnosis
The first workflow run on commit `8d2c2afcf3cd32a6dcc746dee56608447906bd1f` completed with failure. Checkout succeeded, but `actions/configure-pages@v5` failed with a `Not Found` error stating that the repository's Pages site was not enabled/configured to build using GitHub Actions. Artifact upload and deployment were therefore skipped.

### [CHATGPT] Evidence handling
Today's public log records the observed GitHub Actions state and repository changes without copying credentials, tokens, personal authentication data, or raw sensitive logs.

### [RUDRA] Publication scope
The research repository is intended to remain fully public. Future commits must therefore continue to pass a public-release review before being pushed.

### Next checkpoint
Enable/configure GitHub Pages for the public repository, rerun the deployment workflow, verify the published site, then continue the controlled security research cycle and record each substantive test as a dated checkpoint.

### [CHATGPT] Live GitHub data integration
The public HTML guide now reads repository metadata, GitHub Actions Pages status, recent commits, the public file tree, and the research diary/agenda/findings from GitHub at page load. GitHub is the source of truth for the live research record.

### [RUDRA] Public guide access
The live guide is available at `https://rudra-khandelwal.github.io/hydra/` for direct access.

### [CHATGPT] GitHub Pages deployment verified
The latest Pages workflow run (#7) for commit `171fc032305750e1c35bad7952073cb8c3877155` completed successfully. The earlier failed deployment remains visible as historical deployment history in GitHub.

### [CHATGPT] Live guide data model
The public HTML now treats GitHub as the source of truth: public repository metadata, recent commits, GitHub Actions status, repository file tree, and research diary/agenda/findings are fetched from GitHub when the page loads.

### [RUDRA] Main repository live-guide link
The main GitHub repository README now exposes the public research guide directly at `https://rudra-khandelwal.github.io/hydra/` for easy visitor access.

### [CHATGPT] README publication update
The repository README was updated to prominently link the live GitHub Pages guide and document that GitHub is the source of truth for the live research record.

### [CHATGPT] Public guide restoration and favicon
The public GitHub Pages guide was rebuilt from the earlier v4 research guide content, restoring the documented research checkpoint, research routine, verified Windows toolchain details, troubleshooting history, final clean command sequence, and a single copy-paste setup block. Private vault controls and encrypted credential material were not carried into the public site.

### [RUDRA] Main README cleanup
Removed the prominent live-guide banner from the main repository README as requested. The live guide remains the GitHub Pages site, while the HTML itself provides direct repository/research navigation.

### [CHATGPT] GitHub Pages favicon
Added a public `favicon.svg` with a white H mark so the browser tab uses an H icon instead of the generic globe icon.

### [CHATGPT] Claude design + current data restoration
Restored the earlier Claude visual design language for the public guide: dark brown/orange title bar, sticky left navigation, monospace section labels, compact research panels, and the original build-guide structure. The current verified Node 24.19.0 / VS2022 environment, research checkpoint, one-paste setup, daily status, attributed diary and troubleshooting data were retained. Private credentials/vault material remain excluded.

### [CHATGPT] Single live README link
The main README now contains one direct live-guide link, rather than a large banner or multiple repeated live-guide links.

### [CHATGPT] Live-guide navigation correction
The public guide navigation was corrected so desktop/tablet side navigation stays fixed while the content scrolls. The Overview link now targets the guide hero ("windows · source build · security-minded workflow" / "Hydra Launcher") instead of the Overview section heading. The top-bar repository link was replaced with a single GitHub repo button beside the Hydra Launcher title. When the guide was opened from GitHub, the button can reuse the originating GitHub tab without closing the guide; direct opens fall back to a new repository tab. The README live-guide link was changed to open the guide in a new tab.

### [CHATGPT] Live-guide navigation hardening
The responsive navigation was consolidated so desktop/tablet uses a single fixed sidebar model and mobile keeps the slide-out model. The duplicate desktop CSS override was removed, the old title-bar repository button was removed so only the hero GitHub button remains, and the Overview target received an explicit scroll offset. The GitHub→guide opener bridge now refreshes the originating GitHub tab once via reload and the hero repository button focuses that originating tab when available; direct opens fall back to the repository link in a new tab.

### [CHATGPT] Research notes editor redesign
The Research Notes section was upgraded from a plain text note workflow to a rich editor. A saved note now creates a new numbered section after the original guide sections, with a user-defined section title and a corresponding sidebar entry.

### [CHATGPT] Created-section navigation
Created research notes now render as full research-panel sections and are added to a dedicated sidebar group. New entries use the same navigation/entry animation language as the guide, and saving a note automatically scrolls to the newly created section. Only user-created sections can be deleted; the original guide sections remain protected.

### [CHATGPT] Rich research-note formatting
The note editor now supports bold text, underline, direct clickable URLs, and named clickable links. Link handling is restricted to HTTP/HTTPS URLs, with safe external-link attributes applied when notes are rendered.

### [CHATGPT] Security research navigation simplification
The previous 12A/12B/12C/12D navigation was consolidated into section 12, `security-check`, with a `security research` subtopic and the checkpoint, one-go, status, and diary items grouped beneath it.

### [CHATGPT] Legacy note migration
Existing browser-saved research notes from the earlier plain-text format were migrated into the new rich-note structure, preserving their text and line breaks instead of discarding prior notes.

### [CHATGPT] Research-note validation
The updated client-side JavaScript was syntax-checked after the migration fix and passed validation. The public guide changes were committed to the repository in sequential updates, including the final legacy line-break migration fix.

### [RUDRA] End-of-day checkpoint
Today's guide/editor work is considered complete for the day. Historical diary entries remain preserved, the public guide contains the current research-note workflow, and no private vault credentials or authentication material were added to the public repository.

### Next checkpoint
Verify the latest GitHub Pages deployment in a browser, test creating/formatting/deleting a research note on the live guide, then continue the controlled Hydra security research cycle and record the next substantive runtime test.

## 25 September 2026

### [CHATGPT] Fresh-session security checkpoint
A new research day was started with a fresh Hydra runtime observation cycle.

### [CHATGPT] Download-source API correlation
A Hydra API request and returned download-source metadata were correlated with the client handling path. This established an architectural trust boundary, not proof that a peer/tracker transfer occurred.

### [CHATGPT] Antivirus/AMSI control observation
The EICAR test string was blocked while being assigned in PowerShell. No valid EICAR file or Defender quarantine event was established; the result is limited to script/content interception.

## 29 October 2026

### [CHATGPT] Runtime and controlled-download handoff
The project handoff separated build/configuration/API/catalogue questions from source trust, download behavior, and artifact safety. The prescribed next experiment was a download-only test of an authorized artifact, followed by static inspection. Installation/execution requires a separate approval and isolated environment.

## 4 November 2026

### [RUDRA] Download-source coverage screenshots
Hydra v4.1.4 screenshots showed onlinefix and FitGirl source counts/status and mixed availability across the tested game entries. These observations support limited source coverage for those entries; they do not by themselves establish an application bug or malicious behavior.

### [CHATGPT] Read-only code-path review
The local checkout was reviewed read-only for API configuration, game-specific source requests, URI filtering, and user-facing availability state. A game-specific response was not captured; no application file was changed and no content was downloaded.

### [CHATGPT] Source collection inventory access blocked
Direct GET requests to the exact configured source JSON URLs returned HTTP 403. No JSON payload was parsed and no alternate path, mirror, or bypass was attempted. Counts/overlap at the unique-title level therefore remain unknown.

### [USER] Security-first objective reaffirmed
The user confirmed that prior runtime, source/API, trust-boundary, code-inspection, and AV/AMSI observations should be treated as substantial completed historical work. The main remaining experiment is a controlled download-only test through Hydra, gated on an exact authorized artifact.

### [CODEX REPORT] Initial artifact selection
OpenTTD displayed “No downloads available.” No suitable authorized artifact was identified and no download was started. Fresh Defender/download-directory/free-space checks were not done during that selection pass.

### [CODEX REPORT] Mindustry candidate review
Hydra v4.1.4 displayed one OnlineFix option for Mindustry (Steam app 1127400). The official project/repository and GPL-3.0 licence were identified, but the specific OnlineFix payload/release and authorization of that distribution were not verified. The option was not opened and its URI was not exposed. OpenTTD again showed “No downloads available.” No download, installation, execution, source/settings change, or application/local-checkout modification occurred. Mindustry was not approved.

### [CODEX REPORT] Second read-only candidate search
The follow-up search checked Mindustry, OpenTTD, Hedgewars, Battle for Wesnoth, and SuperTuxKart. No title met all requirements. Mindustry remained the strongest lead but ineligible because the OnlineFix distribution could not be matched to an official release or otherwise authorized route. OpenTTD showed “No downloads available”; no current downloadable entry was established for Hedgewars, Battle for Wesnoth, or SuperTuxKart. The report described a focused search, not exhaustive enumeration. No download links were opened, no URI was exposed, and no download, installation, execution, settings/source change, or application/local-checkout modification occurred. See [second candidate search](checkpoints/2026-11-04-second-candidate-search.md).

### [CHATGPT] Security decision
No artifact is approved. The controlled Hydra download remains blocked on provenance/authorization evidence. Failure to meet the candidate gate is not evidence that Hydra or any configured source is malicious. The next useful step is narrow: verify one exact existing source record against official publisher/release evidence, without opening download links or changing configuration. Only after that should a fresh pre-download baseline and explicit download-only approval be considered.


### [CODEX REPORT] Final targeted provenance check — no qualifying artifact
The final targeted read-only review did not identify an existing Hydra entry that could be independently matched to an official free/open-source project release or an explicitly authorized distributor. No qualifying test artifact is available from the existing Hydra sources based on the checks completed.

Mindustry remains an unapproved lead only: Hydra v4.1.4 showed one OnlineFix option, while the official Mindustry repository and GPL-3.0 licence establish project identity/licensing but do not link OnlineFix to an official release or authorize that specific distribution. The specific option and URI were not opened. OpenTTD, Hedgewars, Battle for Wesnoth, and SuperTuxKart had already failed to produce a qualifying entry in the focused checks.

The investigation stopped without opening download links, exposing URIs, bypassing HTTP 403, changing Hydra settings/sources, modifying the application checkout, downloading, installing, or executing anything. No new malware or safety conclusion follows from this candidate-selection result.

**Disposition:** Keep the Hydra download-path experiment blocked until new exact-source provenance and authorization evidence is available. Do not broaden catalogue searches by default. A direct-from-official-publisher artifact analysis, if separately approved later, would not test Hydra's download path.


### [CHATGPT] Official-publisher artifact-analysis candidate checkpoint
A separate candidate-review checkpoint was added for potential static analysis of software obtained directly from its official publisher. The user-supplied research report identified PuTTY 0.85, 7-Zip 26.05, and Notepad++ 8.9.8.1 as candidates with differing evidence gaps. PuTTY is recorded as a provisional preference based on the reported MIT licence and official GPG/Authenticode guidance; its exact selected package size and package-specific signing details remain unverified. 7-Zip's reported x64 installer is approximately 1.6 MB, but its licence is mixed and the specific installer's signature/checksum was not verified. Notepad++'s release date/current stable status, package size, and publisher/signature details remain unresolved.

The checkpoint defines a read-only baseline and post-approval static-inspection procedure, and distinguishes direct official-publisher artifact analysis from Hydra download-path analysis. No artifact was downloaded, installed, or executed. No Hydra application source, configuration, or local checkout was modified. The Hydra download-path experiment remains blocked by the previously recorded source-distribution authorization gap.

See [official-publisher candidate checkpoint](checkpoints/2026-11-04-official-publisher-static-analysis-candidates.md).


### [RUDRA] PuTTY 0.85 download-only approval
The user explicitly approved downloading only the official PuTTY 0.85 64-bit x86 standalone putty.exe for security analysis. The approval did not include installation or execution and did not authorize any changes to the Hydra application checkout, settings, or configured sources.

### [CODEX REPORT] PuTTY 0.85 artifact and cryptographic verification
The supplied report records putty.exe at 1,706,136 bytes with SHA-256 d01fdb5aae8f112526040a39b0bfb9e27d813003178645e65f8d1cfdb2a26c87, exactly matching the official w64/putty.exe manifest entry. Authenticode was Valid with signer Simon Tatham. The executable GPG signature was Good signature. The sha256sums.gpg file was initially passed to GPG using detached-signature syntax and failed; inspection identified it as a clear-signed PGP message, and verification using the correct format returned Good signature. Both GPG checks used fingerprint 1A07 DAC0 F220 CF12 248E A719 5C67 D0F8 8BC3 E5B5. GPG key trust remains uncertified in the local keyring. Defender's command-line scan reported no threats; Defender status could not be independently queried because the status cmdlet failed to load. PuTTY was not run or installed.

### [CODEX REPORT] Static inspection unavailable
The subsequent Codex pass confirmed the artifact size and hash and reported PuTTY 0.85 version metadata. PE inspection could not be performed because objdump, strings, dumpbin, llvm-readobj, and sigcheck were unavailable and Python was inaccessible. No tool was installed. No verified PE-section, import/export, embedded-string/endpoint, dependency, packing, or obfuscation findings exist. The work is pending until a trusted, already-available static-analysis toolchain can be used without running the artifact.

### [CHATGPT] Five-message handoff review reconciled
The repository's five-message cadence is manual, not an automatic background updater. The available repository and prior conversation context did not establish a specific reason or decision for pausing the report. The supported explanation is that the manual counter/checkpoint was not deliberately carried forward while the research focus moved through candidate provenance and PuTTY verification. The accumulated work has now been documented in a dated handoff; the cadence counter is reset to 0/5. This direct-publisher artifact analysis remains separate from the blocked Hydra download-path experiment.

See [PuTTY artifact-analysis handoff](checkpoints/2026-11-04-putty-static-analysis-handoff.md).


### [CODEX REPORT] PuTTY 0.85 PE and printable-string inspection
The user supplied Codex results from the already-installed Visual Studio `dumpbin.exe`: `/HEADERS`, `/IMPORTS`, and `/EXPORTS` all returned exit code 0. The reported tool file metadata version was 14.44.35229.0. The x64 PE had Windows GUI subsystem, sections including `.text`, `.rdata`, `.data`, `.pdata`, `.00cfg`, `.gxfg`, `.tls`, `_RDATA`, `.rsrc`, and `.reloc`. Imports included standard Windows GUI, system, shell, dialog, and registry libraries. Winsock library names were absent from the static imports but present in extracted strings alongside dynamic-loader names, consistent with possible dynamic loading but not proof of runtime use.

A read-only PowerShell/.NET byte-array scan reported 10,241 ASCII and 1,045 UTF-16LE strings. Reviewed strings included official PuTTY identity/contact strings, certificate status URLs, a placeholder hostname, generic address literals, Winsock DLL names, and process/registry/dynamic-loader API names. No unexplained production endpoint or clearly malicious string was identified. The same target hash and size were reported before and after.

### [CODEX REPORT] PuTTY section entropy and PE resource inventory
PowerShell/.NET raw-byte parsing calculated section entropy. The `.rsrc` section measured 7.8331 bits/byte; entropy alone was not treated as proof of packing. A manually bounded PE resource parser found 24 leaves with no malformed or out-of-bounds branches reported: 12 ICON, two GROUP_ICON, seven DIALOG, one VERSION, one MANIFEST, and one numeric type ID 2000. Version metadata reported PuTTY 0.85.0.0 and Simon Tatham. The manifest declared Common Controls 6.0 and DPI-awareness metadata, with no explicit `requestedExecutionLevel` or compatibility/`supportedOS` element. No elevation inference was made from those absences.

### [CODEX REPORT] PuTTY embedded HTML Help metadata
The resource type ID 2000 payload was confirmed at raw offset `0x13DCF0`, size 365,163 bytes, with ITSF signature. A raw-byte parser identified ITSF v3 and ITSP v1 metadata and five PMGL listing chunks plus one PMGI index chunk. It parsed 561 PMGL entries: nine uncompressed section-0 entries and 552 MSCompressed/LZX section-1 entries. Names included `/index.html` and `/chm.css`; /index.html remains a filename-only landing-page candidate. No embedded file contents were read, extracted, decompressed, rendered, or executed. The user reported that parser reports and inventory are retained locally; the public checkpoint omits local paths and payload contents.

The large compiled HTML Help resource plausibly explains the high `.rsrc` entropy and is consistent with the version string “with embedded help.” Resource names alone do not establish content or behavior. The target size (1,706,136 bytes) and SHA-256 (`d01fdb5aae8e112526040a39b0bfb9e27d813003178645e65f8d1cfdb2a26c87`) were reported unchanged across inspections. PuTTY was never loaded, launched, installed, or executed. No Hydra application or configuration changes occurred.

**Assessment:** The examined static evidence has not identified a clearly malicious indicator, but it does not prove safety. Runtime behavior, embedded help contents/default topic, independent GPG key trust, and Defender real-time status remain unverified. Direct official-publisher analysis remains distinct from the still-blocked Hydra download-path experiment. See the [PuTTY embedded-help metadata checkpoint](https://github.com/rudra-khandelwal/hydra/blob/main/research/checkpoints/2026-11-04-putty-embedded-help-metadata.md).
