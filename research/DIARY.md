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

