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

Fixed guide group order:

1. Hydra Launcher
2. Setup
3. Build
4. Research
5. Security Research
6. Project Control
7. Created Notes (dynamic, after fixed sections)

Created research notes continue at section 18+.

## Project Map rail

The Project Map is now the **primary navigation rail** on sufficiently wide desktop screens. The detailed section sidebar is its **follower** and sits immediately to the right of it.

Primary Project Map sequence follows the guide's document order:

1. Hydra Launcher
2. Setup
3. Build
4. Security Research
5. Research
6. Project Control
7. Created Notes

Each Project Map button performs two coordinated actions:

- scrolls the follower sidebar so the matching category heading is positioned at the top of the sidebar's visible scroll area; any remaining empty space below is left alone;
- scrolls the main document to the corresponding content section, with the section heading aligned below the fixed title bar.

The Project Map uses the stronger themed panel treatment. The follower sidebar uses a quieter translucent treatment and is explicitly labeled as following the Project Map.

The Project Map is hidden below the wide-desktop breakpoint so it cannot crowd the main sidebar or content on smaller screens.

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
