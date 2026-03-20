# Ticket Tracker

This file gives the repo a lightweight view of progress alongside Jira.

## Current

- Planning and architecture baseline
- Goal: finish core planning docs before implementation starts
- Frame0 wireframing workflow is active for dashboard, library, and add-game screen exploration
- Current UI direction:
  - `Dashboard Wireframe v4`
  - `Games Library Wireframe v1`
  - `Add Game Wireframe v2` as the cleaner geometry reference
  - `Add Game Wireframe v3` as the native-rectangle/editable hybrid test

## Next Up

- Choose the first implementation ticket from Jira
- Initialize the Vue + Vite project once the architecture baseline feels right
- Create wireframes or a simple screen sketch if you want one more UX planning step before setup
- In the next session, decide whether to:
  - keep the hybrid Frame0 workflow
  - simplify it further
  - or fix the Frame0 MCP rectangle bug directly
- If continuing wireframes, use [`docs/frame0-workflow.md`](C:\Users\dkaha\Repos\video-game-tracker\docs\frame0-workflow.md) as the starting reference

## Completed

- Added repo collaboration and project reference files
- Documented the initial architecture baseline and default technical decisions
- Confirmed TypeScript is part of the initial project setup
- Added the project brief
- Added the initial data model reference
- Added the sitemap and screen reference
- Validated Frame0 MCP connectivity and built working wireframe pages in Frame0
- Documented the Frame0 workflow and workaround in [`docs/frame0-workflow.md`](C:\Users\dkaha\Repos\video-game-tracker\docs\frame0-workflow.md)
- Confirmed a practical hybrid workflow:
  - duplicate the base page first
  - build layout accuracy with `create_rectangle`
  - replace final `Box` shapes with native `Rectangle` clones
  - re-layer text if needed

## Blocked

- None

## Notes

- Jira remains the source of truth for ticket management.
- This file is a quick project memory for in-repo context and handoff.
- When starting a ticket, replace `Current` with the Jira key and short goal.
- This planning entry can be replaced by the first active implementation ticket.
- The main unresolved UX/tooling question is whether fixing the MCP rectangle behavior is worth more than continuing with the documented workaround.
