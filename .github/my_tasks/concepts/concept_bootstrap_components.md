# Bootstrap — Components, Examples & Spacing Utilities (Module 11, Lesson 11.2)

Source transcript: `course_content/11.0 Bootstrap/11.2 bootstrap_components_transript.txt`
Starter + build: `course_content/11.0 Bootstrap/EX 11.2 Bootstrap Components/`
**Status: the "Move It" website is BUILT — all five sections present, carousel challenge solved
correctly. Audit + the three things still worth fixing are in §10.**
Builds on: `concept_bootstrap_layout.md` (container/row/col — the carousel challenge is literally a
layout-lesson callback), `concept_css.md` (the cascade, `!important`), `concept_flexbox.md`.

---

## The problem this solves

Lesson 11.0 gave one thing: a responsive **grid**. That gets boxes in the right places, but every box
is still empty. A real navbar with a working hamburger menu is a few hundred lines of CSS plus
JavaScript. A carousel with indicators, arrows, and slide transitions is more. Nobody hand-writes
those twice.

Bootstrap's answer: **ship them pre-built and pre-styled, reachable by class name.** You write
`<button class="btn btn-success">Ok</button>` and get a green button with a font, padding, rounded
corners, a hover animation and a focus ring — all of which you already know how to write by hand, and
none of which you now have to.

The honest framing of this whole lesson: **it is not really a coding lesson, it is a shopping
lesson.** The skill being taught is *find the right snippet, paste it, and know which parts are safe
to change.* That sounds trivial until you paste something and half the styling is missing — which is
exactly what happens in §6.

---

## 1. Bootstrap's three toolboxes

The docs are split into three sections, and knowing which one you are in saves a lot of hunting:

| Toolbox | What it gives you | Example | Covered in |
| --- | --- | --- | --- |
| **Layout** | where boxes go | `container`, `row`, `col-lg-6` | lesson 11.0 |
| **Components** | pre-built *things* | `btn`, `card`, `navbar`, `carousel` | **this lesson** |
| **Utilities / Helpers** | one-property tweaks | `mt-3`, `d-flex`, `text-center`, `shadow-lg` | **this lesson, §8** |

A component is a *noun* (a navbar, a card). A utility is an *adjective* (with a bit more margin,
centred, hidden). Most real markup is one component class plus a handful of utility classes — look at
any line of the Move It page and you will see exactly that shape.

---

## 2. Buttons — the colour vocabulary, and the warm-up challenge

The lesson's first challenge: *"put in a green button that says Ok."*

```html
<button class="btn btn-success">Ok</button>
```

Two classes doing two different jobs, and this pattern repeats across nearly every Bootstrap
component:

- **`btn`** = *"be a Bootstrap button"* — the shape, padding, font, radius, hover and focus states.
- **`btn-success`** = *"in the green colour role"* — colour only.

The colour names are **semantic roles, not colours**, and they are the same everywhere in Bootstrap
(`text-bg-primary`, `alert-danger`, `border-warning` …):

| Role | Colour | Means |
| --- | --- | --- |
| `primary` | blue `#0d6efd` | the main action — *Buy*, *Contact Us*, *Download* |
| `secondary` | grey | the lesser action beside it |
| `success` | green `#198754` | it worked / go ahead / OK |
| `danger` | red | destructive — delete, cancel |
| `warning` | yellow | careful |
| `info` | cyan | neutral note |
| `light` / `dark` | — | tonal |

`btn-outline-success` is the same green as a border and text instead of a fill — that is the one
actually used on the Move It navbar's *Check* button.

**Why "semantic, not colour" matters:** naming the *job* rather than the *hue* is what lets one
attribute repaint the whole site in §9. If the class had been `btn-green` it could not follow you
into dark mode.

---

## 3. Where the code actually comes from — four different shops ⭐

This is the most practically useful part of the lesson and it is easy to miss, because the instructor
moves between four different parts of the Bootstrap site without ever saying "these are four
different places."

