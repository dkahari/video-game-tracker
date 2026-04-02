# Decision Log

Use this file to record short architecture or workflow decisions so the project keeps its memory over time.

## Template

Copy this format for new entries:

```md
## YYYY-MM-DD - Decision title

- Context:
- Decision:
- Why:
- Follow-up:
```

## 2026-03-23 - Retire the Frame0 rectangle workaround

- Context: The project had been using a hybrid Frame0 workflow because earlier testing showed MCP `create_rectangle` returning `Box` shapes that were harder to edit than native `Rectangle` shapes.
- Decision: Stop recommending the manual rectangle replacement workflow and use `create_rectangle` directly as the default wireframing path.
- Why: A live validation on 2026-03-23 confirmed that `create_rectangle` now returns `Rectangle`, which removes the main reason for the workaround and simplifies wireframe generation.
- Follow-up: Keep the Frame0 workflow doc aligned with current tool behavior and re-test with a disposable page if rectangle behavior appears to regress.

## 2026-03-17 - Share API contracts but keep internal models separate

- Context: While exploring a layered architecture for the `library` context, the project needed a clear rule for how frontend and backend type sharing should work in a single repo.
- Decision: Use `shared/contracts/` for transport-level request and response DTOs, allow both frontend and backend presentation code to import those contracts, and keep frontend view models plus backend domain and persistence models separate.
- Why: This preserves an intentional API contract without coupling the frontend to backend source layout or leaking backend internals across the boundary.
- Follow-up: Start with `shared/contracts/library.ts` when the `library` context is implemented and avoid direct frontend imports from backend folders.

## 2026-03-17 - Use a library-first layered architecture for the MVP

- Context: The project started with a simpler feature-based frontend direction, but the architecture discussion introduced a layered and bounded-context approach that the MVP can still benefit from if applied selectively.
- Decision: Treat `library` as the first real bounded context, organize the frontend around `app`, `contexts`, and `shared`, and use layered backend-oriented language for `library` without fully scaffolding the other contexts yet.
- Why: This gives the project cleaner boundaries and a better long-term shape while keeping the MVP focused and avoiding architecture for architecture's sake.
- Follow-up: Apply the pattern first in `library`, keep `sessions`, `reviews`, and `sync` documented as future or stretch contexts, and only split deeper into layers or subfolders when the code earns it.

## 2026-03-16 - Create collaboration scaffolding before implementation

- Context: The project is still in an early planning stage, and the goal is to use Codex intentionally rather than jumping straight into code.
- Decision: Add repo-level working rules and lightweight project reference docs before starting implementation.
- Why: This creates a repeatable workflow, keeps project decisions visible, and reduces the need to restate expectations each session.
- Follow-up: Fill in architecture decisions and the active Jira ticket before beginning the first build task.

## 2026-03-16 - Use Vuetify as the initial Material Design library

- Context: The project goal explicitly calls for Vue plus Google's Material Design style, and the app is still pre-implementation.
- Decision: Use Vuetify as the initial UI framework.
- Why: It is the most established Material-oriented option in the Vue ecosystem and lowers setup friction for app shell, forms, cards, and navigation.
- Follow-up: Confirm the generated project structure works cleanly with Vuetify during setup.

## 2026-03-16 - Start with composable-based state and localStorage persistence

- Context: The MVP is a single-user app with straightforward CRUD and filtering requirements.
- Decision: Use a shared composable for game state and a small storage wrapper around `localStorage` instead of introducing Pinia or IndexedDB immediately.
- Why: This keeps the learning surface smaller, matches MVP complexity, and leaves room to grow later if state logic becomes harder to maintain.
- Follow-up: Re-evaluate once we have multiple views mutating shared state.

## 2026-03-16 - Make the dashboard the home route

- Context: The app needs both a dashboard and a game list, and the original project idea includes simple stats as part of the product experience.
- Decision: Use `/` for the dashboard and `/games` for the full library.
- Why: This gives the app a more intentional landing experience and keeps the list page focused on browsing and filtering.
- Follow-up: Keep the dashboard lightweight so it does not delay core CRUD work.

## 2026-03-16 - Use TypeScript from the start

- Context: The app has a defined data model, multiple routed views, and a desire to practice good architecture before implementation.
- Decision: Use TypeScript in the Vue project from the initial setup.
- Why: It will help keep the game model, route-level logic, and storage interactions consistent as the project grows.
- Follow-up: Define shared game and storage types early during project setup.
