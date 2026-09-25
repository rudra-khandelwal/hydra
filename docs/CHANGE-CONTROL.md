# Change Control

This document defines how changes to the research workspace should be made and verified.

## 1. Start from current state

Before editing:

- read `docs/PROJECT-MEMORY.md`
- inspect the current target file
- inspect related CSS/HTML/JS or documentation
- search for duplicate or legacy implementations

Never patch from an old copy of the file.

## 2. Make one coherent change

Keep each change focused enough that its purpose is obvious.

For live-guide changes, prefer changing:

- the implementation
- the matching navigation/control text
- the corresponding documentation/validation record

together.

## 3. Check the actual result

At minimum:

- inspect the resulting file;
- verify the expected selectors/links/functions exist;
- verify obsolete implementations are gone;
- run syntax/build checks available for the changed artifact;
- inspect the GitHub commit.

For Pages changes:

- inspect the newest workflow run;
- inspect the conclusion;
- inspect annotations/warnings;
- do not treat a cancelled older run as the final status.

## 4. Live behavior rule

Code correctness is not live verification.

For browser behavior, distinguish:

- **Implemented** — source code contains the intended behavior.
- **Deployed** — GitHub Pages successfully deployed the commit.
- **Live-verified** — behavior was actually exercised in the published page.

Only the third may be described as browser-verified.

## 5. Public-release rule

Before every public commit:

- search for secrets and credentials;
- remove raw sensitive logs;
- remove proprietary/copyrighted downloaded files;
- remove unnecessary personal data or machine-specific paths;
- check third-party references;
- ensure research claims are evidence-backed.

## 6. Documentation synchronization

When a change alters project state:

- update `PROJECT-MEMORY.md`;
- update `REPOSITORY-MAP.md) when file structure changes;
- update `research/VALIDATION.md) for verification status;
- update `research/DIARY.md) for substantive research/engineering events;
- update `research/AGENDA.md) when a task is completed or added.

## 7. Commit discipline

Prefer descriptive prefixes:

- `docs:`
- `research:`
- `security:`
- `build:`
- `fix:`
- `chore:`

When multiple commits are required by tooling, the final project-memory update should capture the resulting combined state.
