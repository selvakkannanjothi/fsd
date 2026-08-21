# CSS — Styling, Selectors, Cascade, Box Model, Layout & Projects

Source transcripts: `course_content/CSS/` — `intro_to_css.txt`, `how_to_add_css.txt`, `css_selctors.txt`,
`combining_css_selectors.txt`, `css_colors.txt`, `color_vocab_transcript.txt`,
`cascade_specificity_inheritence.txt`, `inspecting_css.txt`, `the_box_model.txt`, `font_properties.txt`,
`css_display_transcript.txt`, `css_positioning.txt`, `css_flag_project.txt`, `poster_motivational.txt`
Practice exercises/projects: `EX 5.1 Adding CSS`, `EX 5.3 CSS Selectors`, `EX 5.4 Color Vocab Project`,
`8.0 CSS Display`, CSS Positioning, Flag of Laos project, Motivational Poster project

## The problem this solves

HTML gives you *content and structure* (from the earlier HTML block), but every page still looks like a
plain 1990s document. **CSS (Cascading Style Sheets)** is the styling layer — the "paint and decor" in
the house analogy from `how_do_websites_actually_work`. This whole section takes you from "why does
styling need its own language" all the way to laying out and positioning elements and building real
CSS-only artwork. If you know API/UI testing already: CSS **selectors** are essentially the same idea as
CSS/XPath locators in Selenium/Cypress — you're identifying elements by tag, class, id, or attribute.

---

## 1. What CSS is & why it exists (`intro_to_css.txt`)

- **CSS = Cascading Style Sheets.** "SS" = *Style Sheet* (a language, like the "ML" in HTML = Markup
  Language). "Cascading" = styles flow **from most general down to most specific**, like a waterfall.
- **The problem historically**: early HTML had no styling. When styling was crammed into HTML tags, you
  couldn't separate content from styling and files ballooned. CSS enforces **separation of concerns**
  (analogy: car manufacturing — one person does headlights, another wheels; modular).
- Deprecated styling tags from HTML 3.2 (1997) — `<font>`, `<center>`, and attributes like `color`,
  `face`, `size` — **should no longer be used**. Modern styling all lives in CSS.
