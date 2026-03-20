# Architecture Notes

This document captures the current technical direction for the Video Game Tracker project. It is meant to stay practical, lightweight, and easy to evolve as the app grows.

## Project Goal

Build a personal video game tracker as a Vue-based Progressive Web App using Material Design principles. The app should help track games that were bought, played, completed, or dropped, while also serving as a portfolio-quality learning project.

## Primary User

- A single primary user: you, tracking a personal game collection
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

## Architecture Direction

The project will use a modest modular-monolith structure with:

- a Vue frontend organized by app shell, contexts, and shared code
- a layered backend-oriented design language for domain boundaries
- a small shared contract area for transport-level request and response types
- `library` as the first and only context we actively structure around in the MVP
- other contexts documented as future expansion areas rather than immediate implementation commitments

This means we are adopting the shape of layered architecture where it helps, without forcing every future context into existence before the app needs it.

## Contract Sharing Rule

Share contracts, not internal models.

That means:

- shared request and response DTOs may live in `shared/contracts/`
- frontend code may use shared contracts for API typing
- backend presentation code may use shared contracts for endpoint typing
- frontend view models should stay frontend-specific
- backend domain entities and persistence models should stay backend-specific
- frontend code should not import DTOs directly from backend source folders

This keeps API shapes intentional without tightly coupling the frontend to backend implementation details.

## Current Context Strategy

### Primary MVP Context

- `library`
  - owns the game collection
  - owns game status and progress fields
  - owns list, detail, create, update, and delete flows
  - owns filtering and summary behavior derived from the library

### Deferred Contexts

These are useful future directions, but they are not first-wave implementation targets:

- `sessions`
  - stretch goal for tracked play sessions and active play timing
- `reviews`
  - stretch goal for ratings and written review flows
- `sync`
  - stretch goal for import or external account integrations

For the MVP, these should be treated as placeholders in planning docs, not as folders we must fully scaffold on day one.

## Initial Technical Decisions

- Framework: Vue 3
- Language: TypeScript
- Build tool: Vite
- UI library: Vuetify
- Routing: Vue Router
- State management: start with composables and context-local state instead of introducing Pinia
- Persistence: `localStorage` with a versioned storage wrapper
- PWA approach: use Vite PWA tooling for manifest and service worker support
- Home route: use the dashboard as `/`, with the full game library on `/games`

## Why This Direction

- The app is still MVP-sized, so heavy architecture would be mostly ceremony.
- A library-first context gives us one bounded area to practice cleaner separation.
- Feature-first frontend organization keeps Vue code easy to navigate.
- Layered backend-style thinking helps separate business rules from storage concerns, even if the first implementation is local-only.
- Keeping future contexts documented now makes expansion easier without overbuilding them today.

## Frontend Direction

The frontend should be organized around three top-level areas:

- `app/`
  - app shell, router, providers, layouts, and startup wiring
- `contexts/`
  - user-facing feature areas, starting with `library`
- `shared/`
  - reusable UI primitives, shared composables, utilities, styles, and storage helpers

Suggested frontend shape:

```text
src/
  app/
    router/
    providers/
    layouts/
    App.vue
    main.ts
  contexts/
    library/
      views/
      components/
      composables/
      api/
      types/
      mappers/
  shared/
    ui/
    components/
    composables/
    styles/
    utils/
  pwa/
```

Suggested shared contract shape:

```text
shared/
  contracts/
    library.ts
```

### Frontend Layer Guidance

- `views/` should hold route-level pages such as library list, game detail, and game form flows.
- `components/` should hold library-specific UI pieces such as cards, filter bars, and dialogs.
- `composables/` should hold feature logic such as loading games, saving changes, and managing filters.
- `api/` should isolate data access, even if the first version talks to a local storage adapter instead of a remote backend.
- `types/` should hold DTO or feature-local TypeScript shapes.
- `mappers/` are optional and should only appear when raw data needs shaping for the UI.

### Frontend Data Shape Guidance

The frontend may import shared DTO contracts, but it should still be free to map them into UI-facing shapes. A healthy flow is:

```text
shared contract DTO
  ->
frontend mapper
  ->
frontend view model
```

This keeps the UI flexible even when the API contract is stable.

## Backend And Domain Direction

Even if the MVP starts as a frontend-first app with browser storage, the project should think in terms of backend layers inside the `library` context:

- `presentation`
  - transport-facing contracts and request handling concerns
- `application`
  - use cases and orchestration
- `domain`
  - business rules, entities, value objects, and repository interfaces
- `infrastructure`
  - storage and integration details

Suggested backend-oriented shape for `library`:

```text
backend/src/
  app/
  contexts/
    library/
      presentation/
      application/
      domain/
      infrastructure/
  shared/
```

### Layer Responsibilities

- `presentation` receives input and returns output
- `application` coordinates workflows such as add game, update status, or delete game
- `domain` owns the game library concepts and validation rules
- `infrastructure` handles persistence details such as storage adapters or future API/database access
- `shared/contracts` holds transport-level shapes that both frontend and backend are allowed to agree on

For the MVP, these layers should stay lightweight. We do not need to create every subfolder until the code actually earns it.

### Shared vs Separate Types

Good candidates for shared contracts:

- request DTOs
- response DTOs
- transport-level enums that are part of the API contract

Types that should remain separate:

- frontend view models
- backend domain entities
- backend persistence models
- backend-only validation internals

## State And Data Flow

The working flow should be:

- route-level views coordinate page behavior
- feature composables orchestrate reads, writes, and UI state
- a storage or repository adapter handles persistence
- domain-oriented rules stay out of presentational components
- shared UI components remain mostly presentational

If local state and storage logic become hard to manage, that is the point to evaluate Pinia or a more explicit application service layer.

## Route Direction

- `/`: dashboard
- `/games`: library list
- `/games/new`: add game
- `/games/:id`: game detail
- `/games/:id/edit`: edit game
- `/settings`: reserved for import/export and future options

These routes still serve the library context first, even though the landing screen is a dashboard.

## Data Model Direction

The MVP data model remains centered on the game library and should align with [`docs/data-model.md`](c:\Users\dkaha\Repos\video-game-tracker\docs\data-model.md).

Core fields currently expected:

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

## Folder Direction

The current target structure should be treated as a direction, not a checklist:

- `src/app/` for shell, router, providers, and startup
- `src/contexts/library/` for the first real bounded context on the frontend
- `src/shared/` for reusable UI and utilities
- `src/pwa/` for service worker registration and offline-related code
- `shared/contracts/` for deliberate transport-level contracts such as `library.ts`

If a backend or service layer is added in-repo later, mirror the `library` context with presentation, application, domain, and infrastructure layers.

## Expected Build Order

1. Initialize Vue + Vite project with TypeScript
2. Install and configure Vuetify
3. Add router and app shell
4. Define the library data model and storage wrapper
5. Create the frontend `library` context structure
6. Implement library list and add game flows
7. Implement detail, edit, and delete flows
8. Add dashboard summary behavior from library data
9. Add PWA manifest and service worker support
10. Reassess whether any additional context has earned implementation

## Deferred Decisions

- Whether Pinia is needed later
- Whether `localStorage` should be replaced by IndexedDB
- Whether to formalize repository and service interfaces immediately or only after core screens exist
- Whether dashboard behavior belongs inside the `library` context or deserves its own context later
- When to introduce `sessions`, `reviews`, and `sync` beyond planning docs

## Update Rule

If a ticket changes technical direction, storage shape, route strategy, context boundaries, or major libraries, update this file in the same task.
