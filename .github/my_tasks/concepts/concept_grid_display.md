# CSS Grid — `display: grid` (Module 10 opener)

Source transcript: `course_content/GRID/grid_display.txt`
Practice exercise: `EX 10.0 Display Grid` (Chessboard) — **graded 10/10**, see §8

## The problem this solves

Flexbox is excellent at one thing: lining items up **along a single line**. Give it a row of nav links
or a row of pricing cards and it's perfect (that was the whole of `EX 9.4`).

Now picture a magazine-style dashboard — a header spanning the top, a sidebar down the left, a wide
hero panel, three unequal tiles beneath it, a footer. Could you build that with Flexbox? Technically
yes, by nesting flex containers inside flex containers inside flex containers — but getting every item
to line up **both horizontally and vertically at the same time** becomes miserable. Web designers hit
this wall too, which is why **CSS Grid** was created: a layout system designed from the start for
**two-dimensional** layouts.

The transcript's real-world example is a Swiss weather site (Bern forecast) whose whole page is one
grid — and it stays proportional as the window shrinks, with every panel edge still aligned.

---

## 1. Grid vs Flexbox — the actual distinction

| | Flexbox | Grid |
|---|---|---|
| Dimensions | **1D** — a single row *or* a single column | **2D** — rows *and* columns together |
| Best at | Aligning/spacing content along one line | Laying out page regions in a table-like structure |
| Natural instinct | **Squish and adapt** content to fit the space | **Keep the grid** — everything lines up on shared row/column lines |
| Typical use | Nav bar, card row, button group, centring | Page skeleton, dashboards, image galleries, chessboards |

**⚠️ It is not an either/or choice.** Real sites use both, nested inside each other:

- A **Flexbox inside a Grid** — e.g. the grid defines a weather panel, and inside that panel a
  `flex-direction: column` flexbox stacks and aligns the temperature/icon/label. This is extremely common.
- A **Grid inside a Flexbox** — also fine.

> "Sometimes you might have a Flexbox inside a grid and other times you might have a grid inside a Flexbox."

So Flexbox was **not** wasted learning. They're different tools with different strengths, used together.

### The behaviour difference (see it, don't just read it)

The lesson ships a live demo: <https://appbrewery.github.io/grid-vs-flexbox/>. Drag the window edge and
watch the same content laid out both ways:

- **Grid** — items snap to shared column and row lines. All the gaps line up perfectly, dead straight.
- **Flexbox** — items adapt/squish to fill the space. They may *occasionally* line up, but never reliably,
  because "flexible" is literally the point.

You *can* make a one-dimensional grid — nothing stops you — it just behaves differently from a flexbox.

---

## 2. Turning on Grid

Identical muscle memory to Flexbox: the property goes on the **container**, not the children.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr;   /* 2 columns, 2nd is twice as wide */
  grid-template-rows: 1fr 1fr;      /* 2 rows, equal height */
  gap: 10px;                        /* space between rows AND columns */
}
```

| Property | Goes on | What it does |
|---|---|---|
| `display: grid` | container | Switches the container to grid layout; children become **grid items** |
| `grid-template-columns` | container | Defines how many columns and how wide each one is |
| `grid-template-rows` | container | Defines how many rows and how tall each one is |
| `gap` | container | Gutter between tracks — same `gap` you already know from Flexbox |

You write **one value per track**, space-separated. `1fr 2fr` = two columns. `1fr 1fr 1fr 1fr` = four columns.

---

## 3. The `fr` unit — the one genuinely new idea

`fr` = **fraction of the available space** in the container. It's a *ratio*, not a fixed size.

- `grid-template-columns: 1fr 2fr` → the second column is always **twice** as wide as the first.
  If column 1 lands on 100px, column 2 is 200px.
- `grid-template-rows: 1fr 1fr` → two rows of equal height.

This should feel familiar — it's the same **ratio** thinking as `flex-grow` (`flex: 1` / `flex: 2` /
`flex: 3` in a 600px row → 100/200/300). Grid just gives the idea its own unit.

### ⚠️ TRAP — `fr` needs space to divide (my actual bug this session)

`1fr` means "one share of the **available** space". If the container has **no size on that axis**,
available space is `0`, so every track computes to `0px` — the items exist in the DOM but are invisible.

That is exactly what happened on the first chessboard attempt:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows:    1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;  /* ← no container height */
}
```

**Result: a completely blank page.** The 64 divs were all there, each `100% ÷ 8` of a **zero-height**
container = `0px` tall.

Why the columns survived but the rows didn't → **the default sizing of a grid container is asymmetric**:

> "The default behavior for a grid container is to try and take up the full width, but only have as much
> height as it allows to fit the content."

- **Width**: a grid container is block-level, so it fills its parent → `1fr` columns have real space to split. ✅
- **Height**: it only grows to fit its content → with empty divs, content height is `0` → `1fr` rows get nothing. ❌

**The fix is one of two things** — either give the *container* a height, or give the *children* a height.
Both are covered in §7.

**Rule of thumb:** `fr` on rows only works if the row axis has a defined size (a container `height`, or
content tall enough to define it). Same trap family as `align-items` needing a container height in Flexbox.

