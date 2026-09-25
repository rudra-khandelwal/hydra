# HTML Guide Design Record

**File:** `index.html`  
**Public guide:** https://rudra-khandelwal.github.io/hydra/  
**Record date:** 25 September 2026

## Design direction

The guide keeps its existing dark brown/orange research-console theme. New navigation and control UI must look native to that system rather than introducing a second visual language.

Core visual rules:

- dark brown/near-black surfaces
- thin muted borders
- monospace labels for navigation/control surfaces
- orange/gold used as an accent, not as a persistent fill
- transparent or translucent surfaces where possible
- subtle hover/focus feedback instead of heavy filled buttons
- responsive behavior remains a single-page layout with one fixed desktop content sidebar and a mobile slide-out navigation

## Primary navigation

The main sidebar is the detailed section navigator. On desktop it remains fixed while document content scrolls.

Project Map / fixed guide group order:

1. Hydra Launcher
2. Setup
3. Build
4. Security Research
5. Research
6. Project Control
7. Created Notes (dynamic, after fixed sections)

Created research notes continue at section 18+.

## Project Map rail

## Navigation synchronization and repository-link rule — 25 September 2026

The two desktop navigation rails are bidirectionally synchronized:

- Clicking a Project Map category scrolls the main detailed sidebar to that category and scrolls the document to the corresponding content.
- Clicking or scrolling through the main sidebar updates the Project Map's active category.
- The final detailed-sidebar item remains reachable with explicit bottom scroll space.
- The Project Map's **Hydra Launcher** category points to the guide hero/top state, not the Overview section heading.

The hero **GitHub repo** button is a normal external repository link. It must open `https://github.com/rudra-khandelwal/hydra` in a new tab and must not use an opener/referrer bridge that redirects focus back to the GitHub tab from which the live guide was opened. GitHub may naturally render the repository README on its root page; that is repository-page behavior, not a guide-navigation target.

## Current refinement — 25 September 2026

The Project Map uses title-case labels throughout. Its **Hydra Launcher** action targets the guide's hero/top-of-page state (`#guide-top`), matching the main sidebar's **Overview** destination and restoring the fixed title bar at the top of the viewport. The Project Map title has a visible underline to establish it as the navigation rail's heading.

On wide desktop screens, the rail pair is shifted left with explicit configurable spacing so the main detailed sidebar does not sit unnecessarily far to the right. The detailed sidebar itself retains the original visual treatment.

The Project Map is the **primary navigation rail** on sufficiently wide desktop screens. The detailed section sidebar is its **follower** and sits immediately to the right.

Primary Project Map sequence follows the guide's document order:

1. Hydra Launcher
2. Setup
3. Build
4. Security Research
5. Research
6. Project Control
7. Created Notes

The Project Map intentionally uses the **same original sidebar visual language** as the guide: dark page surface, thin muted border, monospace labels, transparent items, panel-soft hover, and orange accent only for active state. It is not a glassmorphism/card-style sidebar.

The follower sidebar retains its original styling from the guide. Its fixed position and independent scrolling are preserved; Project Map interactions only coordinate its scroll position and the main document position.

Each Project Map button:

- scrolls the follower sidebar so the matching category heading is positioned near the top of its visible scroll area;
- scrolls the main document to the corresponding content section below the fixed title bar;
- leaves unused space below the sidebar alone.

The Project Map is hidden below the wide-desktop breakpoint so it cannot crowd the existing responsive layout.

## Control Center action styling

Project Control Center document links are transparent by default. They do not use a persistent yellow/orange fill.

On hover/focus they use a subtle translucent accent background and muted orange border/text. The accent is feedback, not a permanent button fill.

## Live-link operating rule

The maintainer regularly accesses the public GitHub Pages live link after repository updates. This is the expected user verification path.

The project must continue to distinguish:

- **Implemented** — source code contains the intended change.
- **Deployed** — the GitHub Pages workflow published the commit.
- **Live-verified** — the deployed page was actually exercised in the browser.

A repository commit or successful Actions run must never be described as live-verified on its own.

## Implementation guardrails

- Keep the main navigation outside the project-map rail; never nest the rail inside `<nav>`.
- Keep one authoritative save-notes function; do not allow a legacy duplicate function to override it.
- Preserve the existing mobile slide-out navigation.
- Search for duplicate UI elements after navigation/layout changes.
- Keep public-page UI free of long-lived repository write credentials.


## Persistent final UI context

The original dark brown/orange research-console theme is canonical for the entire guide. The Project Map and detailed sidebar must look like members of the same system, not like separate component libraries.

Canonical visual tokens are defined in project memory. The core rule is: dark surfaces, thin muted borders, monospace navigation labels, transparent controls, panel-soft hover, and restrained orange active/focus treatment. Do not introduce glassmorphism.

The Project Map is the primary rail on wide desktop. The detailed 250px sidebar is the follower. Project Map order is Hydra Launcher, Setup, Build, Security Research, Research, Project Control, Created Notes.

Navigation is bidirectional. Project Map clicks update the detailed sidebar and main document. Detailed-sidebar navigation and scroll-spy state update the Project Map active category. Hydra Launcher targets #guide-top, which restores the fixed title bar and hero. The last detailed-sidebar item must remain reachable.

The hero GitHub repository control is a normal new-tab link to https://github.com/rudra-khandelwal/hydra with noopener/noreferrer semantics and no opener/focus bridge.

The maintainer checks the public Pages URL after repository updates. Implemented, Deployed, and Live-verified remain separate states.


## Static-page security boundary

The guide is intentionally a static GitHub Pages application. Client-side JavaScript is appropriate for navigation, animation/state synchronization, rich Research Notes, validation, and other UI behavior.

The guide must not accept a GitHub personal access token or perform repository Contents writes directly from the browser. Maintainer file publishing uses a handoff to GitHub's authenticated upload UI. A separate backend is required only when the project needs authenticated server-side persistence, GitHub App/OAuth operations, or cross-device Research Note storage.
