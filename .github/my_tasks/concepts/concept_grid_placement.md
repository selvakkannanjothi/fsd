# CSS Grid - Placing Items with Lines, Spans, Shorthands, and Areas (Module 10, EX 10.2)

Source material: `course_content/GRID/EX 10.2 Grid Placement/`
Hands-on reinforcement: Grid Garden levels 1-19
Builds on: `concept_grid_display.md` and `concept_grid_sizing.md`

## The problem this solves

Defining rows and columns creates the **map**, but it does not answer the next design question:
"Which item belongs in which part of that map?"

Without placement rules, Grid uses **auto-placement**: it reads the HTML in source order, fills cells
from left to right, and then moves to the next row. That is perfect for uniform galleries, but a real
page needs a header spanning several columns, a sidebar spanning several rows, a hero panel occupying
a rectangle, and sometimes intentional overlap. Grid placement gives each item an address.

---

## 1. Tracks are spaces; grid lines are the addresses

A grid with 3 columns has **4 vertical grid lines**. A grid with 2 rows has **3 horizontal grid lines**.
Lines include the outside edges.

```text
vertical lines:   1 | column 1 | 2 | column 2 | 3 | column 3 | 4
horizontal lines: 1 ----------- 2 ----------- 3
```

This is the first placement discipline: **count lines, not boxes**. An item that covers columns 1 and
2 starts at vertical line `1` and ends at vertical line `3`.

---

## 2. Parent properties vs item properties

| Goes on the grid container | Goes on an individual grid item |
|---|---|
| `display: grid` | `grid-column-start` / `grid-column-end` |
| `grid-template-columns` | `grid-row-start` / `grid-row-end` |
| `grid-template-rows` | `grid-column` / `grid-row` |
| `grid-auto-rows` / `grid-auto-columns` | `grid-area` |
| `gap` | `order` |

This follows the same ownership rule as Flexbox: the **parent creates the layout system**; a child can
then say where it belongs inside that system.

---

## 3. Start and end lines

```css
.hero {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 2;
}
```

The end line can be numerically smaller than the start line. Grid still understands the area between
the two lines:

```css
.item {
  grid-column-start: 5;
  grid-column-end: 2; /* covers the area between lines 2 and 5 */
}
```

Negative line numbers count from the far edge: `-1` is the final line, `-2` is the line before it.
This is especially useful when the exact number of tracks might change.

```css
.sidebar {
  grid-column-start: -3;
  grid-column-end: -1;
}
```

---

## 4. `span` answers "how many tracks?"

Sometimes the precise end line matters less than the item's size relative to its starting position.
Use `span` followed by a **positive** track count:

```css
.cowboy   { grid-column: span 2; }
.book     { grid-row: span 2; }
.banner   { grid-column: 2 / span 3; }
```

- `grid-column: span 2` means "occupy two column tracks from wherever auto-placement puts me."
- `grid-column: 2 / span 3` means "start at line 2 and occupy three columns."
- `span` is a size/count, not a destination line.

Selva-speak: **line numbers answer where; `span` answers how many.**

---

## 5. The two-axis shorthands

```css
.item {
  grid-column: 2 / 5; /* column start / column end */
  grid-row: 1 / 3;    /* row start / row end */
}
```

A single value such as `grid-column: 2` selects the track beginning at line 2 and uses the default
one-track span. A value such as `grid-row: 3 / 6` covers rows between horizontal lines 3 and 6.

---

## 6. `grid-area` - the four-number rectangle

`grid-area` combines both axes in this exact order:

```css
grid-area: row-start / column-start / row-end / column-end;
```

Example:

```css
.astronaut {
  grid-area: 2 / 1 / 3 / 3;
}
```

Read it as: start at row line 2 and column line 1; stop at row line 3 and column line 3.
That produces one row tall by two columns wide.

Mnemonic: **Row, Column, Row, Column - walk around the rectangle.**

The same area in longhand is:

```css
.astronaut {
  grid-row: 2 / 3;
  grid-column: 1 / 3;
}
```

Use whichever version is easier to verify. While learning, longhand is often safer because a swapped
row/column value in `grid-area` is valid CSS but the wrong rectangle.

---

## 7. Auto-placement and `order`

Items without explicit line placement follow source order. Grid items default to `order: 0`, and Grid
sorts lower values before higher values.

```css
.poison { order: 1; }  /* moves after the order:0 items */
.first  { order: -1; } /* moves before them */
```

This is the same warning as Flexbox: `order` changes the **visual layout only**. It does not change the
DOM, reading order, or keyboard focus order. Do not use it to repair meaningful document structure.

---

## 8. Explicit placement can overlap items

Grid does not stop two items from claiming the same cell or area. `demo4.html` deliberately places the
book across an area already used by the cowboy and astronaut:

```css
.cowboy   { grid-area: 1 / 1 / 2 / 3; }
.astronaut{ grid-area: 2 / 1 / 3 / 3; }
.book     { grid-area: 1 / 2 / 3 / 4; }
```

That overlap can create intentional layered designs. When two items overlap, painting/source order and
`z-index` determine which appears on top. Treat overlap as a design decision, not an accident.

---

## 9. Flexbox inside a grid item

The first placement exercise is a direct demonstration that Grid and Flexbox are partners:

```css
.item {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Grid decides the boxes' rows/columns. Flexbox centers the emoji **inside each box**. Grid owns the
macro 2D layout; Flexbox owns the small 1D alignment problem inside a cell.

---

## 10. EX 10.2 practice audit (source files preserved)

The `course_content/` files are source material, so they were inspected but not edited.

| Exercise | Goal | Current status |
|---|---|---|
| `exercise1.html` | Center every emoji horizontally and vertically | **Correct** - the items use Flexbox centering |
| `exercise2.html` | Cowboy and astronaut each span two columns; book occupies the right column | **Needs one line** - `order: 1` puts the astronaut after the book, but `.astronaut` still needs `grid-column: span 2` |
| `exercise3.html` | Book spans both rows on the right | **Correct** - `grid-row: span 2` is a valid solution |

The important distinction in exercise 2:

- `order: 1` answers **when the item is auto-placed**.
- `grid-column: span 2` answers **how wide it is**.

Changing order cannot secretly change size. This is the same debugging discipline as Flexbox sizing:
separate **position**, **size**, and **alignment** into different questions.

---

## Selva-speak

- **The template draws the map; placement gives each item an address.**
- **Count grid lines, not boxes.** Three columns have four vertical lines.
- **Line numbers answer where; `span` answers how many.**
- **`grid-area` = row / column / row / column. Walk around the rectangle.**
- **`order` changes when, not where or how wide.**
- **Grid outside, Flexbox inside** is a normal real-world pattern.

---

## Key takeaways

- Grid auto-places unpositioned items left-to-right, then row-by-row.
- Start/end properties use grid **line numbers**, including negative numbers from the far edge.
- `span n` occupies `n` tracks and only accepts positive counts.
- `grid-column` and `grid-row` use `start / end`.
- `grid-area` uses `row-start / column-start / row-end / column-end`.
- Explicit areas may overlap; use that intentionally.
- `order` is visual only and cannot replace a missing width/span rule.
- Use Flexbox inside a grid item when its internal content needs centering or one-dimensional alignment.

**Next:** apply placement and sizing together in `EX 10.3 Mondrian Project`.
