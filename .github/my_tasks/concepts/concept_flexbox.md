# Flexbox — Modern Layout System

Source transcript: `course_content/FLEXBOX/flexbox_transcript.txt`
Practice exercises: `EX 9.0 Display Flex`, `EX 9.1 Flex Direction`

## The problem this solves

Before Flexbox, laying out a page in columns/rows meant hacks: HTML `<table>` elements used purely for
styling (semantically wrong — tables should only hold tabular data), `display: inline-block` (fiddly
alignment), `position: absolute` (inflexible, breaks as content changes), or `float` (powerful for
wrapping text around images, but a "hack" for full-page layout — not what it was designed for).
**Flexbox** is a layout system built specifically for arranging boxes in a row or column, added because
the web outgrew the old "newspaper/magazine" layout model (inline/block/float) that HTML/CSS originally
borrowed from print design.

---

## 1. Turning on Flexbox (`EX 9.0 Display Flex`)

- Wrap the elements you want laid out inside a parent container (e.g. `<div class="container">`).
- Set `display: flex` on that **container** — not on the children.
- The moment a container is `flex`, **all the old display rules for its children are thrown out the
  window**. It doesn't matter that a `<div>` is normally block-level or a `<li>` is normally list-item —
  Flexbox takes over and lays them out in a row by default, sized to fit their content.
- **`gap`** adds spacing between the flexed items — `gap: 10px` (static) or `gap: 1rem` (scales with the
  root font-size, same `rem` unit from the font-properties lesson).

```css
.container {
  display: flex;
  gap: 10px;
}
```

### `flex` vs `inline-flex` (container's own box behavior)

Same distinction as `display: block` vs `display: inline-block`, just applied to the *container itself*
(the children's layout inside is unaffected either way):

| | `display: flex` | `display: inline-flex` |
|---|---|---|
| Container sizing | **Full width** — behaves like `display: block` | **Shrinks to fit content** — behaves like `display: inline-block` |
| Line flow | Starts on its own new line | Can sit inline next to other elements/text |
| Visual effect | A border around the container spans the whole page width | A border hugs tightly around just the flexed items |

---

## 2. Targeting the flexed children precisely (`EX 9.1 Flex Direction`)

Once children are inside a flex container, you often need to select **only the direct children** (e.g.
to give them all a `flex-basis`) without accidentally matching something nested deeper inside one of
them later. This connects back to the **combinators** lesson (see `concept_css.md` §4):

| Selector | What it targets |
|---|---|
| `.container div` | All `div` descendants (any depth) — loose, matches too much if nesting grows |
| `.container > div` | Only **direct child** `div`s |
| `.container > *` | All direct children, **regardless of tag** — uses the universal selector |
| `.container > :is(div)` | Same as `> div` but composable — extend with more tags: `:is(div, p)` |

The safest default for "style every direct child the same way" is `.container > *`, since it doesn't
care what tag each child happens to be.

```css
.container {
  display: inline-flex;
  flex-direction: column;
}

.container > * {
  flex-basis: 100px;
}
```

- **`flex-direction: column`** stacks the flex items vertically instead of the default horizontal row —
  covered in more depth in the next lesson on the Flexbox axis/direction.

---

---

## 3. Main axis vs cross axis — the mental model everything else hangs off

```text
flex-direction: row (DEFAULT)          flex-direction: column
  main axis  ──────────────►             main axis  │
  cross axis      │                                 ▼
                  ▼                      cross axis ──────────►
```

- **Main axis** = the direction items flow in. **Cross axis** = perpendicular to it. Both flip the
  moment you change `flex-direction`.
- `flex-basis` follows the **main axis**: it's the **width** in a `row`, the **height** in a `column`.
- `flex-basis` is a **child** property — it goes on the items, not on the container.
- Handy extras from the exercises: `list-style: none` kills the bullets when you flex a `<ul>` into a
  nav bar.

### 🗣️ Selva-speak (the versions that actually stick)

- **"Rules meera padum."** The second a parent becomes `display: flex`, the children's own
  `block` / `inline` / `list-item` rules are *overruled and discarded*. Flexbox is a separate system —
  don't reason about it with block/inline instincts.
- **Normal `flex` = 100% block**, takes the full width. **`inline-flex` = inline-block**, hugs its content.
- **Float is for floating images around text — NOT for layouts.** That's the one job it was designed for.

---

## Key takeaways

- Flexbox = declare `display: flex` (or `inline-flex`) on a **container**; its children get laid out by
  Flexbox rules regardless of their own default display type.
- `flex` vs `inline-flex` only changes how the **container** sits in the page (full-width vs shrink-to-fit)
  — same mental model as `block` vs `inline-block`.
- Prefer `.container > *` over `.container div` when styling "all direct children" — it's tag-agnostic
  and won't accidentally reach into nested elements later.
- Old layout hacks (`<table>` for styling, `inline-block`, `position: absolute`, `float`) still exist in
  older code but are considered legacy for whole-page layout — Flexbox/Grid replaced them.