| Where | What is there | Move It used it for |
| --- | --- | --- |
| **Docs → Components** | one component at a time, with every variant + the API | buttons, carousel |
| **Examples** (`/docs/5.3/examples/`) | whole *sections* of real pages — Headers, Heroes, Features, Footers | navbar layout, hero, features, footer |
| **Icons** (`icons.getbootstrap.com`) | ~2000 free SVG icons, royalty-free even commercially | box-seam, briefcase, bus-front, chat-square-heart, chevron-right |
| **Themes** | whole paid site templates | (mentioned only) |

**Docs vs Examples is the distinction to keep.** Docs give you *a* button. Examples give you *a hero
section that already contains a heading, a paragraph, two buttons and an image, laid out and spaced*.
For building a page fast, Examples is the better shop — and it is the one a beginner never finds,
because it is not in the main docs nav.

### The extraction workflow (worth memorising as a sequence)

The instructor never names this, but he does it four times:

1. Open the Examples page and find the section you want.
2. Right-click → **Inspect**.
3. **Hover upward through the DOM tree** — parent, grandparent — watching the blue highlight on the
   page, until the highlight covers *exactly* the region you want and no more.
4. Right-click that node → **Copy** → **Copy element**.
5. Paste into your HTML at the right position.
6. Replace `src`, `alt`, and text.

Step 3 is the actual skill. Too shallow and you get one card without its wrapper; too deep and you
drag in the example page's own `<main>` and its layout. It is the same "which element owns this?"
question that has already bitten twice (the `<ul>` vs `<li>` padding in EX 9.4, `col-10` leaking in
11.0) — just aimed at *copying* instead of *styling*.

---

## 4. ⚠️ Two CDN links — CSS gives looks, JS gives behaviour

This is the lesson's best debugging moment. The navbar is pasted in, it looks perfect, the hamburger
button appears at narrow widths — **and clicking it does nothing.**

Bootstrap ships as **two** files and the starter only had one:

```html
<!-- in <head> — STYLING. Without it: an unstyled wall of text. -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.x/dist/css/bootstrap.min.css" rel="stylesheet" ...>

<!-- last thing before </body> — BEHAVIOUR. Without it: it looks right but nothing moves. -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.x/dist/js/bootstrap.bundle.min.js" ...></script>
```

**The rule to keep: if a component *looks* right but does not *move*, you are missing the script tag.**
Everything below is dead without it:

| Needs JS | Pure CSS, works without JS |
| --- | --- |
| navbar hamburger (collapse) | button colours and hover |
| dropdown menus | the grid, containers, columns |
| **carousel** (arrows, indicators, sliding) | cards, spacing utilities |
| modals, tooltips, popovers, toasts, accordion, offcanvas | typography, borders, shadows |

Three details worth carrying:

- **`bundle` in the filename** means Popper.js (the positioning engine dropdowns and tooltips need) is
  included. `bootstrap.min.js` alone is *not* enough for dropdowns.
- **Position matters** — just before `</body>`, so the HTML exists before the script tries to wire it
  up. Same reason `<script>` goes at the bottom generally.
- **CSS and JS versions should match.** The starter file pairs `5.3.0-alpha2` CSS with `5.3.0-alpha3`
  JS; the built page pairs `5.3.0-alpha2` CSS with `5.3.8` JS. Both happen to work, but a mismatched
  pair is a real source of "it works in the tutorial, not for me" bugs. See §10.

*"No JavaScript knowledge needed yet"* is true and is the point — you are consuming someone else's
JS through `data-bs-*` attributes. Those attributes (`data-bs-toggle="collapse"`,
`data-bs-target="#navbarSupportedContent"`, `data-bs-slide="next"`) are how the pasted HTML *tells*
Bootstrap's JS what to do. **Delete a `data-bs-*` attribute and the component goes quiet** — worth
knowing before you "tidy up" someone else's snippet.

---

## 5. The Move It build, section by section

A one-page site for a fictional moving startup, assembled almost entirely by pasting.

