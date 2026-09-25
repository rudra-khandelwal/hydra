# Project Memory — Canonical AI & Maintainer Handoff

**Repository:** `rudra-khandelwal/hydra`  
**Upstream:** `hydralauncher/hydra`  
**Public guide:** `https://rudra-khandelwal.github.io/hydra/`  
**Default branch:** `main`  
**Project status:** Active public research/development workspace  
**Last memory review:** 25 September 2026

## Purpose

This file is the canonical project-memory document for future AI assistants and maintainers working on this repository.

It exists so the project does not depend on hidden conversation context. A future assistant should read this file first, then inspect the current repository state before making changes.

This is **public**. Do not place credentials, private authentication material, raw sensitive logs, or other secrets here.

## Source-of-truth hierarchy

When sources disagree, use this order:

1. **Current repository contents and current Git history** — what actually exists.
2. **Dated evidence/checkpoints** — what was actually observed and recorded.
3. **This project memory** — operational context, decisions, invariants, and handoff state.
4. **Research diary/agenda** — chronology and planned work.
5. **Conversation memory** — useful context, but never a substitute for checking the repository.

Never claim a live behavior was verified solely because the code looks correct.

## Project goal

Build and maintain a reproducible Windows development and defensive security-research workflow around the open-source Hydra Launcher project.

The research path is:

`source → build → baseline → controlled operation → differential observation → source correlation → validation → finding`

The immediate security-research objective after guide maintenance is a controlled download experiment using a **legitimate free/open-source artifact**, followed by process, network, filesystem, hash, Defender/AV, and static analysis before any appropriate execution.

The project must not drift into:

- DRM bypass
- credential theft or unauthorized access
- unauthorized acquisition/distribution of copyrighted software
- unsupported malware/safety verdicts
- publication of secrets

## Repository invariants

These rules are persistent:

- The repository is public.
- Every committed file and its Git history should be treated as public.
- Never commit passwords, tokens, API keys, cookies, private keys, recovery codes, or raw credential-bearing logs.
- Do not commit proprietary/copyrighted downloaded software as research artifacts.
- Keep Hydra behavior separate from API behavior, community-source behavior, third-party download infrastructure, and downloaded-file behavior.
- Use **Fact → Observation → Hypothesis → Finding → Next Action** for substantive research.
- Do not upgrade a hypothesis into a finding without evidence.
- Keep historical diary entries; do not rewrite history as if later work happened earlier.
- Keep the live guide responsive without creating separate device-specific pages.
- The maintainer normally opens the current public GitHub Pages live link after each repository update; treat this as the expected browser-check path, while still distinguishing deployed state from live verification.
- The live guide uses a dark brown/orange research-console theme. Project Control links are transparent by default with only a subtle translucent accent on hover/focus.
- On wide desktop screens, a compact Project Map rail sits to the left of the main fixed sidebar. Its category buttons scroll the main sidebar to Hydra Launcher, Setup, Build, Created Notes, Project Control, Security Research, or Research.
- The Project Map rail is hidden on narrower screens to protect the existing responsive layout.
- Detailed UI decisions are recorded in docs/HTML-GUIDE-DESIGN.md.
- When changing the live guide, update the GitHub repository first; GitHub Pages is deployment output.
- After every material change, inspect the resulting diff/state before reporting completion.
- A green GitHub Actions run is not automatically a clean run; inspect warnings/annotations too.

## Current validated Windows environment

- Windows 11
- Node.js 24.19.0
- Yarn 1.22.22
- Rust 1.98.1 / Cargo 1.98.1
- Visual Studio 2022 Build Tools 17.14.41
- MSVC v143
- Windows SDK
- x86_64-pc-windows-msvc

The validated native-build environment uses VS2022/v143 consistently. Do not mix the VS2026 toolchain into the Hydra native build.

## Live-guide invariants

The public guide `index.html` is both a build/security guide and a project-control surface.

Current navigation requirements:

- Desktop/tablet sidebar remains fixed while document content scrolls.
- Mobile uses the slide-out navigation.
- Sidebar `overview` targets the hero containing “windows · source build · security-minded workflow” and “Hydra Launcher”.
- Only one GitHub repository button exists: beside the Hydra Launcher title.
- README → live guide opens in a separate tab.
- When the guide is opened from GitHub and browser policy exposes an opener, the guide may refresh the originating GitHub tab once; the guide remains open.
- The hero GitHub button focuses the originating GitHub window when available; direct opens fall back to a normal new-tab repository link.
- User-created research notes start after the fixed guide sections. Fixed section 17 is the project control center; user-created notes therefore begin at 18.

These behaviors must be verified against the deployed guide before being described as live-verified.

## Current repository-control state

The public repository now has a dedicated control layer:

- `docs/PROJECT-MEMORY.md`
- `docs/PROJECT-GOAL.md`
- `docs/REPOSITORY-MAP.md`
- `docs/CHANGE-CONTROL.md`
- `research/LESSONS.md`
- `research/VALIDATION.md`

The live guide exposes these through **17 — Project Control Center**. Fixed guide sections run through 17; user-created research-note sections begin at 18.

The repository uses one canonical checkpoint directory: `research/checkpoints/`. The earlier case-variant `research/CHECKPOINTS/` path has been removed.

The README and public documentation now describe the repository as public. The README no longer lists a nonexistent `scripts/` directory.


