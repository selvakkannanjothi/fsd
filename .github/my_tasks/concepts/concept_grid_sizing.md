# CSS Grid — Sizing Tracks: Fixed, Auto, Fractional, MinMax, Repeat (Module 10, Lesson 61)

Source transcript: `course_content/GRID/grid_sizing.txt`
Practice exercise: `EX 10.1 Grid Sizing` (the "Test" page) — not yet attempted, see §9
Builds on: `concept_grid_display.md` (turning on Grid, the `fr` unit, the width/height default asymmetry)

## The problem this solves

`EX 10.0` got a grid on the screen at all — `display: grid` + equal `fr` tracks was enough for a
chessboard where every square is identical. But almost no real layout is "8 identical squares." A
real page wants: a sidebar that's *always* 250px, a content column that *fills whatever's left*, an
image column that's *flexible but never too narrow or too wide*, and it all has to keep working if
the browser window resizes or if some cell gets more content than the others.

This lesson is the sizing toolbox that makes that possible: **fixed / `auto` / `fr` / `minmax()` /
`repeat()`**, plus the two questions every real layout eventually asks — *what if I have fewer items
than grid cells?* and *what if I have more?*

---

## 1. Fixed sizing — `px` / `rem` — never responsive

```css
.container {
  grid-template-rows: 100px 200px;
  grid-template-columns: 400px 800px;
}
```

Exactly what it says: row 1 is 100px, row 2 is 200px, column 1 is 400px, column 2 is 800px — forever.
Resize the browser window and **nothing changes**.

Swapping `px` for `rem` (`1rem 2rem`) does **not** fix this. `rem` is relative to the root
(`<html>`) font-size, so it responds to *zoom* or a `html { font-size }` change — but it has no idea
how wide the browser window is. **Relative-to-root is not the same thing as responsive-to-screen.**
(Same distinction as `em`/`rem` in the CSS fonts lesson — relative units solve *scaling*, not
*layout responsiveness*.)

---

## 2. The `grid-template` shorthand (recognise it, don't write it yet)

```css
grid-template: 100px 200px / 400px 800px;
/* rows first, then a forward slash, then columns */
```

This is exactly equivalent to writing `grid-template-rows` and `grid-template-columns` separately.
The instructor deliberately tells learners **not** to use it yet:

> "I don't recommend us to write code like this at this stage because... when you're reviewing your
> code and you're trying to spot problems, it's much easier when you've got the rows defined and
> your columns defined... this just makes it a little bit more hidden as to what's going on."

Explicit now, shorthand later once debugging Grid is second nature. You still need to recognise it
when reading other people's CSS.

---

## 3. `auto` — the row/column asymmetry (⚠️ this lesson's big trap)

```css
.container {
  grid-template-columns: 200px auto;   /* column 2 stretches to fill leftover width */
  grid-template-rows: 100px auto;      /* row 2 just fits its own content's height */
}
```

- **`auto` on a column** → *extensible*: it grows or shrinks so the columns together always add up to
  100% of the container's width. Paired with a fixed `200px` column, the `auto` column simply eats
  whatever's left over.
- **`auto` on a row** → *not* the same idea at all. It does **not** try to fill 100% of the
  container's height. It just **fits the content** — "as long as [the content] fits in there
  perfectly, then it will automatically adjust the height to fit that."

> **This is the exact same asymmetry from `EX 10.0`'s "blank page" trap, just wearing a different
> costume.** Back then it was a *default* (grid container = full width, content height) that bit you
> silently. Here it's the *same width-greedy / height-shy split*, except now you're asking for it
> explicitly with the word `auto`. Once you've internalised "columns care about width, rows care about
> content," both traps disappear.

---

## 4. Fractional sizing (`fr`) — ratios, and a genuinely subtle gotcha

Same idea as `EX 10.0`: `fr` is a *ratio* of the available space, not a fixed size.

```css
grid-template-rows: 1fr 2fr;       /* row 2 is always twice row 1's height */
grid-template-columns: 1fr 1fr;    /* two equal-width columns */
```