| # | Section | Came from | What was actually edited |
| --- | --- | --- | --- |
| 1 | Navbar | Docs → Navbar (the search-bar variant) | deleted the `disabled` list item · renamed Link→About, Dropdown→Services · `navbar-brand` text → "Move It" + SVG icon · Search→Postcode, button→Check |
| 2 | Hero | Examples → Heroes | image `src` → `moving-van.jpg` · `h1`, `p`, both button labels from `website-text.txt` |
| 3 | Features | Examples → Features | 3× heading + paragraph · 3 icon SVGs · 3 chevron SVGs · **plus the `.feature-icon` custom CSS (§6)** |
| 4 | Carousel | Docs → Carousel (with-indicators variant) | 3 image `src`s · **wrapped in `<div class="container">`** — the challenge |
| 5 | Footer | Examples → Footers | barely touched |

### The carousel challenge — and why it is a layout question in disguise

The brief: *"the images don't go all the way to the edge, they are aligned with the rest of the
content."* The pasted carousel is full-bleed and comes out taller than the viewport.

The fix is **not** a carousel property. It is `container` from lesson 11.0:

```html
<div class="container">                     <!-- ← the whole answer -->
  <div id="carouselExampleIndicators" class="carousel slide">
    …
  </div>
</div>
```

Because `.container` is capped at 540 / 720 / 960 / 1140 / 1320px, and the slide images are
`class="d-block w-100"` (`width: 100%`), the images inherit the container's width — so they line up
with the hero and features above, *and* the height problem solves itself, because the image is scaled
by width and its aspect ratio does the rest.

**The transferable idea: sizing a component is usually its parent's job, not the component's.**
Bootstrap components are almost all `width: 100%` by design, precisely so that the container decides.
That is the same lesson as the chessboard in EX 10.0 — *"you don't size the squares, you size the
board."*

---

## 6. ⚠️ Copy-paste leaves three kinds of debt

This is where the lesson stops being trivial. Pasting a snippet gets you **the HTML only**. Three
things do *not* travel with it, and all three bit the Features section:

### Debt 1 — custom CSS that was never Bootstrap's

The pasted Features section looked wrong: the icons had no blue rounded squares. The transcript's
diagnosis method is the useful bit:

> Inspect the element on the *example* page and **read which file each rule came from.**
> Rules from `utilities.css` / `bootstrap.css` → they come with Bootstrap, you already have them.
> Rules from some *other* filename → that page's own custom CSS, and **you have to copy it yourself.**

Here the missing rule was `.feature-icon` (verified: `feature-icon` appears **nowhere** in
`bootstrap@5.3.0-alpha2`, so it is genuinely custom):

```css
.feature-icon { width: 4rem; height: 4rem; border-radius: 0.75rem; }
```

Everything *else* on that div — `d-inline-flex`, `align-items-center`, `justify-content-center`,
`text-bg-primary`, `bg-gradient`, `fs-2`, `mb-3` — is real Bootstrap and arrived with the HTML.
So the one hand-written rule creates the box; Bootstrap's utilities colour and centre it.

**Generalised rule: DevTools' right-hand "source file" column tells you what you are missing.**
If a pasted section looks wrong, that column is the first place to look — not the class names.

### Debt 2 — icons don't travel

The Examples pages use an **SVG sprite** — `<svg class="bi"><use xlink:href="#briefcase"></use></svg>`
— which points at a `<symbol>` defined elsewhere on *that* page. Copy the `<svg>` and you copy a
pointer to something that does not exist in your file, so it renders as **an empty box of the right
size**. Nothing errors; nothing appears.

Fix used: download the icons from `icons.getbootstrap.com` and reference them as ordinary images.
(That has its own cost — see §7.)

> This is still live in the built page: the footer's
> `<svg class="bi"><use xlink:href="#bootstrap"></use></svg>` is a leftover sprite reference with no
> matching symbol, so it renders as a 40×32 invisible gap. See §10.

### Debt 3 — placeholder content

`src="…/bootstrap-docs/…"`, `alt="Example image"`, lorem-ish body copy. The `src` and the visible text
get noticed because they are visible. **`alt` does not**, because it is invisible unless the image
breaks or a screen reader reads it. `alt="Example image"` shipped in both the course solution and the
built page.

---

## 7. SVG icons — `<img>` vs inline `<svg>`, and what it silently costs ⭐

The transcript offers three ways to use a Bootstrap icon and says *"it really is up to you"*. It is
not quite — the choice has consequences the video does not mention, and they explain something the
video does with no explanation at all (why every icon needs a hand-written `height="30"`).

