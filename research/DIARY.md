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
The live HTML now treats GitHub as the source of truth: public repository metadata, recent commits, GitHub Actions status, repository file tree, and research diary/agenda/findings are fetched from GitHub when the page loads.

### [RUDRA] Main repository live-guide link
The main GitHub repository README now exposes the public research guide directly at `https://rudra-khandelwal.github.io/hydra/` for easy visitor access.

### [CHATGPT] README publication update
The repository README was updated to prominently link the live GitHub Pages guide and document that GitHub is the source of truth for the live research record.

### [CHATGPT] Public guide restoration and favicon
The public GitHub Pages guide was rebuilt from the earlier v4 research guide content, restoring the documented research checkpoint, daily research routine, verified Windows toolchain details, troubleshooting history, final clean command sequence, and a single copy-paste setup block. Private vault controls and encrypted credential material were not carried into the public site.

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
The public guide's Research Notes section was upgraded from a plain text note workflow to a rich editor. A saved note now creates a new numbered section after the original guide sections (17, 18, 19, …), with a user-defined section title and a corresponding sidebar entry.

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
A new research day was started with a fresh Hydra runtime observation cycle. Existing historical diary entries were preserved rather than rewritten.

### [CHATGPT] Download-source API correlation
Hydra requests to the game download-source endpoint were observed with source IDs `BVnaGLvo` and `w4nVajB6`. The API returned a concrete download-source record associated with `w4nVajB6` and the source name `FitGirl`, including URI/torrent metadata. The full magnet/tracker data was not copied into the public diary because it is unnecessary to the security finding.

### [CHATGPT] Source-code correlation
Repository source inspection showed that Hydra maintains a local `downloadSources` store and synchronizes source definitions with the Hydra API. The client also exposes API-backed source creation and synchronization logic. This strengthens the architectural model in which the Hydra API is a trust boundary between the client and configured download-source metadata.

### [CHATGPT] Trust-boundary conclusion
The current evidence demonstrates metadata flow from Hydra API responses into the Hydra client and local source storage. It does not establish peer/tracker communication or behavior of a downloaded executable. Those require a separate controlled download and analysis experiment.

### [CHATGPT] Antivirus control result
Windows antivirus/AMSI blocked the EICAR test string at the PowerShell command stage. Because the assignment was blocked before a valid test file was established, the result is recorded as an AV interception control rather than a completed EICAR-file quarantine test. No Defender threat-history record was displayed by the queried cmdlets in the captured output.

### [RUDRA] Public-evidence handling
The public research record will retain conclusions and reproducible methodology while avoiding publication of credentials, authentication data, raw sensitive logs, or unnecessary redistribution metadata.

### Next checkpoint
Perform a controlled download test with a legitimate free/open-source artifact, then compare process, network, filesystem, hash, and Defender observations before considering execution.


### [CHATGPT] Responsive multi-environment guide foundation
The public guide was upgraded to use a responsive foundation for desktop, laptop, tablet, and phone viewports while preserving the existing visual design and content. The layout now adapts navigation, spacing, typography, grids, tables, code blocks, research panels, and note-editor controls to available screen width.

The mobile navigation becomes a touch-friendly slide-out menu with keyboard Escape support and automatic closing after navigation. Safe-area insets, dynamic viewport height, touch targets, reduced-motion preferences, forced-colors support, and horizontal overflow handling were added so the same guide can be used across mouse, keyboard, touch, and narrow-screen environments.

### [CHATGPT] Responsive design basis
The responsive changes follow the current web platform approach of flexible layouts, media/container-aware adaptation, responsive typography, touch interaction, accessibility, and overflow-safe components. The implementation keeps the guide as a single HTML page rather than creating separate desktop/mobile versions.


### [CHATGPT] GitHub Actions runtime warning cleanup
The GitHub Pages workflow was updated after a successful deployment still reported a Node.js 20 deprecation annotation. First-party actions were moved to Node 24-compatible current major versions: `checkout@v7`, `configure-pages@v6`, `upload-pages-artifact@v5`, and `deploy-pages@v5`. The runner was pinned to `ubuntu-24.04` so the repository is not silently moved by the upcoming `ubuntu-latest` → Ubuntu 26.04 migration. The warning was treated as maintenance debt rather than a deployment failure.