- Other stylesheet languages exist (**Sass** = "Syntactically Awesome Style Sheet", **Less** = "Leaner
  CSS") but CSS is the essential one.
- Demo: `appbrewery.github.io/just-add-css` — toggles CSS on/off; the HTML never changes, only the CSS.

---

## 2. Three ways to add CSS (`how_to_add_css.txt`, EX 5.1)

Every CSS **rule** = a **property** (what to change) + a **value** (what to set it to), separated by a
colon: `color: blue;`. Internal/external rules also need a **selector** + `{ }` curly braces.

| Method | How | Best for |
|---|---|---|
| **Inline** | `style="..."` attribute inside an element's opening tag | A single element / quick test |
| **Internal** | `<style>...</style>` element (conventionally in `<head>`) | Styling one page |
| **External** | separate `.css` file linked via `<link>` in `<head>` | **Multi-page sites (most common)** |

```html
<!-- Inline -->
<h1 style="color: blue">Hi</h1>

<!-- Internal -->
<head>
  <style>
    h1 { color: red; }
  </style>
</head>

<!-- External: in the HTML <head> -->
<link rel="stylesheet" href="./style.css" />
```
```css
/* in style.css */
h1 { color: green; }
```
- `<link>` is a **self-closing** tag with `rel` (relationship = "stylesheet") and `href` (relative file
  path — reuses `./` and `../` from the multi-page-websites block).
- `style` is a **global attribute** — works on any element.

---

## 3. Selectors — targeting elements (`css_selctors.txt`, EX 5.3)

| Selector | Symbol | Targets | Notes |
|---|---|---|---|
| Element | *(tag name)* | all elements of that tag | e.g. `p { }` — hits every `<p>` |
| Class | `.` | all elements with that class | **reusable** across many/different elements |
| ID | `#` | the one element with that `id` | must be **unique — one per page** |
| Attribute | `[attr]` / `[attr="value"]` | elements having that attribute (optionally a value) | e.g. `li[value="4"]` |
| Universal | `*` | **everything** | e.g. `* { text-align: center; }` |

```css
p            { color: red; }      /* element */
.red-text    { color: red; }      /* class  — HTML: class="red-text" */
#main        { color: green; }    /* id     — HTML: id="main" */
p[draggable] { color: red; }      /* attribute present */
*            { text-align: center; }
```
- Class/ID names are **case-sensitive and must match exactly** — copy-paste them to avoid typos.
- An element selector hits *all* matching tags — to style just one of three `<h2>`s, give it an id.

---

## 4. Combining selectors (`combining_css_selectors.txt`)

Uses the DOM **family metaphor**: parent → child → grandchild; ancestor → descendant.

| Combinator | Syntax | Meaning |
|---|---|---|
| **Group** | `A, B` (comma) | apply the same rule to A *and* B |
| **Child** | `A > B` | B that is a **direct child** of A (exactly one level deep) |
| **Descendant** | `A B` (space) | B anywhere inside A (**any depth**) |
| **Chaining** | `AB` (no space) | one element matching *all* — e.g. `li.done`, `h1#title.big` |

```css
h1, h2      { color: blueviolet; }   /* group */
.box > p    { color: firebrick; }    /* direct child paragraph */
.box li     { color: blue; }         /* descendant li at any depth */
li.done     { color: seagreen; }     /* an <li> that also has class "done" */
ul p.done   { font-size: 0.5rem; }   /* combos mix freely */
```
- **Chaining takes NO spaces** — one space changes it to a descendant selector (different meaning!).
- **In a chain the element selector must come first**: `li.done` ✔, `.doneli` ✘ (reads as one class name).
- Preference: use the **descendant** (space) over child (`>`) unless you specifically need only direct
  children.

### Direct-child selector alternatives (Flexbox `EX 9.1 Flex Direction`)

When a rule should only touch **direct children** (e.g. `.container div { flex-basis: 100px; }` matching
only the first-level `<div>`s, not any nested ones), these all work:

| Selector | What it targets |
|---|---|
| `.container div` | All `div` descendants (any depth) — the loose/default version |
| `.container > div` | Only **direct child** `div`s — most precise, matches the intent here |
| `.container > *` | All direct children regardless of tag — uses the universal selector |
| `.container > :is(div)` | Same as `> div` but composable — extend to more tags: `:is(div, p)` |

---

## 5. The Cascade, Specificity & Inheritance (`cascade_specificity_inheritence.txt`)

When multiple rules target the same element and **conflict**, the browser decides a winner. Four
categories, checked in this order (this is *the* CSS debugging tool — "why isn't my CSS applying?"):

> **1. Position → 2. Specificity → 3. Type → 4. Importance**

- **Position** — when everything else ties, the rule **lower in the file wins** (water settles at the
  bottom of the cascade).
- **Specificity** — most → least specific: **ID (`#`) → attribute (`[]`) → class (`.`) → element**.
  (Officially attribute == class, but in practice attribute usually wins.)
- **Type** — ascending importance: **external → internal → inline**. A category can win on specificity yet
  *lose* on type (an inline style beats an ID selector).
- **Importance** — `!important` (written `color: red !important;`) is the "Top Trump" — overrides
  everything: inline, ID, position, all of it. Use sparingly.
- **Inheritance** — some properties (e.g. `font-family`) are automatically passed down to children even
  without a rule on them. Seen clearly in DevTools' Computed tab.

Worked mnemonics from the lesson's quizzes: ID beats class (specificity) → but inline beats ID (type) →
but `!important` beats all (importance); two equal classes → position (lower) wins.

---

## 6. Color properties (`css_colors.txt`, EX 5.4)

- `color` = **text** color; `background-color` = element's **background**. (Check MDN when unsure which
  property does what.)
- Three ways to specify a color:
  1. **Named** — keyword like `cornflowerblue`, `antiquewhite`, `whitesmoke`, `coral` (see MDN named-color
     list).
  2. **Hex** — `#5D3891`-style codes (a compact number for the color).
  3. **RGB** — three channels 0–255: `rgb(93, 56, 145)` = 93/255 red, 56/255 green, 145/255 blue.
- Tools: **colorhunt.co** for ready-made designer palettes (background/main/accent tones); copy the hex.

---

## 7. Font properties (`font_properties.txt`, "6.1 Font Properties")