## Current UI preference checkpoint — 25 September 2026

The maintainer explicitly requested that the Open project memory action and the other Project Control Center document links remain transparent by default. The accent should appear as a light translucent treatment only on hover/focus; there should be no persistent solid yellow/orange fill.

The maintainer also requested a compact category sidebar to the left of the main detailed sidebar. The Project Map is the primary navigation rail, ordered as Hydra Launcher → Setup → Build → Security Research → Research → Project Control → Created Notes. Its buttons scroll both the follower sidebar (category heading near the top of its visible scroll area) and the main document (corresponding section heading below the fixed title bar). The Project Map and follower sidebar now use the original guide's visual system: dark page surface, thin muted borders, monospace navigation, transparent controls, panel-soft hover, and restrained orange active states. No glass/card styling is used for either sidebar.

## Current research state

Verified findings currently recorded:

- Hydra/Electron runtime HTTPS activity was observed and requires endpoint/function correlation.
- Community download-source configuration is a separate trust boundary.
- Hydra API-mediated download-source metadata was observed for source IDs `BVnaGLvo` and `w4nVajB6`; this does not prove tracker/peer activity by itself.
- Windows antivirus/AMSI intercepted the EICAR string at the PowerShell command stage; a valid EICAR file/quarantine event was not established.
- No malware/safety verdict has been established.

Next substantive experiment:

- use a legitimate free/open-source artifact;
- capture pre-download process/network/filesystem state;
- perform one controlled download;
- capture post-download differences;
- hash and statically inspect the artifact;
- record Defender/AV results;
- correlate behavior with source code;
- execute only when the artifact is suitable for the controlled test.

## Mistake-prevention memory

Previous project mistakes/near-misses that must not be repeated:

1. **Claiming a UI fix before live confirmation.** Code inspection is not browser verification.
2. **Overlapping CSS rules.** The guide previously accumulated duplicate fixed/sidebar media rules. Keep one authoritative rule per breakpoint.
3. **Duplicate GitHub buttons.** A replacement button was once added without fully removing the older one. Search for duplicates after UI changes.
4. **Navigation JavaScript in the wrong scope.** Navigation code was previously embedded inside the exported research-note HTML string. Keep runtime navigation logic in the main page script only.
5. **Green workflow interpreted as fully clean.** GitHub Pages succeeded while emitting a Node.js 20 deprecation warning. Inspect annotations, not only conclusion.
6. **Outdated documentation.** Several files still described the repository as private after it became public. Run terminology/state consistency checks after structural changes.
7. **Case-only directory divergence.** The repository accumulated both `research/CHECKPOINTS` and `research/checkpoints`. This is unsafe for Windows case-insensitive filesystems. Keep one canonical lowercase path: `research/checkpoints/`.
8. **Repeated fragmented Pages runs.** Rapid sequential commits cause older Pages runs to be cancelled by the concurrency rule. After a batch of changes, verify the newest run rather than judging an intermediate cancelled run.

## Change protocol

Before changing anything:

1. Read this file.
2. Inspect the current target files.
3. Search for related duplicate/legacy code or documentation.
4. Make the smallest coherent change.
5. Check syntax/structure where possible.
6. Review the resulting repository state.
7. Update this memory when the change alters project state, invariants, or workflow.
8. Update the diary/agenda when the change is substantive.
9. Verify GitHub Actions status and annotations for deployment-related changes.
10. Only then report the change as complete.

## Canonical control files

- `docs/PROJECT-MEMORY.md` — AI/maintainer memory and persistent invariants
- `docs/PROJECT-GOAL.md` — goal, scope, phases, and success criteria
- `docs/REPOSITORY-MAP.md` — repository architecture and file responsibilities
- `docs/CHANGE-CONTROL.md` — required change/verification procedure
- `research/LESSONS.md` — mistakes, corrections, and prevention rules
- `research/VALIDATION.md` — current verification matrix
- `research/DIARY.md` — chronological research history
- `research/AGENDA.md` — current and future work
- `research/FINDINGS.md` — supported research findings
- `.github/workflows/pages.yml` — live deployment workflow
- `index.html` — published live guide

## Last known deployment checkpoint

The last confirmed successful GitHub Pages run before the project-control restructuring was workflow run #41 for commit `8e273eaa506f6df4be11d305e58d3e56f284cf84`.

The control-pass HEAD `d9b83fee2ad9a8bf4a1875693a88c765bbc455cb` was then deployed successfully as workflow run **#66**. Its `deploy` check completed with **success** and **0 annotations**.

The published browser behavior is still separate from deployment status: source/deployment success does not by itself count as live browser verification.

## Current control-pass checkpoints

- Project memory and canonical control documents: implemented.
- Live Project Control Center section 17: implemented.
- User-created note numbering moved to section 18+: implemented.
- Public/private documentation consistency audit: implemented.
- Checkpoint directory case cleanup: implemented.
- Workflow runtime maintenance: implemented in `.github/workflows/pages.yml`.
- Control-pass Pages deployment: run #66 succeeded with 0 annotations.
- Live browser behavior: still requires direct exercise after deployment.

## Handoff instruction

A future AI assistant should:

> Read `docs/PROJECT-MEMORY.md`, inspect the current repository, check `research/VALIDATION.md`, then continue from the documented next action. Never assume that an earlier assistant's “fixed” statement means the live behavior was verified.
