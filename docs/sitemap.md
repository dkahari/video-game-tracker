# Sitemap

This document maps the planned screens, routes, and core user flows for the Video Game Tracker MVP.

## Route Map

```text
/
|- /games
|  |- /games/new
|  |- /games/:id
|     |- /games/:id/edit
|- /settings
```

## Screen List

### Dashboard

- Route: `/`
- Purpose: provide a quick overview of the library with summary stats and fast paths into the most common actions
- Main content:
  - total games
  - counts by status
  - recently updated games or currently playing games
  - quick action to add a new game

### Game List

- Route: `/games`
- Purpose: act as the main browsing screen for the full collection
- Main content:
  - searchable list or card grid of games
  - status and platform filters
  - links to detail pages
  - action to add a new game

### Add Game

- Route: `/games/new`
- Purpose: let the user create a new game record
- Main content:
  - title
  - platforms
  - status
  - purchase date
  - hours played
  - completion percent
  - genre tags
  - notes
  - save and cancel actions

### Game Detail

- Route: `/games/:id`
- Purpose: show the complete record for one game and make common updates easy
- Main content:
  - core game metadata
  - progress information
  - notes
  - edit action
  - delete action
  - navigation back to the library

### Edit Game

- Route: `/games/:id/edit`
- Purpose: update an existing game record using the same core form structure as create
- Main content:
  - pre-filled game form
  - save and cancel actions
  - validation feedback

### Settings

- Route: `/settings`
- Purpose: hold app-level tools and low-frequency actions that do not belong in the main browsing flow
- Main content:
  - import and export actions later
  - future display or storage settings if needed

## Navigation Direction

Primary navigation should likely include:

- Dashboard
- All Games
- Add Game
- Settings

The exact presentation can be decided during app shell work:

- mobile-friendly bottom navigation
- app bar plus navigation drawer
- responsive combination of both

## Primary User Flows

### Add A New Game

1. User opens dashboard or game list
2. User selects add game
3. User fills out the form
4. User saves
5. User is returned to the game list or detail page

### Update Progress Or Status

1. User opens game list
2. User selects a game
3. User opens edit
4. User updates status, hours, or completion percent
5. User saves and returns to detail or list

### Review Backlog Or Completed Games

1. User opens game list
2. User applies status filter
3. User scans results
4. User opens a game for more detail if needed

### Check Overall Library Health

1. User opens dashboard
2. User reviews totals and status counts
3. User jumps into a list view or add flow from quick actions

## Screen Relationship Notes

- Dashboard is the landing screen but should stay lightweight
- Game list is the main operational screen for browsing and filtering
- Add and edit should share most of their form structure
- Settings should stay minimal until import/export is implemented

## MVP Coverage Check

This sitemap supports the documented MVP by covering:

- dashboard stats
- game list browsing
- add/edit/delete flows
- detail view
- future import/export placement

## Future Screens That Are Explicitly Deferred

- dedicated import flow
- analytics or charts screen
- wishlist screen
- authentication or profile screens