- **`font-size` units:**
  - `px` (pixels) and `pt` (points) are **static/absolute** sizes.
  - `em` = relative to the **parent's** font-size (`2em` = 2× parent). Gets confusing when deeply nested.
  - `rem` = relative to the **root** (`<html>`) font-size. **Recommended** — predictable, only the root
    changes it.
  ```css
  body { font-size: 20px; }
  h1   { font-size: 2em; }   /* = 40px (2 × parent) */
  h2   { font-size: 2rem; }  /* = 2 × the <html> root size, ignores parent */
  ```
- **`font-weight`**: `normal` / `bold`, relative `lighter` / `bolder` (±100), or numeric `100`–`900`.
- **`font-family`**: preferred font first, then a **generic backup** after a comma so users without the
  font still get something close. Generics: `sans-serif` (no "feet"), `serif` (little feet/decorations),
  `monospace` (typewriter — equal widths), `cursive`, `fantasy`. **Multi-word names need quotes**:
  `font-family: "Times New Roman", serif;`
- **Google Fonts** (`fonts.google.com`): pick font + weight(s) → copy the **`<link>`** into the `<head>`
  (outside `<style>`, placement matters) → apply the CSS rule. Works for everyone regardless of OS.
- **`text-align`**: `left` / `right` / `center`, plus `start` / `end` (adapt to text direction — `start`
  is right-side for right-to-left languages like Arabic).
- `font_properties_practice_website.txt` is **not a transcript** — just a link to
  `appbrewery.github.io/css-inspection/` (the practice site for the next lesson).

---

## 8. The Box Model (`the_box_model.txt`)

Every element is a **box**. From inside out: **content (width/height) → padding → border → margin**.

- **`width` / `height`** — content size, in `px` or `%` (percent of available width).
- **`padding`** — space *inside* the border, between content and border.
- **`border`** — shorthand `thickness style color`, e.g. `border: 30px solid black;` (styles: `solid`,
  `dashed`, …). **Border grows outward — it does NOT change width/height.**
- **`margin`** — space *outside* the border, between this box and others. Two adjacent 10px margins =
  20px gap.
- **Multi-value shorthand (clockwise: top, right, bottom, left):**
  - 4 values → `padding: 0px 10px 20px 30px;` (T R B L)
  - 2 values → `border-width: 0px 20px;` (top/bottom, then left/right)
  - 1 value → `margin: 10px;` (all four sides)
- **`<div>`** (Content Division Element) — an invisible container to group content for styling/layout;
  invisible until you add CSS. Give divs ids/classes to style them separately.
- **Gotchas**: `<p>` has a default `1em` top/bottom margin — set `margin: 0` to remove it. To make two
  boxes touch corner-to-corner you compute total width (`content + padding×2 + border×2`) and push with
  `margin-left`.
- **Tooling**: the **Pesticide** Chrome extension ("night-vision goggles") outlines every box so you can
  see invisible divs; DevTools' box-model diagram (Styles tab) shows and live-edits each layer.

---

## 9. Inspecting CSS with Chrome DevTools (`inspecting_css.txt`)

- Open: right-click → **Inspect**, or **Ctrl+Shift+I** (Win) / **Cmd+Option+I** (Mac) / **F12**.
- **Elements → Styles**: shows applied rules and their source file; **struck-out** rules were overridden
  (the cascade in action). Click the source filename to jump to it.
- **Computed tab**: the final resolved values (colors shown as RGB), and where inherited properties (like
  `font-family`) come from — cuts through the strike-through clutter.
- **Live editing**: add rules with `+`, disable a rule by clicking to strike it. **Edits never touch the
  real source file** — they reset on refresh (same point made in the earlier DevTools lesson). Editing
  another site (e.g. TechCrunch) is local-only and harmless.
