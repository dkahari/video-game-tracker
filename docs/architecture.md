# Architecture Notes

This document captures the initial technical baseline for the Video Game Tracker project. It should stay concise, practical, and easy to update as the app evolves.

## Project Goal

Build a personal video game tracker as a Vue-based Progressive Web App using Material Design principles. The app should help track games that were bought, played, completed, or dropped, while also serving as a portfolio-quality learning project.

## Primary User

- A single primary user: you, acting as a gamer tracking a personal collection
- Main jobs:
  - add games to a library
  - update status and progress over time
  - review backlog and completed games
  - get a quick sense of totals and current activity

## MVP Scope

- View a list of games
- Add a new game
- Edit and delete a game
- Track status such as backlog, playing, completed, and dropped
- Store data locally in the browser
- Support installable PWA basics
- Show simple summary stats

## Non-Goals For Initial Build

- User accounts or cloud sync
- Online game database integration
- Social features
- Advanced analytics
- Complex offline conflict handling

## Initial Technical Decisions

- Framework: Vue 3
- Language: TypeScript
- Build tool: Vite
- UI library: Vuetify
- Routing: Vue Router
- State management: start with a simple app-level composable instead of Pinia
- Persistence: `localStorage` with a versioned storage wrapper
- PWA approach: use Vite PWA tooling for manifest and service worker support
- Home route: use the dashboard as `/`, with the full game library on `/games`

## Why These Defaults

- Vuetify is the most direct fit for a Vue project that wants Material Design quickly.
- TypeScript fits the project well because the app has a clear data model and several screens that will benefit from shared type safety.
- A composable keeps early state management simple and reduces setup overhead.
- `localStorage` is enough for an MVP and keeps persistence easy to understand.
- Vite PWA tooling gives a cleaner path to installability than hand-rolling service worker behavior.
- A dashboard home screen gives the app a stronger product feel while still keeping the game list one click away.

## App Areas

- Dashboard: summary stats, recently added or currently playing items, quick actions
- Game list: all games, search, filters, status browsing
- Game detail: full record for a single game
- Add/edit game form: create or update a game entry
- Settings or tools: import/export and future app preferences

## Route Direction

- `/`: dashboard
- `/games`: game list
- `/games/new`: add game
- `/games/:id`: game detail
- `/games/:id/edit`: edit game
- `/settings`: reserved for import/export and future options

## Data Model Direction

Initial game fields expected for MVP:

- `id`
- `title`
- `platforms`
- `status`
- `purchaseDate`
- `hoursPlayed`
- `completionPercent`
- `genreTags`
- `notes`
- `createdAt`
- `updatedAt`

Planned statuses:

- `backlog`
- `playing`
- `completed`
- `dropped`

Suggested storage wrapper shape:

- `version`
- `games`
- `updatedAt`

This should eventually be represented with TypeScript types or interfaces in the app code.

## State And Data Flow

- UI components should remain mostly presentational
- Route-level views should coordinate page behavior
- A shared composable should own game collection reads and writes
- Persistence should be handled in one place instead of directly inside components
- If the composable becomes difficult to manage, that is the point to consider Pinia

## Folder Direction

Once the app is created, favor a structure similar to:

- `src/app/` for app shell, router, providers, and startup code
- `src/features/games/` for game list, detail, form, and model logic
- `src/features/dashboard/` for dashboard UI and stats
- `src/shared/` for reusable UI, utilities, and storage helpers

This is a direction, not a rigid rule. We can simplify if the generated project starts smaller.

## Expected Build Order

1. Initialize Vue + Vite project
2. Initialize the project with TypeScript enabled
3. Install and configure Vuetify
4. Add router and app shell
5. Define the game model and local storage wrapper
6. Implement game list and add form
7. Implement edit/delete and detail flow
8. Add dashboard stats
9. Add PWA manifest and service worker support

## Deferred Decisions

- Whether to introduce Pinia later
- Whether to use IndexedDB instead of `localStorage`
- Whether import/export belongs in settings or on the game list page
- Whether dashboard should include charts or stay stat-card based

## Update Rule

If a ticket changes technical direction, storage shape, routes, or major libraries, update this file in the same task.
