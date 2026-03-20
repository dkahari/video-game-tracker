# Frame0 Workflow

This note captures the working Frame0 wireframing workflow we validated in this repo.

The goal is simple:

- generate wireframes with MCP
- keep the result editable in the Frame0 UI
- avoid shape types that are hard to drag or tweak later

## Problem

Using the MCP `create_rectangle` tool creates shapes of type `Box`.

In practice, those `Box` shapes were harder to manipulate manually in the Frame0 editor than rectangles created directly in the UI. Text was still easy to edit, but the generated boxes were awkward to drag, resize, or tweak.

Manual rectangles created inside Frame0 showed up as type `Rectangle` and behaved better in the editor.

## Working Solution

Use a hybrid workflow:

- build the layout with MCP `create_rectangle` for cleaner geometry
- replace those generated boxes with native Frame0 rectangles after the layout is finalized

This gives better first-pass alignment while still ending with editable native `Rectangle` shapes.

## Recommended Page Setup

Keep one reusable page available in Frame0, for example:

- `Page Base`

That page should include at least:

- one plain manually-created rectangle

Optional:

- a second manually-created shape if you want a different default style
- a text sample if you want a typography reference

## Recommended Generation Pattern

For each new screen:

1. Duplicate `Page Base`
2. Rename the duplicated page to the new screen name
3. Find the seeded native rectangle on that page
4. Build the screen normally with `create_rectangle` and `create_text`
5. Review the layout and adjust spacing until the page looks right
6. Duplicate the native rectangle enough times to replace the generated `Box` shapes
7. Copy the final geometry and styling onto those native rectangle clones:
   - position
   - width and height
   - fill and stroke
   - corner radius
8. Delete the original `Box` shapes
9. Re-layer text if needed so labels are above the new rectangles

This is currently the best balance between layout accuracy and editability.

## What To Avoid

Avoid doing the whole layout from duplicated native rectangles too early if precise spacing matters.

Why:

- clone-first layout work was more likely to drift out of alignment
- `create_rectangle` gave cleaner geometry during initial composition
- the best results came from swapping to native rectangles after the layout was already stable

Also note:

- `create_rectangle` produced `Box`
- duplicated manual rectangles stayed `Rectangle`
- `Rectangle` behaved better in the editor during testing

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

- Keep the original seed rectangle during layout generation so it is available for the end-of-process swap.
- Once the page is built, it is fine to delete or hide the seed rectangle if you do not want it hanging around on the final page.
- If you prefer to keep it, move the seed rectangle off to the side so it stays available as a local template.
- Build low-fidelity first. Focus on layout, spacing, and information hierarchy before polish.
- Use visible search by default when the screen depends on filtering or browsing.
- Prefer top-level shapes over deep nesting when editability matters.
- If the new native rectangles cover the labels, duplicate the text layers after the swap so the copies land on top, then remove the older text layers underneath.

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
- place one native rectangle on it
- duplicate page
- build screen with `create_rectangle`
- duplicate native rectangle
- reshape clones to match final boxes
- delete generated boxes
- add text separately
- re-layer text if needed