---

## 4. Grid infers what you mean

Set only `grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr` (8 columns) and drop 64 divs in — you
**already get a chessboard**. Grid takes items 1–8 for row 1, 9–16 for row 2, and so on, auto-creating
rows as needed (these are *implicit* rows; a later lesson names them).

Writing `grid-template-rows` anyway is still good practice — it makes the intent explicit and gives you
control over row heights instead of leaving them to the browser.

---

## 5. `repeat()` — shorthand for identical tracks

Writing `1fr` eight times is noisy. `repeat(count, size)` says it once:

```css
grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;   /* verbose */
grid-template-columns: repeat(8, 1fr);                     /* identical result */
grid-template-columns: repeat(8, 100px);                   /* fixed-size version */
```

---

## 6. Grid items stretch to fill their cell by default

A grid item with **no** `width`/`height` **fills its whole cell**, in *both* directions. This is the
same `stretch` default you already met as `align-items: stretch` in Flexbox — Grid just applies it on
both axes at once.

That's why the chessboard works with completely unstyled, empty `<div>`s: give the *cell* a size and the
square fills it automatically. It also means a `background-color` on a grid item paints the entire cell.

---

## 7. `EX 10.0 Display Grid` — the Chessboard

**Brief:** 64 pre-written `<div>`s alternating `.white` / `.black`. Turn them into an 8×8 board where
every square is exactly **100px × 100px**. Colours: white `#f0d9b5`, black `#b58863`.

Why this exercise exists: a chessboard is the purest possible 2D layout. With float or Flexbox, making
64 boxes line up perfectly in both directions is painful. With Grid it's four lines of CSS.

### Two valid solutions — opposite directions

**(a) Size the children — the official solution**

```css
.container {
  width: 800px;                    /* no height needed */
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows:    repeat(8, 1fr);
}
.white, .black { width: 100px; height: 100px; }
```

Columns: `800px ÷ 8 = 100px`. Rows: the container has no height, so rows size to their **content** —
and the content is told to be `100px` tall, so each row becomes 100px and the container grows to 800px
on its own.

**(b) Size the container — my solution**

```css
.container {
  width: 800px;
  height: 800px;                   /* ← this is what makes the 1fr rows work */
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows:    repeat(8, 1fr);
}
.white { background-color: #f0d9b5; }
.black { background-color: #b58863; }
```

Both axes now have 800px for `1fr` to split → 100px tracks. The squares need **no** size at all, because
grid items stretch to fill their cell (§6).

**Both render pixel-identical boards.** (b) is arguably the more idiomatic grid approach: you let the
**grid dictate sizes to the children**, instead of forcing sizes on the children and letting the grid
infer itself. It also means changing `800px` to `640px` resizes the whole board in one edit.

### Why `width: 800px` on the container at all?

Without it, the container stretches to the **full window width**, so `1fr` columns become far wider than
100px and gaps appear to open up between the coloured squares (the squares stay 100px but their cells
don't). Fixing the width to `8 × 100px = 800px` makes the cells exactly square-sized and the board compact.

> The instructor's own note: not setting the width is *fine* — the exercise is really about
> `display: grid` + `grid-template-columns`.

---

## 8. Grading — `EX 10.0` submission

| Criteria | Marks |
|---|---|
| `display: grid` on the container | 2/2 |
| 8 equal columns via `1fr` | 2/2 |
| 8 equal rows via `1fr` | 2/2 |
| Squares render at exactly 100×100px | 2/2 |
| Correct colours (`#f0d9b5` / `#b58863`) | 2/2 |
| **Total** | **10/10** |

Only debugging step needed: the missing container `height` (§3). Once added, correct first time — and
the chosen approach (size the container, let items stretch) is the more scalable of the two.

---

## 🗣️ Selva-speak (the versions that actually stick)

- **Flexbox = one line. Grid = a table.** If the design has an X *and* a Y, reach for Grid.
- **`fr` is `flex-grow` with a unit.** Both are ratios sharing leftover space. `1fr 2fr` ≡ `flex: 1` / `flex: 2`.
- **`fr` of nothing is nothing.** No size on that axis → `0px` tracks → blank screen. Check the *container's*
  height before blaming the grid.
- **Grid container is greedy sideways, shy downwards** — full width by default, content height by default.
- **You don't size chess squares, you size the board.** Grid items stretch into their cell for free.

---

## Key takeaways

- `display: grid` goes on the **container**; `grid-template-columns` / `grid-template-rows` define the
  track sizes; `gap` spaces them — all container properties.
- `fr` = a fraction of **available** space, i.e. a ratio. It needs real space on that axis to divide.
- A grid container defaults to **full width but content height** — the #1 cause of collapsed `1fr` rows.
- Grid auto-creates rows if you only define columns, but declaring both is clearer.
- `repeat(n, size)` replaces repeated track values.
- Grid items **stretch to fill their cell** on both axes unless you size them.
- Flexbox and Grid are **complements, not competitors** — nest them freely.

**Next lesson:** customising the grid further (`10.1 Grid Sizing`, `10.2 Grid Placement`, then the
`10.3 Mondrian Project`).