- **CSS Overview** (DevTools' own ⋮ → More tools → CSS Overview → Capture overview): summarizes a page's
  colors and fonts — great for lifting exact hex codes/fonts from a site you admire.

---

## 10. The Display property (`css_display_transcript.txt`, "8.0 CSS Display")

Controls how an element flows in layout. Key values:

| Value | Behaviour | width/height settable? |
|---|---|---|
| `block` | takes full width; next element stacks **below** (default for most) | yes |
| `inline` | sits on the **same line** until it wraps; sizes to content | **no** |
| `inline-block` | same line as neighbours **and** you can set width/height | yes |
| `none` | element disappears entirely | — |

- `<span>` is `inline` by default — used to style a run of text mid-sentence.
- **#1 gotcha**: `inline` elements **ignore width/height**. Use `inline-block` when you need both sizing
  and same-line flow.
- EX 8.0: same three 200×200 squares → `inline-block` lines them up horizontally; `block` stacks them
  vertically. Layout changes with *only* the display value.

---

## 11. Positioning (`css_positioning.txt`, Section 7 lecture 45)

The `position` property + offset properties `top` / `right` / `bottom` / `left`:

| Value | Positioned relative to | In normal flow? |
|---|---|---|
| `static` | nothing — normal HTML flow (**the default**; `top`/`left` do nothing) | yes |
| `relative` | **its own** original static position | yes |
| `absolute` | nearest **positioned ancestor**, else the top-left of the page | **no (removed from flow)** |
| `fixed` | the **browser window** — stays put while scrolling | no |

- **Common idiom (memorize)**: **parent `position: relative` + child `position: absolute`** → position
  the child precisely inside the parent. Without a positioned ancestor, absolute falls back to the page's
  top-left corner.
- **`z-index`** — stacking order on the Z-axis (toward the viewer). Default `0`; higher sits on top;
  negative (e.g. `-1`) pushes behind. Absolute elements sit on a separate layer.
- **Circles**: `border-radius: 50%` on a square (`width == height`) = a perfect circle (`5px` = slight
  round, `50px` = app-icon round). Note `50%` offsets place the box's **top-left corner**, not its centre.
- Positioning sits **outside** margin in the box model.

---

## 12. Projects (consolidation)

- **Color Vocab flashcards** (`color_vocab_transcript.txt`, EX 5.4) — Spanish colour vocab site.
  Reinforces: **creating and linking an external `.css`** at the correct file path, ID selectors
  (`#rojo { color: red; }`), a shared class (`.color-title { font-weight: normal; }`) so only flashcard
  titles change, and sizing images in CSS (`img { height: 200px; width: 200px; }`). Trick: temporarily
  set `* { background-color: red; }` to confirm the stylesheet is actually linked, then delete it.
- **Flag of Laos** (`css_flag_project.txt`) — pure HTML/CSS flag. Consolidates combining selectors +
  specificity + cascade + positioning. HTML is deliberately class-less, so you target **craftily** with
  `.flag > div`, `.flag > div > div`, etc. Red `.flag` 900×600, blue band 100%×300, white circle 200×200
  with `border-radius: 50%`, centred via relative-parent/absolute-child. Reset `<p>` margins to `0`
  (default margins push the circle off-centre). Get exact hex colours via DevTools **CSS Overview**.
- **Motivational Poster** (`poster_motivational.txt`) — meme/poster site. Bordered image
  (`border: 5px white`), black background, big uppercase title in Google Font **Libre Baskerville**,
  caption paragraph. **Simple centring** (proper centring is "a whole science" saved for later): wrap all
  three in one classed `<div>`, `width: 50%` + `margin-left: 20%` (horizontal), `margin-top: 100px`
  (vertical, by eye), image `width: 100%`. Learn **`text-transform: uppercase`** yourself from the docs.

---

## Quick reference — CSS syntax cheat sheet

```css
selector { property: value; }        /* the shape of every rule */

/* selectors */
p {}  .cls {}  #id {}  [attr="v"] {}  * {}
h1, h2 {}   .box > p {}   .box li {}   li.done {}   /* group / child / descendant / chain */

/* common properties */
color / background-color: red | #5D3891 | rgb(93,56,145);
font-size: 20px | 12pt | 2em | 2rem;    font-weight: 100–900 | bold;
font-family: "Times New Roman", serif;  text-align: center;
width / height: 200px | 50%;
padding / margin / border-width: 10px  (all) | 10px 20px (TB LR) | 0 1px 2px 3px (T R B L);
border: 30px solid black;               border-radius: 50%;   /* circle */
display: block | inline | inline-block | none;
position: static | relative | absolute | fixed;   top/right/bottom/left: 50px;   z-index: 1;
```

## Why this matters going forward

CSS is the backbone of everything visual from here on. The **box model** and **display**/**position**
properties are the foundation for the next two big topics — **Flexbox** and **Grid** — which are just
higher-level, easier layout systems built on these same boxes (and which finally solve the "centring is
hard" problem this section flagged). **Selectors** carry over unchanged into JavaScript
(`document.querySelector` uses the exact same syntax) and into every framework (React, etc.). And the
DevTools + cascade debugging workflow is how you'll diagnose styling for the rest of your web-dev career.