```html
<!-- A: inline SVG — paste the whole <svg> markup -->
<svg class="bi" width="30" height="30" fill="currentColor" viewBox="0 0 16 16"><path d="…"/></svg>

<!-- B: as an image — what this lesson uses -->
<img src="./briefcase.svg" alt="briefcase icon" height="30">

<!-- C: sprite <use> — what the Examples pages use, and what does NOT survive copy-paste -->
<svg class="bi"><use xlink:href="#briefcase"></use></svg>
```

**The rule that explains all of it: an SVG loaded through `<img>` is a separate, isolated document.
Your page's CSS cannot reach inside it.** Two things follow, both verified in the built page:

1. **Bootstrap's own icon sizing rule cannot apply.** Bootstrap ships
   `.icon-link > .bi { width: 1em; height: 1em; }` — but `class="bi"` on an `<img>` selects the image
   element, not anything inside the SVG, and there is no `.bi` element to match anyway. Measured: the
   chevron renders at its **intrinsic 16×16**, not `1em`. That is exactly why the video has to add
   `height="30"` by hand to every single icon. With inline SVG (option A) Bootstrap would have sized
   them.
2. **You cannot recolour it from your CSS.** `color: red` on the parent does nothing; the icon's
   `fill="currentColor"` resolves inside the SVG's own document, not yours. Inline SVG *does* inherit
   `currentColor` — which is the entire reason Bootstrap Icons ship with `fill="currentColor"`.

The one thing that *does* cross the boundary is the **colour scheme**: the browser propagates
light/dark into the image document, so `currentColor` → the default text colour → flips. Verified on
the built page: the same unchanged `<img src="./box-seam.svg">` renders **black in light mode and
white in dark mode**. So the icons do survive §9's dark-mode switch — by luck of how
`fill="currentColor"` is defined, not because your CSS reached them.

**Choose by what you need:** `<img>` for clean markup on a static icon · **inline `<svg>` whenever the
icon must change colour with its context, size from CSS, or animate** (a hover state, an icon inside
a coloured button, an icon that must match a theme).

---

## 8. ⚠️ Spacing utilities — and the video gets x and y backwards

The naming formula, and it is completely regular:

```
{property}{sides}-{size}                 →  mt-3   pb-0   mx-auto
{property}{sides}-{breakpoint}-{size}    →  mb-lg-0   me-sm-3   px-md-4
```

**Property** — `m` = margin (space *outside* the border), `p` = padding (space *inside*, between the
border and the content). Straight from `concept_css.md`'s box model.

**Sides:**

| Letter | Sets | Note |
| --- | --- | --- |
| *(none)* | all four | `m-3` |
| `t` / `b` | top / bottom | |
| `s` / `e` | **s**tart / **e**nd | **left / right in LTR.** Bootstrap 5 uses logical properties so layouts auto-flip in RTL languages. (Bootstrap 4 used `l`/`r`.) |
| `x` | **left + right** — the **horizontal** axis | |
| `y` | **top + bottom** — the **vertical** axis | |

### 🚨 THE VIDEO SAYS THIS BACKWARDS — this lesson's headline finding

> *"if you want to set the margin for both the top and the bottom, you'll use the x-axis. And if you
> want to set the margin or padding for the left and the right, then you can use that y-axis."*

That is **exactly inverted**. Verified by reading `bootstrap@5.3.0-alpha2` directly:

```css
.mx-3 { margin-right: 1rem !important; margin-left:   1rem !important; }   /* x = HORIZONTAL */
.my-3 { margin-top:   1rem !important; margin-bottom: 1rem !important; }   /* y = VERTICAL   */
```

The instructor then *gets it right* one sentence later — *"my-3 … set the margin for the y-axis"* —
which is why it slides past on a first watch. The class names are correct throughout the code; only
the spoken definition is swapped.

**Memory hook, borrowed from maths and from Grid:** it is the same x/y as a graph — **x runs across,
y runs up and down.** Identical to `gap` splitting into `column-gap` (x) and `row-gap` (y), and to
`translateX` / `translateY`. Bootstrap did not invent a new convention; the video just misread it.

