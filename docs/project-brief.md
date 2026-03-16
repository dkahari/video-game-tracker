# Project Brief

## Project Name

Video Game Tracker

## Summary

Video Game Tracker is a personal Progressive Web App for tracking video games that have been bought, played, completed, or dropped. The project is also a learning and portfolio app focused on Vue, TypeScript, Material Design, and PWA fundamentals.

## Why This Project Exists

- Track a personal game library in one place
- Practice building a real app with Vue and TypeScript
- Learn how to build and ship a Progressive Web App
- Create a portfolio project with clear product and architecture decisions

## Primary User

The primary user is you: a gamer who wants to keep a clean record of owned games, current progress, and completed titles.

## User Goals

- Add a game after buying or starting it
- See which games are in the backlog
- Mark a game as playing, completed, or dropped
- Track simple progress such as hours played or completion percent
- Review quick stats about the library

## Target Platforms

- Desktop browsers
- Mobile browsers
- Installable PWA on supported devices

## Tech Direction

- Vue 3
- TypeScript
- Vite
- Vuetify for Material Design
- Vue Router
- Local browser persistence with `localStorage`
- PWA support through Vite-compatible tooling

## MVP Features

- Dashboard with summary stats
- Game list view
- Add game form
- Edit and delete game actions
- Game detail view
- Status tracking: backlog, playing, completed, dropped
- Progress tracking: hours played and completion percent
- Local persistence across reloads
- Basic installable PWA support

## Stretch Ideas

- Import and export game data
- Platform-specific filtering and richer search
- Cover art support
- Sorting options such as recently updated or most played
- Wishlist or unowned game tracking
- Cloud sync or account support

## Non-Goals For MVP

- Multi-user support
- Online sync
- External game database integration
- Social/community features
- Advanced analytics dashboards

## Success Criteria

The project is successful if:

- it works well as a personal tracker on desktop and mobile
- the core CRUD flow feels smooth and reliable
- data persists locally without confusion
- the app can be installed as a PWA
- the codebase is organized enough to extend without major rewrites

## Delivery Approach

- Start with planning and architecture
- Build the smallest useful vertical slices first
- Keep implementation aligned with Jira tickets
- Document important decisions as they are made
