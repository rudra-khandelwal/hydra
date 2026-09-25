# Lessons, Mistakes & Prevention

This file is a deliberate error-prevention log.

The purpose is not blame. The purpose is to prevent the same failure mode from recurring.

## L-001 — Do not call an unverified live UI fix complete

**Observed mistake:** A sidebar implementation was described as fixed while the user still observed the old scrolling behavior.

**Prevention:** Separate implementation, deployment, and live verification. Do not collapse them into one status.

## L-002 — Avoid overlapping responsive CSS

**Observed mistake:** Multiple desktop sidebar media rules accumulated, making it unclear which rule was authoritative.

**Prevention:** One base rule plus one authoritative rule set per breakpoint. Search for duplicate selectors after responsive changes.

## L-003 — Remove old UI controls when adding replacements

**Observed mistake:** A new GitHub repository button was added while the previous title-bar button remained.

**Prevention:** Search for the old class/text after every UI replacement and verify the intended count of controls.

## L-004 — Keep runtime scripts out of exported content

**Observed mistake:** Navigation JavaScript was embedded inside the research-note export string.

**Prevention:** Keep page runtime controllers in the main document script. Exported HTML should contain only export-specific code.

## L-005 — Green is not the same as clean

**Observed mistake:** A successful Pages run still carried a Node.js 20 deprecation annotation.

**Prevention:** Inspect workflow annotations and action runtime warnings after every deployment-related change.

## L-006 — Audit documentation after visibility changes

**Observed mistake:** Multiple documents still described the repository as private after the repository became public.

**Prevention:** After state changes, search the entire repository for contradictory terminology such as “private repository”, “before making public”, and similar stale statements.

## L-007 — Avoid case-only directory variants

**Observed mistake:** Both `research/CHECKPOINTS/` and `research/checkpoints/` existed.

**Why it matters:** Windows commonly uses case-insensitive filesystems, so case-only directory variants are a practical source of checkout/path problems.

**Prevention:** Maintain one canonical lowercase `research/checkpoints/` path.

## L-008 — Batch related validation

**Observed mistake:** Multiple rapid commits caused intermediate GitHub Pages runs to be cancelled by the workflow's concurrency policy.

**Prevention:** Make coherent batches where possible and judge the newest run after the batch settles.

## L-009 — Keep public claims smaller than the evidence

**Observed mistake:** There was a risk of describing API metadata or an AV/AMSI control observation more broadly than the evidence supported.

**Prevention:** Preserve the exact observation, state what it does not establish, and record the next experiment.

## Maintenance rule

Add a new lesson whenever a recurring mistake, ambiguity, or tooling failure teaches a reusable project rule.


## L-010 — Never place a literal closing script tag inside page JavaScript strings

**Observed mistake:** The research-note export function contained a literal `</script>` inside a JavaScript template/string expression. The HTML parser interpreted that sequence as the end of the page's real script element, causing the remainder of the JavaScript source to appear visibly on the live page.

**Prevention:** When JavaScript constructs HTML containing a script element, do not place a literal closing `</script>` sequence in the surrounding page source. Build it safely (for example by splitting the string as `</scr`+`ipt>`), and verify that the published page does not expose source code as text.

## L-011 — Interactive action links need explicit hover/focus treatment

**Observed mistake:** Primary and secondary action controls had different visual states; only the primary control appeared filled while secondary controls did not visibly enter the same hover/focus state.

**Prevention:** Define explicit `:hover` and `:focus-visible` states for non-danger action controls and verify keyboard focus as well as pointer hover.


## L-012 — Protect the last fixed-sidebar item from overlap and reachability problems

**Observed mistake:** The final detailed-sidebar option became difficult or impossible to click after the Project Map was positioned nearby.

**Prevention:** Keep the Project Map outside the main nav, keep the detailed sidebar above overlapping layers, preserve explicit bottom scroll padding, and test the final item as a real click target.

## L-013 — Secondary navigation must be bidirectionally synchronized

**Observed mistake:** Project Map clicks moved the detailed sidebar and document, but detailed-sidebar navigation did not update the Project Map.

**Prevention:** Treat both rails as one navigation state. Main-sidebar clicks and scroll-spy updates must synchronize the active Project Map category.

## L-014 — Do not let an opener/referrer bridge hijack a normal repository link

**Observed mistake:** The hero GitHub button could focus the originating GitHub tab, making the repository README position appear to be the button destination.

**Prevention:** Keep the hero repository control as a normal external new-tab link without opener/focus redirection.

## L-015 — New navigation must inherit the canonical theme

**Observed mistake:** The secondary Project Map temporarily introduced a glass/card treatment that diverged from the original guide sidebar.

**Prevention:** Reuse the canonical dark surfaces, muted borders, monospace labels, transparent controls, panel-soft hover, and restrained orange active treatment.


## L-016 — Never collect repository write tokens on a public static page

**Observed mistake:** The live guide temporarily exposed a maintainer upload form that accepted a fine-grained GitHub token and called the GitHub Contents API directly from public client-side JavaScript.

**Why it matters:** The token was not persisted, but the page still became a credential-handling boundary. Any XSS, compromised dependency, malicious browser extension, accidental paste, or future client-side mistake could expose a repository write credential. It also bypassed the project's intended review/change-control boundary by writing directly to main.

**Correction:** Remove token collection and direct Contents API writes from the public page. The guide now validates the intended file/folder locally and opens GitHub's authenticated upload interface. GitHub account/repository permissions remain the actual write boundary.

## L-017 — Browser-local research notes are not repository persistence

**Observed gap:** Research Notes are stored in browser localStorage, so they persist only in the current browser profile.

**Prevention:** Describe them as browser-local unless a real backend/GitHub synchronization layer is implemented. Do not call them cross-device or server-persistent data.


## L-018 — Remove legacy responsive overrides

**Observed mistake:** An older mobile sidebar media rule remained alongside the newer responsive foundation. Later rules overrode some properties but not all, creating a hidden conflict and making the effective mobile behavior harder to reason about.

**Prevention:** Keep one authoritative responsive rule set per breakpoint. Remove superseded media blocks instead of relying on cascade order to override them.


## L-019 — Current-state docs must follow the current HEAD

**Observed mistake:** Deployment notes in the project-memory and validation records still pointed at older Pages runs after newer repository commits had already superseded them.

**Prevention:** When a deployment or audit changes repository state, refresh all current-state references to the newest confirmed HEAD/run. Keep older run numbers only where they are explicitly historical.
