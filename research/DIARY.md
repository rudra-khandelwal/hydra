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
