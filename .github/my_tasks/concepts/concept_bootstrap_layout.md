# Bootstrap — The 12-Column Layout System (Module 11, Lesson 65)

Source transcript: `course_content/11.0 Bootstrap/11.0_bootstrap_layout.txt`
Practice exercise: <https://appbrewery.github.io/bootstrap-layout/> (URL in `11.0 bootsrap_layout_url.txt`)
**Status: all 3 exercises solved and verified — see §8 and §9.**
Builds on: `concept_flexbox.md`, `concept_flex_sizing.md` (⚠️ weak area — Bootstrap's grid *is* flexbox
underneath, see §2), `concept_css.md` (the cascade — source order is the whole mechanism, see §6).

---

## The problem this solves

Every layout built so far was hand-written: measure the design, pick tracks, write the CSS, then add a
`@media` query per screen size and re-write the numbers. The Mondrian capstone needed four measured
column tracks and four measured row tracks. The pricing table needed a media query just to flip
`flex-direction` on mobile.

That is fine for one page. It does not scale, because the *same* few layout decisions get retyped on
every project: "sidebar + content", "three cards in a row", "full width on phones". And the pixel
values for "phone", "tablet", "laptop" are the same on every site in the world.

Bootstrap's answer: **pre-write all of it as classes.** Someone already picked the breakpoints,
already wrote the media queries, already did the percentage maths. Instead of writing CSS you write
`class="col-lg-6 col-sm-12"` and get a responsive layout with **zero lines of your own CSS**.

The trade-off is honest and worth naming up front: you stop writing CSS and start *remembering class
names*. That is why this lesson is mostly vocabulary, and why the instructor says outright that it
"is a little bit complicated when you're first working with it."

---

## 1. The three-part skeleton — container → row → columns

Bootstrap layout is always the same three nested pieces. Never skip a level.

```html
<div class="container">        <!-- 1. sets the overall width + side margins -->
  <div class="row">            <!-- 2. one horizontal line of content -->
    <div class="col">Item</div>   <!-- 3. the items themselves -->
    <div class="col">Item</div>
    <div class="col">Item</div>
  </div>
</div>
```

- **`container`** — how wide the whole block is, and whether it has breathing room at the sides.
- **`row`** — a horizontal band. Its children are the columns. Rows are what the 12 columns are
  counted *within*.
- **`col`** — one item. With bare `col` (no number), Bootstrap divides the row equally: 6 items → each
  gets one-sixth; 3 items → each gets a third. No maths on your part.

Muscle memory: **container wraps rows, rows wrap columns, columns wrap your content.** Your actual
content goes *inside* the `col` div, never directly in the `row`.

---

## 2. What is actually underneath (this is just Flexbox) ⭐

Bootstrap is not magic and it is not a new layout engine — it is Flexbox with the CSS pre-written.
Read straight out of `bootstrap@5.3.0-alpha2` (verified in DevTools during this lesson):

```css
.row      { display: flex; flex-wrap: wrap; --bs-gutter-x: 1.5rem; margin-left: -.75rem; margin-right: -.75rem; }
.row > *  { flex-shrink: 0; width: 100%; max-width: 100%; padding-left: .75rem; padding-right: .75rem; }
.col      { flex: 1 0 0%; }
.col-6    { flex: 0 0 auto; width: 50%; }
.col-auto { flex: 0 0 auto; width: auto; }
```

Every one of these maps onto something already learned:

| Bootstrap class | What it really is | Where this was learned |
| --- | --- | --- |
| `.row` | `display: flex` + `flex-wrap: wrap` | `concept_flex_layout.md` |
| `.row > *` | `width: 100%` — **this is why a class-less div in a row is already full width** | — |
| `.row > *` | `flex-shrink: 0` — items **never squash**, they wrap to a new line instead | flex sizing scenario `1 0` |
| `.col` | `flex: 1 0 0%` = grow 1, shrink 0, **basis 0** = *equal widths, share everything* | `concept_flex_sizing.md` §"basis auto vs 0" |
| `.col-6` | `flex: 0 0 auto` + `width: 50%` — rigid, sized by a plain percentage | the priority ladder: no basis set → `width` governs |
| `.col-auto` | `flex: 0 0 auto` + `width: auto` — sized by its content | content width, bottom of the ladder |

Three consequences worth internalising:

1. **A `<div>` inside a `.row` with no class at all is already 12/12 wide.** That is not a Bootstrap
   "default behaviour" rule to memorise — it is literally `.row > * { width: 100% }`. This is why
   `col-sm-12` is so often redundant (§8, Exercise 1).