*(This is the third video error caught in this course — after `flex: 2` being called "grow 2 shrink 2"
in flex-sizing, and the `col-sm-12` omission in 11.0. Pattern worth keeping: **the class names and the
code are reliable; the spoken explanations are not. Check the stylesheet.**)*

### The size scale — verified values

| Class suffix | Value | Pixels (at the 16px root) |
| --- | --- | --- |
| `-0` | `0` | 0 |
| `-1` | `0.25rem` | 4px |
| `-2` | `0.5rem` | 8px |
| `-3` | `1rem` | 16px |
| `-4` | `1.5rem` | 24px |
| `-5` | `3rem` | 48px |
| `-auto` | `auto` | margin only |

The scale is deliberately short. The transcript's *"5 is usually the maximum you'll need"* is not a
guideline — **5 is the maximum that exists.** There is no `mt-6`; it silently does nothing.

Three more things that are true and not in the video:

- **Every spacing utility carries `!important`.** That is why they always win over your own CSS — and
  why you cannot override `mb-2` with a plain class of your own. It is `!important` from cascade rule
  4 in `concept_css.md`, used deliberately: utilities are meant to be the last word.
- **`mx-auto` is the centring trick** — `margin-left: auto; margin-right: auto`, the classic "centre a
  block". It is used in the Move It hero (`<div class="col-lg-6 mx-auto">`) to centre the paragraph
  column. `my-auto` exists too; **`p-auto` does not** (padding cannot be `auto`).
- **⚠️ `pe-` is overloaded.** `pe-0`…`pe-5` are `padding-right`, but `pe-none` / `pe-auto` are
  **`pointer-events`**. Same prefix, unrelated property.
- **Negative margins are off by default.** `.m-n1` does not exist in the stock build (verified: zero
  matches) — it is an opt-in Sass flag.

### Decoding practice — read these off the built page

