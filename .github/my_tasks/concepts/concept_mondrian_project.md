# CSS Grid - EX 10.3 Mondrian Project (Section Capstone)

Source transcript: `course_content/GRID/EX 10.3 Mondrian Project/mondrian_project.transcript.txt`
Reference assets: `dimensions.png`, `goal.png`, and `solution.html`
Builds on: Grid track sizing, placement, spans/areas, gaps, and Flexbox centering

## The problem this solves

Until now, every lesson isolated one property. The Mondrian project removes the scaffolding: start
with a blank page and convert a measured painting into HTML and CSS. It tests whether you can look at
a visual design and reverse-engineer:

1. how many tracks exist,
2. how large each track must be,
3. which blocks span multiple tracks,
4. how the "lines" are produced, and
5. how the finished composition is centered on the page.

This is the first full **design-to-layout** exercise in the Grid section.

---

## 1. Start from the geometry, not the colours

The reference is a `748px x 748px` composition. Its visible regions require four columns and four
rows, even though some neighbouring cells look like one large block.

```css
.container {
  width: 748px;
  height: 748px;
  display: grid;
  grid-template-columns: 320px 198px 153px 50px;
  grid-template-rows: 414px 130px 155px 22px;
  gap: 9px;
}
```

Why four columns? The bottom yellow and black regions split what looks like one larger middle region
into two independent widths (`198px` and `153px`). Grid lines must exist wherever any later region
needs a boundary.

Why four rows? The blue block, lower white block, and bottom coloured strips all end at different
horizontal positions.

Rule: **draw every boundary line first; merge cells later with spans.**

---

## 2. The black-line trick: colour the gap, not the grid line

CSS grid lines are coordinates; they are not paintable objects. The project creates visible black
lines by making the container black and leaving transparent gaps between the items:

```css
.container {
  background-color: #000;
  gap: 9px;
}

.item {
  background-color: #F0F1EC;
}
```

The `gap` exposes the parent's black background. This is the same ownership discipline from the
pricing-table project: ask **which element actually owns the visible colour?** Here the children own
the coloured panels; the container owns the black seams.

---

## 3. Nine visual regions = nine HTML items

The solution uses one `<div>` for each painted region:

```html
<div class="container">
  <div class="item red"></div>
  <div class="item white1"></div>
  <div class="item white2"></div>
  <div class="item white3"></div>
  <div class="item blue"></div>
  <div class="item white4"></div>
  <div class="item"></div>
  <div class="item yellow"></div>
  <div class="item black"></div>
</div>
```

The base `.item` class gives every region the common off-white colour; colour classes override only
the exceptional cells. This keeps the CSS declarative instead of repeating the same white value.

---

## 4. Use spans where the visual merges cells

```css
.white1 { grid-column: span 3; }
.white2 { grid-row: span 2; }
.white3 { grid-area: 2 / 2 / 4 / 4; }
.white4 { grid-row: span 2; }
```

- `white1` consumes the last three columns in row 1.
- `white2` consumes rows 2 and 3 in column 1.
- `white3` occupies the rectangle from row line 2 / column line 2 to row line 4 / column line 4.
- `white4` fills the fourth column across rows 3 and 4.

The project deliberately mixes `span` and `grid-area`. There is no prize for using the shortest
property everywhere; use the form that makes the shape easiest to verify.

---

## 5. The blue block includes its own extra black border

The reference blue region is `130px` high and has an additional `10px` black line underneath it.

```css
.blue {
  background-color: #004592;
  border-bottom: 10px solid #000;
}
```

This line belongs to the blue item itself, unlike the normal `9px` seams owned by the container gap.
It is a useful reminder that one visual can combine multiple box-model sources.

---

## 6. Center the entire artwork with Flexbox

Grid builds the painting; Flexbox positions the finished painting in the viewport:

```css
body {
  margin: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

This is the same centering recipe from the pricing-table capstone. `min-height: 100vh` is safer than a
locked `height: 100vh` if the content ever becomes taller than the viewport.

Macro composition: Grid. One-object viewport alignment: Flexbox.

---

## 7. Colour palette

| Role | Hex |
|---|---|
| Gap/line black | `#000` |
| Off-white | `#F0F1EC` |
| Red | `#E72F24` |
| Dark block | `#232629` |
| Blue | `#004592` |
| Yellow | `#F9D01E` |

Keeping colours in named classes (or custom properties in a later refactor) separates visual identity
from placement geometry.

---

## 8. Current local attempt audit (source file preserved)

`course_content/GRID/EX 10.3 Mondrian Project/index.html` already contains a strong near-complete
attempt. It was inspected but not edited because `course_content/` is source material.

What is already correct:

- Nine HTML items are present.
- The 4-column geometry is correct.
- The major red/white/blue/yellow/black regions are assigned.
- The `9px` gap plus black container background produces the seams.
- Spans/areas successfully recreate the major shapes.

What remains for the hands-on project:

1. **Centering is missing.** Add the body Flexbox centering recipe.
2. **Final row should be `22px`, not `20px`, for an exact `748px` fit.**
   `414 + 130 + 155 + 22 + (3 x 9) = 748`.
3. Prefer a shared `.item { background-color: #F0F1EC; }` plus semantic colour/shape classes to reduce
   repeated row/column rules, after the pixel-perfect version works.

The geometry is close; the remaining mistakes are again **ownership and arithmetic**, not a lack of
layout understanding.

---

## 9. A repeatable design-to-grid workflow

1. Draw every horizontal and vertical boundary over the reference.
2. Count tracks and remember: tracks + 1 = grid lines.
3. Write the container's width, height, tracks, and gap.
4. Add one neutral item for every visual region.
5. Let auto-placement handle simple single cells.
6. Add `span`, `grid-row`, `grid-column`, or `grid-area` only where a region crosses boundaries.
7. Apply colours after the geometry matches.
8. Inspect with the DevTools grid overlay and "Show track sizes".
9. Check the arithmetic: sum of tracks + sum of gaps = container size.
10. Center the finished component only after its internal layout is correct.

---

## Selva-speak

- **Draw every boundary first; merge cells later.**
- **The gap is transparent, so paint the parent black.**
- **Grid makes the painting; Flexbox hangs it on the wall.**
- **Tracks + gaps must add up to the frame.**
- **Do geometry first, colours second, centering last.**

---

## Key takeaways

- Complex artwork is still just tracks, gaps, and rectangular spans.
- A visible grid "line" is commonly the container background showing through `gap`.
- One div per visual region is a clean starting model.
- `span` is ideal for simple widths/heights; `grid-area` is ideal for a known rectangle.
- Flexbox and Grid solve different layers of the same project.
- Pixel-perfect work requires arithmetic: track sizes plus gaps must equal the declared container size.
- The local attempt is close but the capstone should remain **not fully complete** until centering and the
  `22px` final row are corrected by Selva.