2. **Columns wrap, they don't shrink.** `flex-shrink: 0` means if your `col-*` numbers add up to more
   than 12, the overflow drops to a second line rather than everything getting squeezed. That is the
   transcript's *"if it didn't add up to 12, then it will go to the next row."*
3. **The gutter is a negative-margin trick.** The row pulls itself 0.75rem outward on each side, and
   every child pushes 0.75rem of padding inward. Net effect: even gaps *between* columns, but the
   outer edges still line up flush with the container. This is why you must not put your own
   `margin` on a `col` — use the built-in `g-*` gutter classes instead.

**Say it out loud: "Bootstrap's grid is not CSS Grid. It's Flexbox with the homework done."**

---

## 3. The container family — six variants, one question

Selva's own note on the transcript was *"explore!!! what are container / -sm / -lg / -xl / -xxl / -fluid"*.
Here is the answer, read out of Bootstrap's real stylesheet rather than guessed:

```css
@media (min-width: 576px)  { .container, .container-sm { max-width: 540px; } }
@media (min-width: 768px)  { .container, .container-sm, .container-md { max-width: 720px; } }
@media (min-width: 992px)  { .container, ..., .container-lg { max-width: 960px; } }
@media (min-width: 1200px) { .container, ..., .container-xl { max-width: 1140px; } }
@media (min-width: 1400px) { .container, ..., .container-xxl { max-width: 1320px; } }
```

Look at *when each name first joins the list*. That is the entire mechanism:

| Class | Behaviour | Plain English |
| --- | --- | --- |
| `container` | capped at every step: 540 / 720 / 960 / 1140 / 1320 | always has side margins |
| `container-sm` | identical to `container` (joins at the very first step) | the transcript says this too |
| `container-md` | **100% below 768px**, then 720 / 960 / 1140 / 1320 | edge-to-edge on phones |
| `container-lg` | **100% below 992px**, then 960 / 1140 / 1320 | edge-to-edge on phones + tablets |
| `container-xl` | **100% below 1200px**, then 1140 / 1320 | edge-to-edge until desktop |
| `container-xxl` | **100% below 1400px**, then 1320 | edge-to-edge until a TV |
| `container-fluid` | never appears in the list at all → **always 100%** | edge-to-edge, always |

The rule in one line: **`container-{bp}` means "be 100% wide *until* `{bp}`, then behave like a normal
container."** A container variant's name is the point at which it *stops* being full-width.

Selva's transcript note *"1 & 6 will be used in many cases"* is exactly right and matches the
instructor: `container` when you want a tidy margin down both sides, `container-fluid` when you want a
hero banner / nav bar / footer to bleed edge-to-edge. The middle four are situational.

---

## 4. The six breakpoints

