# CSS Grid Garden - Complete 28-Level Revision Notes

Practice site: <https://appbrewery.github.io/gridgarden/>
Completed and verified: **28/28 on 2026-08-29** (final "You win!" screen reached)
Builds on: Grid display, sizing, and placement

## The problem this solves

Grid properties are easy to recognise while reading notes and surprisingly easy to mix up when the
editor is blank. Grid Garden forces one small decision at a time: choose a start line, choose an end
line, count backwards, use a span, place an area, change auto-placement order, then design the tracks.

The value of the game is not the carrots. It turns property names into **muscle memory**.

---

## 1. The mental model used across all 28 levels

Ask these questions in order:

1. **Am I placing an item or defining the grid?**
   - Item placement: `grid-column-*`, `grid-row-*`, `grid-area`, `order`.
   - Grid definition: `grid-template-columns`, `grid-template-rows`, `grid-template`.
2. **Do I know the destination line or only the number of tracks?**
   - Destination line -> use a number (`2 / 5`).
   - Number of tracks -> use `span` (`2 / span 3`).
3. **Am I counting from the left/top or from the far edge?**
   - From the far edge -> use negative line numbers; `-1` is the last line.
4. **Is the task two-dimensional?**
   - Use both `grid-column` and `grid-row`, or one `grid-area` rectangle.
5. **Am I sharing leftover space?**
   - Use `fr`. Fixed tracks are removed first; `fr` shares what remains.

---

## 2. Verified solutions - levels 1 to 14

| Level | Concept being drilled | Verified CSS |
|---:|---|---|
| 1 | Start at vertical line 3 | `grid-column-start: 3;` |
| 2 | Start at vertical line 5 | `grid-column-start: 5;` |
| 3 | End at vertical line 4 | `grid-column-end: 4;` |
| 4 | End may be before start | `grid-column-end: 2;` |
| 5 | Count the end line from the right | `grid-column-end: -2;` |
| 6 | Count the start line from the right | `grid-column-start: -3;` |
| 7 | Span 2 tracks toward the end | `grid-column-end: span 2;` |
| 8 | Span 5 tracks toward the end | `grid-column-end: span 5;` |
| 9 | Span 3 tracks backward from the end | `grid-column-start: span 3;` |
| 10 | Column shorthand: start / end | `grid-column: 4 / 6;` |
| 11 | Column shorthand with span | `grid-column: 2 / span 3;` |
| 12 | Start at horizontal row line 3 | `grid-row-start: 3;` |
| 13 | Row shorthand: start / end | `grid-row: 3 / 6;` |
| 14 | Place on both axes | `grid-column: 2;` + `grid-row: 5;` |

### What levels 1-14 prove

- A track and a line are not the same thing. Five columns need six vertical lines.
- End does **not** have to be numerically greater than start.
- Negative numbers count lines from the opposite edge.
- `span` is a positive track count, never a negative destination.
- `grid-column` and `grid-row` are the same idea on perpendicular axes.

---

## 3. Verified solutions - levels 15 to 28

| Level | Concept being drilled | Verified CSS |
|---:|---|---|
| 15 | Span a large 2D area with two shorthands | `grid-column: 2 / 6;` + `grid-row: 1 / 6;` |
| 16 | Four-value area shorthand | `grid-area: 1 / 2 / 4 / 6;` |
| 17 | Place a second, overlapping area | `grid-area: 2 / 3 / 5 / 6;` |
| 18 | Move poison after normal items | `order: 1;` |
| 19 | Move poison before normal items | `order: -1;` |
| 20 | Make the first column half the garden | `grid-template-columns: 50%;` |
| 21 | Eight equal percentage columns | `grid-template-columns: repeat(8, 12.5%);` |
| 22 | Mix track units | `grid-template-columns: 100px 3em 40%;` |
| 23 | Divide the whole width 1:5 | `grid-template-columns: 1fr 5fr;` |
| 24 | Fixed outside tracks, three flexible middle tracks | `grid-template-columns: 50px 1fr 1fr 1fr 50px;` |
| 25 | Remove 75px, then divide the remainder 3:2 | `grid-template-columns: 75px 3fr 2fr;` |
| 26 | Five rows; top path fixed, row 5 gets the rest | `grid-template-rows: 50px 0 0 0 1fr;` |
| 27 | Rows / columns shorthand | `grid-template: 60% 40% / 200px;` |
| 28 | Final two-row, two-column garden | `grid-template: 1fr 50px / 20% 1fr;` |

