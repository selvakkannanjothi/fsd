# HTML Elements — Structure, Lists, Links & Images

Source transcripts: `course_content/HTML/html_part1.txt` → `html_part7.txt`
Practice exercises: `course_content/HTML/EX 2.1 Heading Element` → `EX 3.4 Birthday Invite Project`

## The problem this solves

Knowing that HTML is "the content layer" (from `how_do_websites_actually_work`) isn't enough — you need
the actual vocabulary of tags to write that content. This block of lessons builds that vocabulary from
scratch: how a tag is put together, then six specific elements (heading, paragraph, void elements, lists,
anchor, image), plus the two cross-cutting skills that make any of it readable — **nesting/indentation**
and **attributes**.

## 1. Anatomy of an element (tags vs. elements)

```html
<h1>Hello World</h1>
```

- **Tag** = anything inside angle brackets. `<h1>` is the *opening tag*, `</h1>` is the *closing tag*
  (a closing tag is identified by the `/` right after the opening angle bracket).
- **Element** = opening tag + content + closing tag, the whole thing.
- Opening and closing tag names must match (`<h1>...</h1>`, never `<h1>...</h6>`).

## 2. Heading elements — `h1` … `h6`

- Six levels of heading exist; there is **no `h7`**. Level = importance/hierarchy, like a book's table of
  contents (book title → chapters → sections → subsections).
- Browsers give each level a default size (`h1` biggest, `h6` smallest) purely as a visual cue that you
  wrote the hierarchy correctly — this is *not* how you should do real styling (that's CSS's job later).
