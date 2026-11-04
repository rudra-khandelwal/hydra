# Five-Message Handoff Cadence

**Current counter:** 3 of 5 user messages since the 4 November 2026 handoff.  
**Current checkpoint:** [4 November 2026 handoff](../research/checkpoints/2026-11-04-download-source-investigation.md)

## Required routine for every AI continuing this project

1. Before work, read the latest dated handoff and this file. Use the counter stored in that handoff.
2. Each new user message about this Hydra project increments the counter by one. A new chat does not reset it.
3. On message **5**, update the current-state document, create/refresh the dated handoff, append the dated project diary, update the agenda if priorities changed, and reset the counter to 0 in the new handoff.
4. Update the handoff earlier whenever verified state, decisions, blockers, safety boundaries, or next actions change, and before ending a session with unfinished work. Preserve the count when doing an early update.
5. Report the documentation commit and its verification to the user. Never state that a write occurred unless GitHub confirms it.

## What the cadence can and cannot guarantee

This is a manual, repository-backed checklist. There is no dependable mechanism here that counts user messages across arbitrary chats and automatically commits to GitHub in the background. Each assistant must carry forward the count from the latest handoff. If a chat starts without this file or the latest handoff, inspect repository history and ask the user only if the count cannot be reconstructed. Do not invent a count or claim automation. No timer-based automation can reliably implement “every fifth conversation message,” so none is used.

A handoff checkpoint is a documentation review; it does not authorize changes to the app checkout, external messages, downloads, installations, execution, merges, releases, or tags.