### `grid-area` order - do not guess

```css
grid-area: row-start / column-start / row-end / column-end;
```

For level 16, `1 / 2 / 4 / 6` means rows 1-4 and columns 2-6. The easiest prevention for a swapped
answer is to say the four labels out loud before typing the numbers.

### `grid-template` order - a different shorthand order

```css
grid-template: rows / columns;
```

Do not confuse this with `grid-area`. Level 27 creates two rows (`60% 40%`) and one `200px` column.
Level 28 creates two rows (`1fr 50px`) and two columns (`20% 1fr`).

---

## 4. Fixed tracks plus `fr` - subtract, then share

Level 24 is the cleanest arithmetic example:

```css
grid-template-columns: 50px 1fr 1fr 1fr 50px;
```

Browser algorithm (ignoring gaps):

1. Reserve `50px + 50px = 100px` for the fixed tracks.
2. Remaining width = container width minus `100px`.
3. Three `1fr` tracks divide that remainder equally.

Level 25 uses the same process, but the remaining space is divided `3:2`:

```css
grid-template-columns: 75px 3fr 2fr;
```

If the container were `1075px`, the remainder would be `1000px`; five total shares means `200px` per
share, so the flexible columns become `600px` and `400px`.

---

## 5. Zero-sized tracks are intentional sometimes

Level 26 is unusual but valid:

```css
grid-template-rows: 50px 0 0 0 1fr;
```

The water item is locked to row 5. The goal needs a 50px dry path at the top and water everywhere
else, so rows 2-4 deliberately collapse to `0`. This connects to Selva's earlier bug:

- Earlier: `0px` rows were accidental because `1fr` had no height to divide.
- Here: `0` rows are deliberate routing tracks used to push row 5 into the correct position.

Same rendering outcome, completely different cause. Always ask whether the zero size is requested or
accidental.

---

## 6. `order` changes sequence, not geometry

Levels 18 and 19 mirror Flexbox:

```css
.poison { order: 1; }  /* after order:0 items */
.poison { order: -1; } /* before order:0 items */
```

`order` affects auto-placement sequence. It does not choose a line, create a span, or change a track
size. It is also visual only, so meaningful reading order should still be correct in the HTML.

---

## 7. Completion evidence and honest status

- Every submitted rule was accepted by the game.
- Each accepted level advanced to the next numbered level.
- Level 28 produced the final **"You win!"** screen and carrot-cake illustration.
- This proves the game solutions, but it does **not** replace doing the local `EX 10.1` sizing exercise
  or correcting the remaining local placement/Mondrian issues yourself.

---

## Selva-speak

- **Where? Use lines. How many? Use `span`.**
- **Negative lines count from the other wall; `-1` is the wall itself.**
- **`grid-area` walks row, column, row, column.**
- **`grid-template` says rows first, columns after the slash.**
- **Fixed tracks eat first; `fr` shares the leftovers.**
- **`order` changes the queue, not the size of the boxes.**

---

## Key takeaways

- Lines 1-17 are mainly placement: start/end lines, negative lines, `span`, rows, and `grid-area`.
- Lines 18-19 prove that Grid auto-placement can be reordered like Flexbox.
- Lines 20-28 define tracks with percentages, lengths, `repeat()`, `fr`, and `grid-template`.
- Fixed and flexible tracks work together: reserve fixed sizes, subtract gaps, share the remainder.
- The final shorthand distinction must stay sharp:
  - `grid-area`: row-start / column-start / row-end / column-end.
  - `grid-template`: rows / columns.

**Result:** Grid Garden complete, **28/28**.
