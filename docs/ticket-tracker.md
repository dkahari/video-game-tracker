# Ticket Tracker

This file gives the repo a lightweight view of progress alongside Jira.

## Current

- Implementation bootstrap complete
- Active repo state:
  - Vue 3 + TypeScript + Vite scaffold is now in place
  - ESLint is configured for Vue single-file components and TypeScript files
  - The stock starter demo was replaced with a project-specific placeholder screen
  - The next setup slice is Vuetify, app shell structure, and router wiring
- Current UI references remain:
  - `Dashboard Wireframe v4`
  - `Games Library Wireframe v1`
  - `Add Game Wireframe v2` as the cleaner geometry reference
  - `Add Game Wireframe v3` as the earlier native-rectangle/editable hybrid test
  - `Game Detail Wireframe v1`
  - `Edit Game Wireframe v1`
  - `Settings Wireframe v1`

## Next Up

- Install and configure Vuetify
- Create the base app shell with navigation placeholders
- Configure Vue Router using the planned MVP routes
- Begin the first `library` context slice after the shared setup layer is ready

## Completed

- Added repo collaboration and project reference files
- Documented the initial architecture baseline and default technical decisions
- Confirmed TypeScript is part of the initial project setup
- Added the project brief
- Added the initial data model reference
- Added the sitemap and screen reference
- Validated Frame0 MCP connectivity and built working wireframe pages in Frame0
- Documented the Frame0 workflow in [`docs/frame0-workflow.md`](C:\Users\dkaha\Repos\video-game-tracker\docs\frame0-workflow.md)
- Re-validated `create_rectangle` in Frame0 and confirmed it now returns native `Rectangle` shapes during live testing
- Simplified the recommended Frame0 workflow:
  - duplicate the base page first
  - build layout directly with `create_rectangle`
  - add text separately
  - re-layer text if needed
- Created `Game Detail Wireframe v1` in Frame0 with back, edit, and delete actions plus overview, status, notes, progress, tags, and cover sections
- Created `Edit Game Wireframe v1` in Frame0 with pre-filled form fields, save/cancel flow, validation feedback, and edit-state cues
- Created `Settings Wireframe v1` in Frame0 with local data, import/export placeholders, storage info, and future-preferences sections
- Covered the main sitemap screen set with first-pass Frame0 wireframes
- Refined the `Games Library` filter sidebar with more realistic filter groups and sample active selections
- Initialized the project with the Vue 3 + TypeScript + Vite starter
- Replaced the default Vite demo with a project-specific bootstrap screen
- Updated the root README with local setup and build commands
- Added ESLint with Vue + TypeScript support and project lint scripts

## Blocked

- None

## Notes

- Jira remains the source of truth for ticket management.
- This file is a quick project memory for in-repo context and handoff.
- When starting a ticket, replace `Current` with the Jira key and short goal.
- This planning entry can be replaced by the first active implementation ticket.
- The previous Frame0 rectangle workaround is no longer the default guidance after the 2026-03-23 validation.
- Mobile-specific wireframes and responsive layout adjustments should be revisited in a later pass.