| Class | Means |
| --- | --- |
| `mb-2` | margin-bottom 0.5rem — the footer example the transcript decodes |
| `px-4 pt-5 my-5` | padding L+R 1.5rem, padding-top 3rem, margin top+bottom 3rem |
| `me-auto` | margin-right auto → **shoves everything after it to the far right** (this is what pushes the navbar's search form to the right edge — the same `margin-left:auto` navbar trick from flex sizing) |
| `mb-2 mb-lg-0` | 0.5rem bottom margin, **removed from 992px up** — the breakpoints-are-min-width rule from 11.0 applied to spacing instead of columns |
| `me-sm-3` | margin-right 1rem, from 576px up |

That last pair is the real payoff: **the whole breakpoint ladder from lesson 11.0 works on utilities
too, not just on columns** — and every rule from that lesson comes with it, including *"there is no
unset, only override."*

---

## 9. Dark mode — one attribute

```html
<html lang="en" data-bs-theme="dark">
```

That is the whole change. Verified on the built page:

| | light | dark |
| --- | --- | --- |
| `body` background | `#ffffff` | `#212529` |
| `body` text | `#212529` | `#adb5bd` |
| navbar background | `#f8f9fa` | `#2b3035` |

**Why it works at all** ties back to §2. Bootstrap 5.3 defines everything through CSS custom
properties (`--bs-body-bg`, `--bs-emphasis-color`, …) and ships a `[data-bs-theme=dark] { … }` block
that reassigns them. Because your markup asked for *roles* (`text-bg-primary`, `bg-body-tertiary`,
`text-body-emphasis`) instead of *colours*, every element follows automatically. Markup full of
`style="background: white"` would not have moved.

`data-bs-theme` also works on **any element**, not just `<html>` — put it on one `<div>` for a single
dark card on a light page. And once JavaScript arrives, a toggle button is one `setAttribute` call.

---

## 10. Audit of the built page ✅

`EX 11.2 Bootstrap Components/index.html` — all five sections present and functional, rendered and
exercised locally:

| Check | Result |
| --- | --- |
| Bootstrap CSS + JS both loading | ✅ |
| Hamburger menu opens/closes below 992px | ✅ (collapse height 0 → 166px) |
| Services dropdown opens | ✅ |
| **Carousel challenge** — inside `<div class="container">`, arrows advance the slides | ✅ **correct** |
| All 11 images resolve | ✅ |
| Feature icons at 30px inside the blue `.feature-icon` squares | ✅ |
| `.feature-icon` custom CSS copied into `<style>` | ✅ |
| All text replaced from `website-text.txt` | ✅ |

Three things worth fixing — none breaks the page, all three are the same *"invisible leftovers"*
family as Debt 2 and Debt 3 in §6:

1. **`alt="Example image"`** on the hero's `moving-van.jpg` (`index.html:69`) — placeholder alt text
   from the Bootstrap example. Alt text is the one thing that never shows up when you look at the
   page, which is exactly why it survives. The course's own solution has the same bug.
   → `alt="Move It movers loading a van"`.
2. **The footer's ghost SVG** (`index.html:152`) —
   `<svg class="bi" width="40" height="32"><use xlink:href="#bootstrap"></use></svg>` points at a
   sprite symbol that only exists on Bootstrap's own docs page. Verified: no `#bootstrap` element in
   the document, so it renders as a 40×32 invisible gap. Either delete it or swap in
   `<img src="./box-seam.svg" height="32" alt="Move It">` to reuse the brand icon.
3. **CSS/JS version mismatch** — CSS is `5.3.0-alpha2`, JS is `5.3.8`. It works (everything was
   exercised above), but they should be one version. Prefer moving the **CSS up to a stable 5.3.x**
   rather than the JS back to an alpha.

Not bugs, just observations:

- The chevrons render at 16×16 while the feature icons are 30px — deliberate in the video, and now
  explained by §7 (`.icon-link > .bi` cannot reach an `<img>`).
- The warm-up `btn btn-success` "Ok" button is not on the page. Neither is it in the course solution —
  it was a scratch exercise, not part of Move It.
- Dark mode is not applied. It is a one-attribute demo, not a requirement.

---

## 11. Quick reference

```html
<!-- both links, or components look right and do nothing -->
<link href="…/bootstrap.min.css" rel="stylesheet">        <!-- in <head>  → styling  -->
<script src="…/bootstrap.bundle.min.js"></script>          <!-- before </body> → behaviour -->

<button class="btn btn-success">Ok</button>                <!-- component + colour role -->
<div class="container">…</div>                             <!-- size a component via its PARENT -->
<html data-bs-theme="dark">                                <!-- whole-site dark mode -->
```

- **Where to shop:** Docs→Components = one thing · **Examples = whole sections** · Icons = SVGs · Themes = whole sites
- **Extraction:** Inspect → hover *up* the tree until the highlight is exactly right → Copy element
- **Roles, not colours:** `primary secondary success danger warning info light dark`
- **Needs JS:** navbar collapse, dropdowns, carousel, modal, tooltip, accordion, offcanvas
- **Paste debt:** custom CSS you didn't copy · sprite icons that don't travel · placeholder `src`/`alt`/text
- **Spacing:** `{m|p}{ |t|b|s|e|x|y}-{0..5|auto}`, breakpoint infix optional · `0 .25 .5 1 1.5 3` rem
- **`x` = horizontal (left+right) · `y` = vertical (top+bottom)** ← the video says this backwards
- `s`/`e` = start/end (= left/right in LTR) · all utilities are `!important` · `mx-auto` centres · no `-6`
- **SVG via `<img>` is an isolated document** — your CSS can't size or colour it; inline `<svg>` can be styled

## Selva-speak

- *"Layout puts the boxes down; Components fill them; Utilities nudge them."*
- *"A component is a noun, a utility is an adjective."*
- *"Looks right but doesn't move? You forgot the script tag."*
- *"Copy-paste gets you the HTML, never the CSS."*
- *"Read the source-file column, not the class names."*
- *"Sizing a component is its parent's job."*
- *"An `<img>` SVG is a locked room — your CSS has no key."*
- *"x runs across, y runs up and down — the video says it backwards."*
- *"5 is not a guideline, 5 is the ceiling."*
- *"Ask for the role, not the colour — that's what makes dark mode free."*