Resize the window → the **column** ratio holds no matter what, because columns are governed by
available *width*, which doesn't care about content.

**⚠️ The gotcha (this is new, and easy to miss):** rows sized in `fr` are governed by *content
height* instead, and content height can change. So if you dump a huge paragraph into the item in
**row 2**, the transcript's own demo shows that **row 1 also gets taller** — even though row 1's
content didn't change at all.

Why: `fr` doesn't lock in a size once. It's a *live ratio* recomputed against whatever total height
the tracks currently need. Grow row 2's content → the "1 share" that row 1 is owed grows right along
with it, purely to keep `1fr : 2fr` intact.

> "It's all done just so that we maintain that fractional ratio, so that this one is always half the
> size of this one." — the instructor, watching row 1 grow after only editing row 2's content.

**Rule of thumb:** with `fr` rows, you're never sizing *a* row — you're sizing a *ratio group*.
Touch one member's content, and the whole group can move.

---

## 5. `minmax(min, max)` — one function, two limits

```css
grid-template-columns: minmax(400px, 800px) 1fr;
```

The first column is free to grow up to `800px` when there's room, and free to shrink down to
`400px` — but refuses to cross either line. This is exactly the "ceiling + floor" idea from
Flexbox's `min-width`/`max-width` (Selva's ⚠️ weak area, see `concept_flex_sizing.md`) — except Grid
gives you **one function** that sets both limits on a single track at once, instead of two separate
properties.

Typical use: a column holding an image or a key piece of content that must never get so narrow the
layout breaks, and never so wide it looks stretched out of proportion.

---

## 6. `repeat()` — beyond just `fr`

Already met in `EX 10.0` for `repeat(8, 1fr)`. It works for **any** track value, not only `fr`:

```css
grid-template-rows: repeat(2, 200px);      /* == 200px 200px */
grid-template-columns: repeat(2, 100px);   /* == 100px 100px */
```

`repeat(count, value)` reads as "repeat this size, this many times" — pure DRY, identical result to
writing it out longhand.

---

## 7. When your item count doesn't match your template

### Fewer items than declared cells

A `2-row × 3-column` template = 6 cells. Put only 4 HTML items in and Grid fills cells **left to
right, then wraps to the next row** — item 1–3 take row 1, item 4 starts row 2. The 2 leftover cells
(5 and 6) are simply **empty** — there's no ghost box sitting there, because no item was ever
assigned to that cell.

### More items than declared cells (implicit rows)

A `2×2` template = 4 cells. Add a 5th `<div>` and it has nowhere defined to go, so Grid creates an
extra ("implicit") row on the fly. By default that new row gets:

| Axis | Default sizing rule |
|---|---|
| Width | **Matches the existing column tracks** (borrows the template's column sizing) |
| Height | **Fits its own content** — same "shy" behaviour as an `auto` row from §3 |

To take control of that instead of leaving it to content-fit, use `grid-auto-rows` (and its column
twin `grid-auto-columns`) on the container:

```css
.container {
  grid-template-columns: 200px 200px;
  grid-template-rows: 200px 200px;
  grid-auto-rows: 300px;   /* every row Grid creates beyond the template gets 300px height */
}
```

Real use case from the transcript: content that gets added dynamically (JS-generated rows, a game
board that keeps adding squares) — you don't know in advance how many extra rows there'll be, but you
do know how tall you want each one.

---

## 8. Inspecting Grid sizing in Chrome DevTools

Any element with `display: grid` gets a small **"grid" badge** next to it in the Elements panel.
Click the badge to toggle a grid overlay directly on the page. Opening the **Layout** pane (bottom of
the Styles sidebar) gives you:

- Overlay line colour (swap the default pink for something more visible, e.g. black)
- **Show line numbers** (on by default)
- **Show track sizes** — prints the exact computed pixel size of every row/column right on the
  overlay, so you can check your `fr`/`minmax()` math without doing it by hand
- **Extend grid lines** to the edge of the viewport, useful for checking alignment against other
  elements on the page

Reference: [Chrome DevTools — Inspect CSS grid layouts](https://developer.chrome.com/docs/devtools/css/grid/).

---

## 9. `EX 10.1 Grid Sizing` — the "Test" exercise

**Brief:** the demo site (`appbrewery.github.io/grid-sizing` → "Test" page, saved locally at
`course_content/GRID/EX 10.1 Grid Sizing/test.html`) shows a green reference grid and a purple copy
with an empty `.grid-container` rule. The task: write CSS so the purple grid matches the green one in
size **and** in how it responds to resizing.

Reading the reference grid (per the transcript):

| Track | Requirement |
|---|---|
| Row 1 | `1fr` |
| Row 2 | `1fr` (same height as row 1) |
| Row 3 | `2fr` (exactly double rows 1–2) |
| Row 4 (outside the template!) | fixed `50px` — handled with `grid-auto-rows`, not a 4th template row |
| Column 1 | `auto` — expands to fill space, shrinks down to its content minimum |
| Column 2 | fixed `400px` |
| Column 3 | `minmax(200px, 500px)` |

**Try it yourself first** — the instructor's own instruction is "Pause the video. Have a think about
this problem, write your code..." before revealing the answer. Open the local `test.html`, type your
CSS into the textarea, click **Apply CSS**, and compare against the green side.

<details>
<summary>Lesson's worked solution (expand only after you've tried)</summary>

```css
.grid-container {
  display: grid;
  grid-template-rows: 1fr 1fr 2fr;
  grid-template-columns: auto 400px minmax(200px, 500px);
  grid-auto-rows: 50px;
}
```

</details>

**Common failure mode the instructor calls out:** a missing `s` — `grid-template-row` /
`grid-template-column` instead of `-rows` / `-columns`. Typos like this fail silently (the browser
just ignores an unrecognised property), so check spelling first if nothing happens.

**Tip for checking your own answer:** the green reference box in `test.html` is a real element
(`.parent`) with its own CSS already applied — Inspect it in DevTools and its Styles/Computed panel
*is* the answer key, no need to just trust the transcript.

---

## 🗣️ Selva-speak (session quick notes, lesson 61 — cleaned up)

- *"Fixed px/rem = never responsive — not even `rem`, because it only reacts to root font-size, not
  window width."*
- *"`auto` column = stretches to fill leftover width. `auto` row = shrinks/grows only to fit its
  content height."* → same width-greedy / height-shy split as `EX 10.0`'s blank-page trap, just behind
  an explicit keyword this time instead of a hidden default.
- *"`fr` = fractions/ratios. Columns are capped by the browser width; rows are driven by content — and
  pumping content into ONE `fr` row drags every other `fr` row on that axis along with it, to protect
  the ratio."*
- *"`repeat(count, value)` — repeat this size, this many times."*
- *"More items than the template → Grid keeps flowing left-to-right, row after row, and auto-sizes the
  leftovers: width borrows the existing columns, height fits the content — unless `grid-auto-rows`
  overrides it."*

---

## Key takeaways

- Fixed `px`/`rem` tracks never respond to window size — only to root font-size, and only for `rem`.
- `grid-template: rows / columns` is valid shorthand, deliberately avoided while learning, for
  debuggability.
- `auto` behaves **differently by axis**: columns stretch to fill width, rows just fit content height.
- `fr` is a *live ratio*, not a locked-in size — growing one row's content can grow its `fr` siblings too.
- `minmax(min, max)` is Grid's one-function version of Flexbox's `min-width` + `max-width` combined.
- `repeat()` works for any track size, not just `fr`.
- Too few items → leftover cells stay empty. Too many items → Grid adds implicit rows sized by
  *existing column widths* + *content height*, unless `grid-auto-rows`/`grid-auto-columns` overrides it.
- Chrome DevTools' grid overlay ("Show track sizes") reads out exact computed pixel sizes for you.

**Next:** `10.2 Grid Placement` → `10.3 Mondrian Project`.