- **Convention rules** (won't break the page, but are professional practice):
  1. Only **one `h1`** per page — it's the "book title."
  2. **Don't skip levels** — if you use `h3`, an `h2` should exist somewhere above it. Go in order.
- Practiced in: `EX 2.1 Heading Element` (formatting an unstructured book table of contents into `h1`–`h4`).

## 3. Paragraph element — `p`

- `<p>...</p>` wraps a block of text. Without it, consecutive text runs together on one line with no
  visual or semantic separation.
- **Accessibility reason it matters**: screen readers announce the start/end of each paragraph, letting a
  blind user jump between paragraphs. Plain unwrapped text gives them nothing to navigate by.
- **Lorem Ipsum**: placeholder Latin text (from Cicero, in print use since the 1500s) used so design/layout
  can be tested without realistic-length, natural-looking content having to be hand-written. Get it from
  lipsum.com (also novelty versions: baconipsum.com, broipsum.com, etc.).
- Practiced in: `EX 2.2 Paragraph Element`.

## 4. Void elements — `hr`, `br`

- A **void element** is forbidden from having content, so it has **no separate closing tag** — it
  self-closes: `<hr />`, `<br />`.
  - Careful: the self-closing `/` sits **just before** the final `>` (`<hr />`), which is visually
    different from a closing tag's `/` which sits **right after** the opening `<` (`</p>`).
  - As of HTML5, the trailing `/` is technically optional (`<hr>` and `<hr />` both render identically) —
    but keep writing it, purely so *you* can spot void elements at a glance while reading code.
- **`<hr />`** (horizontal rule) — draws a dividing line; used to separate unrelated blocks of content
  (e.g. an address block from a bio).
- **`<br />`** (break) — forces a line break *inside* a single paragraph, for content that's semantically
  one block but visually needs separate lines (poems, postal addresses).
  - **Don't misuse `<br />` as a substitute for a new `<p>`.** That breaks the screen-reader paragraph
    navigation described above. Use a new paragraph for a new paragraph; use `<br />` only when it's
    genuinely still one paragraph (poem line, address line).
- **Debugging tip**: paste your code and the solution into diffchecker.com and click "Find Difference" to
  spot typos (e.g. a mistyped closing tag) fast.
- Practiced in: `EX 2.3 Void Elements` (poet name/address/bio) and `EX 2.4 Movie Ranking Project`
  (`<hr />` between a title block and a list of ranked movies).
  - Real mistake I made in `EX 2.3`: forgot to wrap the address block in a `<p>` tag before adding
    `<br />` line breaks — see `EX 2.3 Void Elements/mistake.md`. **Lesson: `<br />` still needs a parent
    block element; it doesn't create one.**

## 5. List elements — `ul`, `ol`, `li`

- `<ul>` = **unordered list** → bullet points. Use when item order doesn't matter (e.g. a shopping list).
- `<ol>` = **ordered list** → numbered points. Use when sequence matters (e.g. recipe steps).
- Both need `<li>` (list item) children — a list element with no `<li>`s renders nothing.
- `<ol>` has a `start` attribute (e.g. `start="5"`) to change the number it counts from.
- Practiced in: `EX 3.0 List Elements` (cinnamon roll recipe: two `<ul>`s for ingredient groups, one
  `<ol>` for instructions).

## 6. Nesting and indentation

- Lists can nest **inside a list item**: put a whole new `<ul>`/`<ol>` after the text content of an `<li>`,
  *before* that `<li>`'s closing tag.
  ```html
  <ul>
    <li>A</li>
    <li>B
      <ol>
        <li>B1</li>
        <li>B2</li>
      </ol>
    </li>
    <li>C</li>
  </ul>
  ```
- **Key rule**: the outer `<li>`'s closing tag moves to *after* the nested list closes — it does not close
  immediately after the visible text.
- Indentation itself has no effect on rendering — it's purely for **humans reading the code** to visually
  match opening/closing tags and spot the nesting depth at a glance.
- VS Code auto re-indents on save (⌘S / Ctrl+S), which also doubles as a **debugging aid**: if indentation
  looks wrong after saving (e.g. a list item appears indented under the wrong list), it usually means a
  closing tag is missing somewhere above it.
- Practiced in: `EX 3.1 Nesting and Indentation` (a 4-level-deep nested `ul`/`ol` structure).

## 7. Attributes & the anchor element — `a href`

- An **attribute** adds extra information to an element and always lives inside the **opening tag**:
  `name="value"`, space-separated if there are several. Value goes in double quotes because it's text data,
  not a reserved keyword.
- `<a href="URL">link text</a>` — without the `href` attribute, an `<a>` renders as plain unstyled text
  and does nothing when clicked; `href` is what makes it an active, styled (blue/underlined) hyperlink.
- **Specific vs. global attributes**: `href` only makes sense on `<a>` (element-specific). Some attributes
  work on *any* element regardless of type — e.g. `draggable="true"` (a **global attribute**).
- When unsure what attributes an element supports, check MDN
  (https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a) rather than memorizing every
  element's docs up front.
- Practiced in: `EX 3.2 Anchor Elements` (top-5-favorite-websites list: `<a>` nested inside `<li>` nested
  inside `<ol>`; extra challenge used `<ol start="5">`).

## 8. Image element — `img src alt`

- `<img src="url" />` — a **void/self-closing element** (an image has no meaningful "text content" the
  way a paragraph does — the image itself *is* the content, supplied via `src`).
- `alt="..."` — alternative text description, read aloud by screen readers in place of the image. Always
  add one when the image is meaningful content (skip only when an image is purely decorative).
- Placeholder image services for testing layouts (like Lorem Ipsum, but for photos): picsum.photos
  (`https://picsum.photos/200/200` → random square photo).
- GIFs work identically to JPEG/PNG in `src` — the browser just animates them automatically.
- Practiced in: `EX 3.3 Image Elements` (cat vs. dog picture + `alt` text) and the capstone
  `EX 3.4 Birthday Invite Project`, which combines everything from this whole unit: `h1`/`h2`/`h3`
  headings, an `<img>`, a `<ul>` of items to bring, and an `<a>` link to a map.

## Quick reference table

| Element | Void? | Key attribute(s) | Purpose |
|---|---|---|---|
| `h1`–`h6` | No | — | Heading hierarchy (one `h1`, don't skip levels) |
| `p` | No | — | Paragraph of text; screen-reader navigable |
| `hr` | Yes | — | Visual/thematic divider between content blocks |
| `br` | Yes | — | Line break *within* one paragraph (poems, addresses) |
| `ul` / `ol` | No | `start` (on `ol`) | Bullet / numbered list container |
| `li` | No | — | One list item; must live inside `ul` or `ol` |
| `a` | No | `href` (specific), `draggable` (global) | Hyperlink |
| `img` | Yes | `src`, `alt` | Embed an image; `alt` for accessibility |

## Why this matters going forward

Every later HTML lesson (semantic tags, forms, tables) is just more elements layered on this same mental
model: tag anatomy → attributes in the opening tag → nesting shown through indentation → accessibility as
a first-class concern (paragraphs, `alt`, avoiding `<br />` abuse). CSS (next major topic) will style these
same elements without changing any of the structure built here.