| Name | Infix | Fires at | Device (transcript's own mapping) |
| --- | --- | --- | --- |
| Extra small | *(none)* | `<576px` | narrow / foldable phones |
| Small | `sm` | `≥576px` | mobile |
| Medium | `md` | `≥768px` | tablet / iPad |
| Large | `lg` | `≥992px` | laptop |
| Extra large | `xl` | `≥1200px` | desktop |
| Extra extra large | `xxl` | `≥1400px` | TV / very large monitor |

**⚠️ Directionality — the transcript flags this twice, so it matters.** A breakpoint always means
**"this width and everything wider"**, never "up to this width". Bootstrap is built entirely on
`min-width` media queries. `col-sm-6` = *"from 576px upward, be half width"* — it applies on a
mobile, a laptop **and** a TV, unless something bigger overrides it.

**Verified at the edge:** with the exercise page open, resizing to exactly `575px` still measured as
extra-small, and `576px` flipped to small. The boundary is **inclusive** — `min-width: 576px` fires
*at* 576, not after it.

Extra small has **no infix**, because it is the bottom of the ladder and there is no `min-width` to
name. `col-10` and `col-sm-10` are two different things: `col-10` starts applying at 0px.

---

## 5. Sizing columns — `col-1` … `col-12`

Picture every row as being divided into **12 equal slices**. `col-N` claims N of those slices.

```html
<div class="row">
  <div class="col-2">2/12  ≈ 16.7%</div>
  <div class="col-4">4/12  ≈ 33.3%</div>
  <div class="col-6">6/12  = 50%</div>
</div>
```

- Why 12? It divides cleanly by 1, 2, 3, 4, 6 and 12 — so halves, thirds, quarters and sixths are all
  exact. 10 would not give you thirds.
- Numbers in a row should add up to **12**. More than 12 → the overflow wraps to a new line
  (because `flex-shrink: 0`, §2).
- **Mixing sized and unsized is allowed and useful:** `col-2` + `col-4` + `col` → the bare `col` takes
  whatever is left (6/12 here). `.col` is `flex: 1 0 0%`, so it grows into the leftover space.
  Handy when one region is fixed-ish and the other is "the rest".

---

## 6. Stacking breakpoints on one div — the mental model that makes this click ⭐

You can put several `col-*` classes on the same div:

```html
<div class="col-sm-12 col-md-8 col-lg-4">…</div>
```

Read it **bottom-up as a set of overrides**, exactly like the cascade from `concept_css.md`:

- from 576px up → 12/12
- from 768px up → 8/12 (overrides the previous line)
- from 992px up → 4/12 (overrides again, and keeps applying on xl and xxl too)

**Why does the bigger one win?** Not specificity — `.col-sm-12` and `.col-lg-4` are *both* one class,
both `(0,1,0)`. It is pure **source order**: Bootstrap's stylesheet lists the media queries
smallest-first, so `.col-lg-4` physically appears later in the file and wins the tie. Verified in
DevTools: `.col-10` is rule #130, `.col-sm-12` is #176, `.col-lg-6` is #260.

This is exactly rule 1 of the cascade already learned — *"Position (lower wins)"*. Bootstrap did not
invent anything; it just ordered its file mobile-first so the cascade does the work.

Two things fall straight out of that:

- **This is called "mobile-first".** You describe the *smallest* screen first, then override upward.
- **A breakpoint you never override keeps applying forever.** `col-lg-4` with nothing above it is
  still 4/12 on a TV.

`col-sm-12` is usually redundant, because `.row > *` is already `width: 100%` (§2). Write it only when
something *else* on the div would otherwise leak upward — which is precisely the trap in §9.

---

## 7. Do you still need media queries?

Mostly no, for *layout*. The transcript's point: the breakpoints cover the common device widths, so
you stop hand-writing `@media (min-width: 992px) { … }` just to change column proportions.

But Bootstrap only pre-writes *layout* responsiveness. Custom responsive **font sizes**, **background
images**, **spacing that isn't on the built-in scale**, or a breakpoint at a width Bootstrap doesn't
have — those still need your own media query. The skill isn't obsolete, just used far less often.

---

## 8. The exercises — solved and verified ✅

Site: <https://appbrewery.github.io/bootstrap-layout/>. Each exercise shows a **demo row** (the target)
above an **editable row** (yours). You edit the HTML in the textarea and hit *Apply Changes*.

### Method used — measure, don't guess

The instructor solves these by eye plus trial and error, and gives one genuinely good tip:
**DevTools → toggle device toolbar → Responsive → drag the handle and watch the width readout at the
top** to find exactly which breakpoint a jump happened at.

Rather than eyeballing, this session did the same thing precisely: for each viewport width, measure
every demo box's width, divide by the row's width, multiply by 12. That converts "looks about half"
into an exact column number. Sampling one width inside each band gives the whole spec in six readings:

| Viewport | Band | Exercise 1 | Exercise 2 | Exercise 3 |
| --- | --- | --- | --- | --- |
| 1500px | `xxl` | 6, 6 | 6, 3, 3 | **1, 11** |
| 1300px | `xl` | 6, 6 | 6, 3, 3 | **2, 10** |
| 1100px | `lg` | 12, 12 | **6, 3, 3** | **4, 8** |
| 850px | `md` | 12, 12 | 12, 6, 6 | **6, 6** |
| 650px | `sm` | 12, 12 | **12, 6, 6** | 12, 12 |
| 450px | `xs` | 12, 12 | **10, 10, 10** | 12, 12 |

Bold = the band where the value first changes, i.e. where a class is needed. Reading each column of
that table downward gives the answer directly — **the table *is* the solution.**

### Exercise 1 — "50% desktop, 100% mobile"

Only one row of the table changes: 6/6 at xl and up, 12/12 everywhere below. Below xl is already the
default (§2), so exactly one class is needed:

```html
<div class="row">
  <div class="col-xl-6">50% desktop, 100% mobile</div>
  <div class="col-xl-6">50% desktop, 100% mobile</div>
</div>
```

The instructor first writes `col-xl-6 col-sm-12`, then deletes the `col-sm-12` to make the point that
it changes nothing. Correct here — but see §9 for when deleting it *does* break things.

### Exercise 2 — three columns, three different behaviours

Three distinct bands: `xs` = 10/10/10, `sm`+`md` = 12/6/6, `lg` and up = 6/3/3.

```html
<div class="row">
  <div class="col-10 col-sm-12 col-lg-6">Column 1</div>
  <div class="col-10 col-sm-6  col-lg-3">Column 2</div>
  <div class="col-10 col-sm-6  col-lg-3">Column 3</div>
</div>
```

`col-10` (no infix) is the extra-small case. Note the boxes are *centred-looking* at xs because 10/12
leaves 2/12 of slack — that visual is the clue that it is 10 and not 12.

### Exercise 3 — five bands, a smooth taper

Column 1 gets narrower as the screen gets wider; Column 2 absorbs the difference. Every pair adds to 12.

```html
<div class="row">
  <div class="col-md-6 col-lg-4 col-xl-2 col-xxl-1">Column 1</div>
  <div class="col-md-6 col-lg-8 col-xl-10 col-xxl-11">Column 2</div>
</div>
```

`xs` and `sm` are both 12/12 = the default, so no class is needed for either. The demo's own source
writes `col-sm-12` anyway; harmless, just noise.

### Verification

Every solution was checked against the demo row programmatically — same measurement harness, comparing
each of *my* boxes' pixel widths to the corresponding *demo* box at six viewport widths:

**3 exercises × 6 bands = 18 checks, 18 PASS.** Widths matched to within 1px everywhere.

---

## 9. ⚠️ THE TRAP — `col-10` silently leaks upward

This is the most valuable thing in the lesson and the video **does not mention it**.

Walking through Exercise 2, the instructor says of the `sm` band: *"our Column 1 is going to take up
the full width of the row"* — and adds no class for it, on the reasoning that full width is the
default. That reasoning was true in Exercise 1. It is **false** here, because `col-10` was added for
extra-small — and `col-10` has no upper bound. It starts at 0px and applies **forever upward** until
something overrides it.

Tested directly on the page at a 700px viewport (the `sm` band):

| Column 1's classes | Measured at 700px | Target |
| --- | --- | --- |
| `col-10 col-lg-6` | **10 / 12** ❌ | 12 |
| `col-10 col-sm-12 col-lg-6` | **12 / 12** ✅ | 12 |

Columns 2 and 3 escape the bug only by accident — they happen to have a `col-sm-6` that overrides the
`col-10`. Column 1 has nothing between `col-10` and `col-lg-6`, so `col-10` survives through both the
`sm` and `md` bands. The exercise page's own answer markup carries `col-sm-12` explicitly, confirming
it is required and not decoration.

**The rule:** `col-sm-12` is redundant *only when nothing smaller is set*. The moment you write a
no-infix `col-N`, going back to full width at a higher breakpoint becomes an **explicit** act —
you must write `col-sm-12` (or `col-md-12`, wherever it should return).

Generalised: **there is no "unset" in Bootstrap's grid, only "override".** Every `col-*` you write is
a floor that persists upward through every larger breakpoint until you overwrite it. When debugging a
layout that is wrong on *one* screen size, read the div's classes bottom-up and ask *"which class is
still in force at this width?"* — not *"which class did I write for this width?"*

This is the same family as the Flexbox mistakes from EX 9.4 and EX 10.0: the layout reasoning was
right, but **which rule actually owns the value at this moment** was wrong. Worth watching for.

---

## 10. Quick reference

```html
<!-- skeleton -->
<div class="container">      <!-- or container-fluid for edge-to-edge -->
  <div class="row">
    <div class="col-12 col-md-6 col-lg-4">…</div>
  </div>
</div>
```

- Breakpoints: *(none)* `<576` · `sm ≥576` · `md ≥768` · `lg ≥992` · `xl ≥1200` · `xxl ≥1400`
- Container caps: 540 / 720 / 960 / 1140 / 1320 px
- `container-{bp}` = full width **below** `{bp}`, capped from `{bp}` up. `container-fluid` = always 100%.
- `col` = equal share · `col-N` = N/12 · `col-auto` = content width
- Breakpoints are `min-width` — **"this size and up"**, always
- Numbers in a row should total 12; overflow wraps to a new line (columns don't shrink)
- Classes stack mobile-first; **larger wins by source order, not specificity**
- No-infix `col-N` applies from 0px upward — override it explicitly to get full width back

## Selva-speak

- *"Container wraps rows, rows wrap columns, columns wrap content."*
- *"Bootstrap's grid is not CSS Grid — it's Flexbox with the homework done."*
- *"`container-{bp}` = the size at which it STOPS being full width."*
- *"Breakpoints go up, never down."*
- *"A no-infix `col-10` is not 'mobile only' — it's 'everywhere, until overridden'."*
- *"There is no unset in Bootstrap, only override."*
- *"Measure, then name the number: width ÷ row width × 12."*
