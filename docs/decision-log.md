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
