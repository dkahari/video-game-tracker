# Frame0 Workflow

This note captures the working Frame0 wireframing workflow we validated in this repo.

The goal is simple:

- generate wireframes with MCP
- keep the result editable in the Frame0 UI
- use native rectangles directly from MCP where possible

## Current Status

As of the latest validation in this repo, the MCP `create_rectangle` tool creates shapes of type `Rectangle`.

That means the earlier `Box` workaround is no longer the default recommendation.

## Working Solution

Use a direct MCP workflow:

- build layout blocks with `create_rectangle`
- add labels and copy with separate `create_text` layers
- adjust positions, sizing, and styling directly on the generated rectangles

This keeps the geometry clean while also leaving the resulting shapes editable in Frame0.

## Recommended Page Setup

Keep one reusable page available in Frame0, for example:

- `Page Base`

That page should include at least:

- any reference elements you want to reuse, such as a heading or spacing guide

Optional:

- a manually-created rectangle if you want a visual style sample
- a text sample if you want a typography reference

## Recommended Generation Pattern

For each new screen:

1. Duplicate `Page Base`
2. Rename the duplicated page to the new screen name
3. Build the screen with `create_rectangle` and `create_text`
4. Review the layout and adjust spacing until the page looks right
5. Tweak rectangle sizing, corners, fill, and stroke directly as needed
6. Re-layer text if needed so labels stay above blocks

This is currently the simplest balance between layout speed and editability.

## What To Avoid

Avoid overcomplicating the workflow with manual rectangle swapping unless a future Frame0 regression brings the old issue back.

Why:

- `create_rectangle` gave cleaner geometry during initial composition
- current validation shows `create_rectangle` now produces native `Rectangle` shapes directly

Also note:

- `create_rectangle` returned `Rectangle` during live testing
- no manual replacement step was needed
- separate text layers are still the easiest way to keep copy editable

## Good Defaults

Use separate text layers for:

- titles
- labels
- placeholders
- card content

Benefits:

- easier to update copy without touching the block shape
- easier to reposition text independently
- less risk of rebuilding a shape just to change words

## Practical Tips

- Build low-fidelity first. Focus on layout, spacing, and information hierarchy before polish.
- Use visible search by default when the screen depends on filtering or browsing.
- Prefer top-level shapes over deep nesting when editability matters.
- If rectangles cover labels, move or recreate the text layers so the copies land on top.
- If the tool behavior changes again, re-run a small disposable page test before rewriting the workflow doc.

## Example Use Cases

This workflow worked well for:

- dashboard wireframes
- library/list screens
- filter-heavy browsing layouts

It should also work for:

- add/edit forms
- detail pages
- settings screens

## Short Version

Use this shorthand:

- create base page manually
- duplicate page
- build screen with `create_rectangle`
- add text separately
- re-layer text if needed
- adjust rectangles directly
