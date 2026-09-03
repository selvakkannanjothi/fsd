# Agent Memory - Learning Context

## Who I am
- Name: Selva (Jothis)
- Background: Automation tester with Selenium Java, API Testing, Cypress, JavaScript
- Goal: Learn full stack web development from scratch — frontend, backend, databases, and deployment
- Editor: (not specified yet)

---

## My Learning Workflow
Every new lesson follows this exact pattern - always follow it proactively:

1. **Digest** → Read the lesson transcript in `course_content/<Topic>/`, and discuss/explain the material with a problem-first approach, connecting it to concepts already covered
2. **Concepts** → Save full revision notes to `.github/my_tasks/concepts/concept_<lesson>.md`
3. **Tasks** → Create practice tasks (Problem Statements + Q&A + Self Assignments) to `.github/my_tasks/tasks/<lesson>_tasks.md`
4. **Quick Notes** → Append one-liner summary to `.github/my_notes.txt` under `Topic: <TopicName>`
5. **Links** → Append any reference/important links found in the lesson to `imp_links.md` (repo root), under the matching topic section

`course_content/` is source material (raw lesson transcripts) and is never edited by the agent.

---

## File Structure
```
.github/
    my_notes.txt                              # Quick revision - one-liners per lesson
    my_tasks/
        concepts/
            concept_what_is_internet.md       # Full revision notes: what is the Internet
        tasks/
            what_is_internet_tasks.md         # Practice tasks: what is the Internet
course_content/
    Introduction/
        what_is_internet.txt                  # Raw lesson transcript (source, not edited)
imp_links.md                                  # Running collection of important links, by topic
refresher.md                                  # Self-quiz memory + wrong-question bank
flexbox_master_notes.html                     # Print source for the flexbox hard copy (edit this)
flexbox_master_notes.pdf                      # Generated hard copy - regenerate with the command below
AGENTS.md                                     # This file - agent memory
CLAUDE.md                                     # Pointer to AGENTS.md, kept in sync
```

Regenerate the flexbox PDF after editing the HTML:

```bash
"/c/Program Files/Google/Chrome/Application/chrome.exe" --headless=new --disable-gpu --no-pdf-header-footer --print-to-pdf="C:/github_projects/fsd/flexbox_master_notes.pdf" "file:///C:/github_projects/fsd/flexbox_master_notes.html"
```

---

## Topics Completed

### Phase 1: Web Fundamentals
- [x] What is the Internet — client/server, ISP, DNS, IP addresses
- [x] How websites actually work — HTML/CSS/JS roles, browser render order, Chrome DevTools
- [ ] HTTP methods, status codes, headers
- [ ] Domain names, hosting, and web servers

### Phase 2: Frontend
- [x] HTML — core elements: headings, paragraphs, void elements (hr/br), lists, nesting/indentation, anchor tags & attributes, images (see EX 2.1–EX 3.4)
- [x] HTML — multi-page websites: file paths (absolute/relative, `./` & `../`), linking pages, HTML boilerplate, portfolio project, hosting on GitHub Pages (see EX 4.0–EX 4.3)
- [ ] HTML — semantic tags, forms, tables
- [x] CSS — adding CSS (inline/internal/external), selectors, combining selectors, cascade/specificity/inheritance, colors, fonts, box model, DevTools inspection, display, positioning; projects: Color Vocab, Flag of Laos, Motivational Poster (see EX 5.1–5.4, 8.0)
- [x] CSS — Flexbox basics: `display: flex` / `inline-flex`, `gap`, `flex-direction`, direct-child selectors for flex items (see EX 9.0, EX 9.1)
- [x] CSS — Flexbox layout: `order`, `flex-wrap`, `justify-content`, `align-items`, `align-self`, `align-content` (main vs cross axis); Flexbox Froggy game (see `flexlayout_transcript.txt`)
- [x] CSS — Flexbox sizing: priority ladder, `flex-basis` vs `width` vs `min`/`max-width`, the four grow/shrink scenarios, the `flex` shorthand & ratios (⚠️ weak area — see `concept_flex_sizing.md` + `flexbox_master_notes.pdf`)
- [x] CSS — **Flexbox section COMPLETE** — capstone `EX 9.4 Flexbox Pricing Table Project` built and corrected (centring recipe, `flex: 1` + `max-width` card pattern, media query `flex-direction: column`; see `concept_pricing_table_project.md`)
- [x] CSS — Grid basics: `display: grid`, `grid-template-columns`/`-rows`, the `fr` unit, `gap`, `repeat()`, 1D vs 2D vs Flexbox; `EX 10.0 Display Grid` chessboard **10/10** (see `concept_grid_display.md`)
- [x] CSS — Grid sizing concepts: fixed/`auto`/`fr`/`minmax()`/`repeat()`, implicit rows via `grid-auto-rows`/`-columns`, DevTools grid inspector (see `concept_grid_sizing.md`); `EX 10.1 Grid Sizing` hands-on practice still to attempt
- [x] CSS — Grid placement concepts: line numbers, negative lines, `span`, `grid-column`/`grid-row`, `grid-area`, overlap, visual `order`; **Grid Garden 28/28 complete** (see `concept_grid_placement.md`, `concept_grid_garden.md`); `EX 10.2` exercise 2 still needs Selva's one-line correction
- [x] CSS — Mondrian capstone concepts: measured fixed tracks, gap-as-black-lines trick, spans/areas, Flexbox centring (see `concept_mondrian_project.md`); local project still needs Selva to add body centring and change the last row from `20px` to `22px`
- [ ] CSS — responsive design
- [x] Bootstrap — 12-column layout system: `container`/`row`/`col`, the six container variants, the six `min-width` breakpoints, `col-N` sizing, stacking breakpoints mobile-first; **all 3 exercises at `appbrewery.github.io/bootstrap-layout` solved and verified 18/18** (see `concept_bootstrap_layout.md`)
- [ ] Bootstrap — lesson 64 "What is Bootstrap?" intro transcript is in the repo (`EX 11.0+Bootstrap+Intro/`) but **not yet digested**
- [x] Bootstrap — components, Examples & spacing utilities: the three toolboxes, the four "shops", the two CDN links (CSS = looks, JS = behaviour), the three kinds of copy-paste debt, `<img>` vs inline SVG, `{property}{sides}-{size}` spacing, `data-bs-theme="dark"`; **"Move It" site built, carousel challenge correct, audited and functional** (see `concept_bootstrap_components.md`)
- [ ] Bootstrap — TinDog project (`11.3+TinDog+Project/`) — the section capstone, still to build
- [ ] JavaScript fundamentals — variables, functions, DOM manipulation, events
- [ ] Frontend frameworks (e.g. React) basics

### Phase 3: Backend
- [ ] Node.js fundamentals
- [ ] Building APIs (e.g. Express) — routing, middleware, REST principles
- [ ] Authentication and authorization basics

### Phase 4: Databases
- [ ] Relational databases (SQL) — schema design, queries, joins
- [ ] Non-relational databases (NoSQL, e.g. MongoDB)
- [ ] ORMs and connecting a backend to a database

### Phase 5: Full Stack Integration & Deployment
- [ ] Connecting frontend to backend (fetch/AJAX, full CRUD app)
- [ ] Version control workflows (Git/GitHub) for full projects
- [ ] Testing a full stack app
- [ ] Deploying frontend + backend + database to the cloud

---

## Teaching Style Preferences
- Always start with **problem statement first** (why do we need this)
- Use **real-world web/automation context** where it helps (e.g. relate backend APIs to the API testing already known from Cypress/Selenium work)
- Keep examples practical and beginner-friendly — favor clear explanations over terse answers
- Prefer well-commented, beginner-friendly code over clever/compact code
- Connect new topics back to ones already covered in `course_content/`
- After explaining a lesson, proactively offer to create the concept file + task file + update quick notes
- Format tasks file with 3 sections: Problem Statements (With Input Data), Questions and Answers, Self Assignments (No Answers)
- Format concept file with numbered/headed sections matching `concept_what_is_internet.md` style

---

## Key Concepts Already Explained (with extra detail)
- **Client vs Server**: Server = always-on computer that stores/serves data on request; Client = the device (browser) making the request.
- **ISP (Internet Service Provider)**: the company (AT&T, Comcast, BT, TalkTalk, etc.) that connects you to the Internet and relays your requests.
- **DNS (Domain Name System)**: a "phone book" that translates human-readable domain names (`google.com`) into IP addresses.
- **IP address**: a unique numeric identifier ("postal code") for every device connected to the Internet.
- **Request flow**: Browser → ISP → DNS server (resolves IP) → Browser requests directly from that IP → server responds with page data.
- **Physical Internet**: undersea fiber-optic cables physically connect continents, carrying data via lasers at very high speeds (see submarinecablemap.com).
- **HTML/CSS/JS roles**: HTML = content (bricks), CSS = styling (paint), JavaScript = functionality (electricity/appliances) — house analogy.
- **Browser render order**: HTML loads first (raw content) → CSS applied (styled) → JavaScript runs (interactive).
- **Chrome DevTools**: Right-click → Inspect opens live HTML/CSS view; edits are local-only and reset on refresh since the browser re-fetches the real files from the server.
- **HTML tag vs. element**: tag = the `<bracketed>` piece; element = opening tag + content + closing tag together.
- **Heading hierarchy (h1–h6)**: only one `h1` per page, don't skip levels — convention, not enforced by the browser.
- **Void elements** (`<hr />`, `<br />`, `<img />`): self-closing, no separate closing tag; don't use `<br />` in place of a new `<p>` (breaks screen-reader paragraph navigation).
- **Lists**: `<ul>` = unordered (bullets), `<ol>` = ordered (numbers, has a `start` attribute); nested lists live inside a parent `<li>`, before that `<li>`'s closing tag.
- **Attributes**: live in the opening tag as `name="value"`; some are element-specific (`href` on `<a>`), some are global (`draggable` on anything).
- **Images**: `<img src="..." alt="...">` is a void element; `alt` text is read aloud by screen readers — always add it for meaningful images.
- **File paths**: unique location of a file/folder. **Absolute** = from the root (`C:\`/`Macintosh HD`); **Relative** = from the file you're editing (preferred in web dev — shorter, survives moving the project). `./` = current directory, `../` = up one level.
- **Multi-page sites**: multiple `.html` files linked via `<a href="./public/page.html">`; convention is `index.html` at top level, other pages in `public/`, assets in `assets/images/`. `href` is for `<a>`, `src` is for `<img>` — never swap them.
- **HTML boilerplate**: `<!DOCTYPE html>` (HTML5) → `<html lang>` (root) → `<head>` (invisible info: `meta charset`, `viewport`, `title`) + `<body>` (visible content). VS Code Emmet shortcut: `!` + Enter (in `.html` files only).
- **Web hosting / GitHub Pages**: hosting = files on an always-on web server (vs local development). Deploy: public repo + README → upload folder *contents* → Settings › Pages › Branch `main`. Home page must be named exactly `index.html`.
- **CSS basics**: Cascading Style Sheets = the styling layer. Rule = `selector { property: value; }`. Add via inline (`style=""`), internal (`<style>`), or external (`.css` + `<link>` — preferred for multi-page). Selectors: element, `.class` (reusable), `#id` (unique), `[attr]`, `*` — same syntax as Selenium/Cypress CSS locators.
- **CSS combinators**: `A, B` group · `A > B` direct child · `A B` descendant (any depth) · `AB` chain (no spaces, element first).
- **The cascade** (resolves conflicts): Position (lower wins) → Specificity (ID > attribute > class > element) → Type (external < internal < inline) → Importance (`!important` beats all). Some properties inherit (e.g. `font-family`).
- **Colors / fonts**: colours as named / hex / `rgb()`; `color` = text, `background-color` = background. Font sizes: `px`/`pt` static, `em` = parent-relative, `rem` = root-relative (preferred). `font-family` needs a generic backup; Google Fonts via `<link>`.
- **Box model** (inside→out): content → padding → border → margin. Border/padding grow the box *outward*. `<div>` = invisible grouping container.
- **Layout**: `display` = `block` / `inline` (can't size) / `inline-block` / `none`. `position` = `static` / `relative` (to itself) / `absolute` (to nearest positioned ancestor) / `fixed` (to window). Idiom: parent `relative` + child `absolute`. `border-radius: 50%` = circle. DevTools: Styles (struck-out = overridden), Computed (final values), CSS Overview (grab a site's colours/fonts).
- **Flexbox**: `display: flex` goes on the **container**, and its children's own default display values are ignored — it's a separate layout system from block/inline. Default = horizontal row, items sized to content. `gap` spaces items (`px` or `rem`). `flex` = full-width container (like `block`); `inline-flex` = shrink-to-fit container (like `inline-block`). `flex-direction: column` stacks vertically (`row` is default). Style flex items with `.container > *` (all direct children, tag-agnostic) rather than `.container div` (any depth). Replaces the legacy `<table>`/`inline-block`/`absolute`/`float` layout hacks — `float` should go back to its real job of wrapping text around images.
- **Flexbox layout**: `order` (child, default `0`, lower first, ties break by HTML order) reorders items visually only — doesn't touch the DOM. `flex-wrap`: `nowrap` (default, overflows) / `wrap` (new line) / `wrap-reverse`. `justify-content` spaces items along the **main** axis (`flex-start`/`flex-end`/`center`/`space-between`/`space-around`/`space-evenly`). `align-items` positions items along the **cross** axis (`flex-start`/`flex-end`/`center`/`baseline`/`stretch`, default `stretch`) — needs container height to actually be visible. `align-self` overrides `align-items` for one child. `align-content` spaces the gaps *between wrapped lines* — only works with `flex-wrap: wrap` and 2+ lines.
- **⚠️ WEAK AREA — Flex Sizing** (stress this in every revision/quiz; full notes in `.github/my_tasks/concepts/concept_flex_sizing.md`, tasks in `.github/my_tasks/tasks/flex_sizing_tasks.md`, hard copy in `flexbox_master_notes.pdf`):
  - **Priority ladder:** `content width < width < flex-basis < min-width/max-width` (rightmost strongest, clamping applied last). The lesson frames it as a **lookup** — walk down the list until you hit something that's set.
  - **"Content width" is a RANGE, not a number:** max-content (all text on one line) → min-content (the longest word). With no sizing props an item starts at max-content and shrinks to min-content, then **overflows off-screen** rather than shrinking further. Shrinking is **not uniform** — each item has its own longest word, so its own floor.
  - **`width` and `flex-basis` behave identically under pressure** — both are only a *preferred* size, abandoned when there's no room. Only the lookup order differs.
  - **The 3 questions** (instructor's debugging method, use before writing CSS): drag the window edge — *Does it grow?* → `flex-grow` · *Does it shrink?* → `flex-shrink` · *What size does it want to be?* → `flex-basis`.
  - **`flex-basis` vs `width`:** basis wins and `width` is ignored — but only on the **main axis** (row → basis = width; column → basis = height).
  - **`flex-basis` vs limits:** `flex-basis` = the *requested* size (the only property actually asking for one); `max-width` = potential to **extend** (ceiling); `min-width` = potential to **shrink** (floor). Limits are never targets. One rule: basis inside the allowed range → basis wins; basis outside → the broken limit wins. S1 `basis 200` + `max 100` → **100** · S2 `basis 50` + `max 200` → **50** · S3 `basis 200` + `min 300` → **300** · S4 `basis 400` + `min 300` → **400**. Vs `max-width` the smaller wins, vs `min-width` the larger wins. Traps: `max-width` also caps `flex-grow`; `min-width` beats `max-width`; always name the limit ("ceiling or floor?") first.
  - **Four grow/shrink scenarios** (all `basis: 100px`): `0 0` rigid · `1 0` basis is the **floor** · `0 1` basis is the **ceiling** ← *the default* (`flex: 0 1 auto` = shrink yes, grow no) · `1 1` fully fluid, basis is only the **starting line** (not "ignored" — it's what free space is measured against).
  - **`basis: auto` vs `0`:** `auto` = content priority (share the leftovers) · `0` = equal widths (share everything).
  - **Shorthand:** `flex: <grow> <shrink> <basis>`. `flex: 1` = `1 1 0%` · **`flex: 2` = `2 1 0%`, NOT `2 2 0`** (one number sets grow only — ⚠️ the *video itself* says "a grow of 2 and a shrink of 2"; that is a slip in the lesson, verified against Chrome) · `flex: auto` = `1 1 auto` · `flex: none` = `0 0 auto` · `flex: initial` = `0 1 auto`. The shorthand resets basis to `0`; the longhand `flex-grow: 1` leaves it at `auto` — that's why they give different widths.
  - **Ratios:** grow/shrink are ratios, not pixels. `flex: 1 / 2 / 3` in 600px → **100 / 200 / 300**, and they grow & shrink together keeping 1:2:3.
  - **Algorithm:** lay down basis → free space = container − Σbasis − gaps → share by grow ratio (or claw back by **shrink × basis**) → clamp → `justify-content` positions the rest. Shrink is weighted by basis; grow isn't.
  - **#1 real bug:** flex items carry a hidden `min-width: auto` (= min-content), so they refuse to shrink past their longest word/image. Fix: `min-width: 0` (or `overflow: hidden`). Behind most "ellipsis doesn't work" issues.
- **Flexbox capstone — EX 9.4 Pricing Table** (built & corrected 2026-08-23; full notes in `.github/my_tasks/concepts/concept_pricing_table_project.md`): the whole project is 4 ideas — the centring recipe (`justify-content: center` + `align-items: center` + a container height), the **`flex: 1` + `max-width: 400px`** card pattern (fluid but capped), resetting the `<ul>`, and one media query flipping `flex-direction: column`.
  - **⚠️ `height: 100vh` must become `height: 100%` (or `min-height: 100vh`) once content stacks.** Measured at 760×900: `100vh` locked the container to 804px while the stacked cards needed 895px → first card's top edge at **−82px**, *above* the page. `justify-content: center` splits overflow **both ways** and the top half is **unreachable by scrolling** — strictly worse than a normal overflow. The lesson demos this deliberately.
  - **⚠️ `padding: 0` on the `<li>` does nothing.** The list indent is the **`<ul>`'s** default `padding-left: 40px`. Verified: `li{padding:0}` → still 40px; `.plan-features{padding:0}` → 0px. With `text-align: center` that pushed the whole list 20px right. Check DevTools → Computed to find which element owns a default.
  - **Axis discipline for units:** `max-width: 50vh` (a *width* capped by screen *height*) was a real submission — valid CSS, wrong axis, no warning. `vh` for height, `px`/`%`/`vw` for width. `rem` for spacing/`gap` so it scales with zoom.
  - Selector hygiene: use the classes the HTML already provides (`.plan-features`, `.plan-button`), not bare `li` / `button`. Media-query hygiene: override only what changes.
  - **Selva's own error pattern here:** layout thinking was right every time; the misses were *which element owns a property* and *which axis a unit belongs to*. Worth probing on future projects.
- **CSS Grid — `display: grid`** (lesson done 2026-08-27; full notes in `.github/my_tasks/concepts/concept_grid_display.md`, tasks in `.github/my_tasks/tasks/grid_display_tasks.md`):
  - **Flexbox = 1D (a row *or* a column). Grid = 2D (rows *and* columns together).** If the design has an X and a Y, use Grid. **Not** either/or — real sites nest them (the lesson's Swiss weather site is a grid with a `flex-direction: column` flexbox inside one panel).
  - **On resize:** Grid snaps items to shared row/column lines so every gap stays dead straight; Flexbox squishes/adapts, so items line up only by accident. Demo: <https://appbrewery.github.io/grid-vs-flexbox/>.
  - `display: grid` goes on the **container** (same muscle memory as `display: flex`). Container props: `grid-template-columns`, `grid-template-rows`, `gap` (the same `gap` from Flexbox; spaces both axes). One value per track, space-separated.
  - **`fr` = a fraction of the *available* space — a ratio, not a size.** Essentially `flex-grow` with its own unit (`1fr 2fr 3fr` ≡ `flex: 1 / 2 / 3`).
  - **⚠️ TRAP (Selva's actual bug this lesson): `1fr` of nothing is nothing.** `grid-template-rows: 1fr×8` with no container `height` → `0px` rows → **completely blank page** despite 64 coloured divs. Cause: a grid container's defaults are **asymmetric** — *full width* (block-level, so `1fr` columns get real space) but *content height* (empty divs = 0 content = 0 space to divide). Same family as `align-items` needing a container height. **Check the container's height before blaming the grid.**
  - **Grid infers:** declare only 8 columns, drop in 64 divs → you already get the chessboard (rows auto-created). Declaring rows anyway is clearer.
  - `repeat(n, size)` replaces repeated track values. **Grid items stretch to fill their cell on *both* axes** by default (`align-items: stretch` applied twice) — that's why empty unstyled divs work.
  - **EX 10.0 Chessboard — graded 10/10.** Two valid, pixel-identical solutions in opposite directions: **(a) size the children** (official: container `width: 800px` only, `.white/.black { width/height: 100px }` — rows size to content) vs **(b) size the container** (Selva's: `width: 800px; height: 800px`, children get only colours — items stretch). (b) is more idiomatic grid: let the *grid* dictate sizes to children; also resizes the whole board from one line.
  - `width: 800px` on the container matters because otherwise it fills the window, `1fr` cells get wider than the 100px squares, and "mystery gaps" appear between them — the squares are 100px but their *cells* aren't.
  - Selva-speak: *"Flexbox = one line, Grid = a table"* · *"fr is flex-grow with a unit"* · *"fr of nothing is nothing"* · *"Grid container is greedy sideways, shy downwards"* · *"You don't size chess squares, you size the board."*
  - **Encouraging pattern:** unlike EX 9.4, this time the miss was *not* which element owns a property — it was a missing container size, diagnosed and fixed in one step.
- **CSS Grid — Sizing tracks** (lesson done 2026-08-27; full notes in `.github/my_tasks/concepts/concept_grid_sizing.md`, tasks in `.github/my_tasks/tasks/grid_sizing_tasks.md`):
  - Fixed `px`/`rem` tracks are **never responsive** to window resize — `rem` only reacts to root font-size (zoom/`html{font-size}`), not to screen width. `grid-template: rows / columns` is valid shorthand, deliberately avoided while learning so rows/columns stay explicit and easy to debug.
  - **⚠️ TRAP — `auto` behaves differently per axis, same family as `EX 10.0`'s blank-page trap:** `auto` on a **column** stretches/shrinks so columns always total 100% of width; `auto` on a **row** does NOT fill height — it only fits its own content. Width-greedy, height-shy — the same asymmetry as a grid container's own defaults, just behind an explicit keyword this time.
  - **`fr` is a live ratio, not a locked-in size:** growing the content in ONE `fr` row can grow a *sibling* `fr` row too (its own content unchanged) purely to preserve the ratio — verified in the transcript's own demo (adding text to row 2 grows row 1).
  - **`minmax(min, max)`** = Flexbox's `min-width` + `max-width` (Selva's ⚠️ weak area) merged into a single grid-track function — grows to the ceiling, shrinks to the floor, never crosses either line.
  - **`repeat(count, value)`** works for any track size, not just `fr` (e.g. `repeat(2, 200px)`).
  - **Item-count mismatches:** too few items → leftover cells stay empty, no phantom boxes. Too many items → Grid adds an implicit row sized by *existing column width* (for width) + *the new item's own content* (for height), unless `grid-auto-rows`/`grid-auto-columns` overrides the height.
  - Chrome DevTools: the "grid" badge + Layout pane's **Show track sizes** reads out every track's exact computed pixel size — no manual math needed.
  - `EX 10.1 Grid Sizing` ("Test" page, `course_content/GRID/EX 10.1 Grid Sizing/test.html`) spec captured but **not yet attempted**: rows `1fr 1fr 2fr` + `grid-auto-rows: 50px` for an out-of-template 4th row; columns `auto 400px minmax(200px, 500px)`. Next step: write it myself in `test.html` before checking the concept notes' worked solution.
- **CSS Grid — Placement + Grid Garden** (reviewed 2026-08-29; full notes in `concept_grid_placement.md` and `concept_grid_garden.md`; tasks in matching task files):
  - **The template draws the map; placement gives items addresses.** A grid with `n` tracks has `n + 1` lines. Count grid lines, not boxes.
  - Parent properties create the map (`display`, templates, auto tracks, `gap`); item properties choose the address (`grid-column`, `grid-row`, `grid-area`, `order`).
  - **Line numbers answer where; `span` answers how many.** `2 / 5` names two destination lines; `2 / span 3` names one line plus a track count.
  - Negative lines count from the far edge (`-1` = final line). Start/end may run in either numeric direction; Grid selects the area between them.
  - **`grid-area` order:** row-start / column-start / row-end / column-end. Selva mnemonic: *"row, column, row, column — walk around the rectangle."*
  - `order` changes the visual auto-placement queue only. It does not change item size, explicit line address, DOM/reading order, or keyboard focus order.
  - Explicit areas can overlap; painting/source order and `z-index` control the top layer.
  - **Grid Garden completed 28/28 on 2026-08-29**, with the final "You win!" screen verified. Levels 1-17 cover placement, 18-19 `order`, 20-28 track sizing and `grid-template`.
  - `grid-template` is **rows / columns**, not the four-value `grid-area` order. Final verified level: `grid-template: 1fr 50px / 20% 1fr`.
  - Fixed tracks and gaps resolve first; `fr` shares the remainder. Example: `75px 3fr 2fr` reserves 75px, then divides remaining width into five shares.
  - **EX 10.2 audit (source preserved):** exercise 1 correct; exercise 2 incomplete because `order: 1` changes sequence but not width — add `grid-column: span 2`; exercise 3 correct with `grid-row: span 2`.
- **CSS Grid — Mondrian capstone** (reviewed 2026-08-29; full notes in `concept_mondrian_project.md`, tasks in `mondrian_project_tasks.md`):
  - Design-to-grid workflow: draw every boundary → count tracks → write sizes/gaps → add one div per region → merge with spans/areas → colours → DevTools → centre last.
  - Reference frame is `748px × 748px`: columns `320 198 153 50`, rows `414 130 155 22`, `gap: 9px`. Track sums plus three gaps must equal the frame.
  - Grid lines cannot be coloured. The project uses a black grid-container background and transparent `gap` so black seams show between coloured items.
  - Major merges: `white1` column span 3; `white2` row span 2; `white3` area `2 / 2 / 4 / 4`; `white4` row span 2.
  - Normal black seams belong to the container gap; the extra `10px` line below the blue block belongs to the blue item's `border-bottom`.
  - **Grid makes the painting; Flexbox hangs it on the wall.** Body Flexbox centring is the outer layout layer; prefer `min-height: 100vh` for safe growth.
  - Local attempt is close but not final: missing body centring and last row uses `20px` instead of the exact-fit `22px`. Keep the capstone hands-on incomplete until Selva fixes these himself.
  - Master hard copy generated from `grid_master_notes.html` as `grid_master_notes.pdf`; includes the full 28-level solution ladder and honest remaining-practice checklist.
- **Bootstrap — 11.0 The 12-Column Layout System** (lesson done 2026-08-30; full notes in `concept_bootstrap_layout.md`, tasks in `bootstrap_layout_tasks.md`):
  - **Bootstrap's grid is NOT CSS Grid — it is Flexbox with the CSS pre-written.** Verified in `bootstrap@5.3.0-alpha2`: `.row{display:flex;flex-wrap:wrap}` · `.row>*{flex-shrink:0;width:100%;max-width:100%}` · `.col{flex:1 0 0%}` · `.col-6{flex:0 0 auto;width:50%}` · `.col-auto{flex:0 0 auto;width:auto}`. Three consequences: a class-less div in a row is **already 12/12** (it's just `width:100%`); columns **wrap rather than squash** (`flex-shrink:0`, so numbers over 12 drop to a new line); `.col` = `flex:1 0 0%` is literally Selva's flex-sizing "basis 0 = equal widths, share everything" case. Gutters are a negative-margin trick — don't put your own `margin` on a `col`, use `g-*`.
  - Skeleton is always **container → row → col**, never skip a level; content goes inside the `col`.
  - **Container ladder** (real values, not the transcript's approximations): caps of 540/720/960/1140/1320px at sm/md/lg/xl/xxl. **`container-{bp}` = "100% wide UNTIL `{bp}`, then a normal container" — the name is the size at which it STOPS being full-width.** `container-sm` is identical to `container`; `container-fluid` never joins the max-width list so it's always 100%. Answers Selva's own "explore!!!" note in the transcript.
  - **Breakpoints:** *(none)* `<576` · `sm ≥576` · `md ≥768` · `lg ≥992` · `xl ≥1200` · `xxl ≥1400`. **⚠️ All are `min-width` — "this width AND WIDER", never "up to".** Verified at the edge on the exercise page: 575px = xs, 576px = sm, so the boundary is **inclusive**. Extra small has no infix because there's no `min-width` to name — which is what makes the trap below possible.
  - **Stacking classes wins by SOURCE ORDER, not specificity.** `.col-sm-12` and `.col-lg-4` are both `(0,1,0)` — a perfect tie; Bootstrap orders its media queries smallest-first so the larger class is physically later. Verified rule indices: `.col-10` #130, `.col-sm-12` #176, `.col-lg-6` #260. This is cascade rule 1 ("position, lower wins") from `concept_css.md` — Bootstrap invented nothing, it just ordered the file mobile-first.
  - **⚠️ TRAP — THE VIDEO IS WRONG HERE (this lesson's headline finding).** In Exercise 2 the instructor says Column 1 is full width at `sm` "by default" and adds no class. True in Ex 1, **false in Ex 2**, because `col-10` was added for xs and a no-infix `col-N` **has no upper bound**. Measured at 700px: `col-10 col-lg-6` → **10/12 (wrong)**; `col-10 col-sm-12 col-lg-6` → **12/12 (right)**. Columns 2 & 3 escape only by accident (their `col-sm-6` overrides it). The exercise page's own answer markup carries `col-sm-12`, confirming it's required. **Generalised: there is no "unset" in Bootstrap's grid, only "override" — every `col-*` is a floor that persists upward until overwritten. When one screen size is wrong, ask "which class is still IN FORCE here?", not "which class did I write for here?"** Same family as Selva's EX 9.4 / EX 10.0 misses: layout reasoning right, *which rule owns the value* wrong.
  - **All 3 exercises solved and verified 18/18** (3 exercises × 6 viewport bands, my box widths vs the demo's, matching within 1px). Ex1 `col-xl-6` ×2 · Ex2 `col-10 col-sm-12 col-lg-6` / `col-10 col-sm-6 col-lg-3` ×2 · Ex3 `col-md-6 col-lg-4 col-xl-2 col-xxl-1` / `col-md-6 col-lg-8 col-xl-10 col-xxl-11`.
  - **Method that beat eyeballing:** measure box width ÷ row width × 12 → exact twelfths. Six readings (450/650/850/1100/1300/1500) capture the whole spec, and the resulting table *is* the solution — read each column downward. Instructor's own tip is the manual version: DevTools → device toolbar → Responsive → drag and watch the width readout.
  - Media queries aren't retired — Bootstrap pre-writes *layout* responsiveness only. Custom font scaling, background images, off-scale spacing, or a non-standard breakpoint still need your own `@media`.
  - Selva-speak: *"Container wraps rows, rows wrap columns, columns wrap content."* · *"Bootstrap's grid is Flexbox with the homework done."* · *"`container-{bp}` = the size at which it STOPS being full width."* · *"Breakpoints go up, never down."* · *"A no-infix `col-10` isn't 'mobile only', it's 'everywhere until overridden'."* · *"There is no unset, only override."*
- **Bootstrap — 11.2 Components, Examples & Spacing Utilities** (lesson done 2026-09-03; full notes in `concept_bootstrap_components.md`, tasks in `bootstrap_components_tasks.md`):
  - **Three toolboxes:** Layout (where boxes go — 11.0) · Components (pre-built *things*: `btn`, `card`, `navbar`, `carousel`) · Utilities/Helpers (one-property tweaks: `mt-3`, `d-flex`, `shadow-lg`). **A component is a noun, a utility is an adjective**; real markup is one component class plus a handful of utilities. Not a coding lesson so much as a *shopping* lesson.
  - **Two classes, two jobs:** `btn` = shape (padding/font/radius/hover/focus), `btn-success` = colour. Colour names are **semantic roles, not colours** (`primary` blue `#0d6efd` = main action · `success` green `#198754` · `danger` · `warning` · `info` · `light`/`dark`). That indirection is exactly what makes dark mode free — a class called `btn-green` couldn't follow you into a dark theme.
  - **Four shops the video never distinguishes:** Docs→Components (one thing) · **Examples** `/docs/5.3/examples/` (whole page sections, already laid out — the one beginners never find, and the better shop) · Icons `icons.getbootstrap.com` (~2000 free royalty-free SVGs) · Themes (paid whole sites). Move It's navbar/hero/features/footer all came from **Examples**.
  - **Extraction workflow** (done four times on camera, never named): Inspect → **hover *upward* through the DOM watching the blue highlight** until it covers exactly the region you want → Copy → Copy element → paste → replace `src`/`alt`/text. Step 3 is the skill: too shallow = a fragment, too deep = the example page's own layout wrapper. Same *"which element owns this?"* question as EX 9.4's `ul`-vs-`li` padding and 11.0's leaking `col-10`, aimed at copying instead of styling.
  - **⚠️ TWO CDN LINKS — CSS gives looks, JS gives behaviour.** The lesson's best debugging moment: the navbar looks perfect and the hamburger does nothing, because the starter only had the stylesheet. **Rule: looks right but doesn't move → you forgot the script tag** (nothing errors, nothing logs). Needs JS: navbar collapse, dropdowns, **carousel**, modal, tooltip, accordion, offcanvas. Fine without: colours, the grid, cards, spacing, typography, shadows. `bundle` = Popper.js included (plain `bootstrap.min.js` → collapse works, dropdowns don't). Goes before `</body>`. `data-bs-*` attributes are how pasted HTML talks to that JS — delete one while "tidying up" and the component silently goes quiet. **Keep CSS and JS on the same version** (starter: alpha2 CSS + alpha3 JS; the build: alpha2 CSS + 5.3.8 JS — both work, but mismatch is a real bug source).
  - **⚠️ The carousel challenge is a LAYOUT question in disguise.** Pasted carousel is full-bleed and taller than the screen; the fix is `<div class="container">` from lesson 11.0, not a carousel property. Slides are `d-block w-100`, so they take the container's capped width and the height follows from aspect ratio. **Generalised: sizing a component is its parent's job** — Bootstrap components are `width: 100%` by design so the container decides. Same idea as *"you don't size the chess squares, you size the board."*
  - **⚠️ Copy-paste leaves three kinds of debt — you get the HTML only:** (1) **custom CSS that was never Bootstrap's** — `.feature-icon{width:4rem;height:4rem;border-radius:.75rem}` (verified absent from `bootstrap@5.3.0-alpha2`) is the one hand-written rule; the six classes beside it are real Bootstrap. Diagnose by **reading the source-file column in DevTools' Styles pane, not the class names**. (2) **sprite icons don't travel** — `<use xlink:href="#briefcase">` points at a `<symbol>` on *that* page, so in your file it renders as an empty box of the right size, silently. (3) **placeholder content** — `src`, body copy, and especially **`alt`**, which survives because it is the one thing never visible on screen.
  - **⚠️ `<img>` SVG vs inline `<svg>` — the bit the video hand-waves as "up to you".** An `<img>`-loaded SVG is a **separate, isolated document; your CSS cannot reach inside it.** Two measured consequences: Bootstrap's `.icon-link > .bi{width:1em;height:1em}` can't apply, so the chevrons render at their intrinsic **16×16** — *that is why the video hand-writes `height="30"` on every single icon*; and you can't recolour it, because `fill="currentColor"` resolves in the SVG's own document. Inline `<svg>` **does** inherit `currentColor` — the whole reason Bootstrap Icons ship with it. The one thing that crosses the boundary is the light/dark **colour scheme**, so the same unchanged `<img src="./box-seam.svg">` renders black in light mode and **white in dark mode** (verified). Choose inline `<svg>` whenever the icon must change colour with context, size from CSS, or animate.
  - **Spacing formula:** `{property}{sides}-{size}`, breakpoint infix optional → `{property}{sides}-{breakpoint}-{size}`. Sides: *(none)* all · `t` top · `b` bottom · `s`/`e` **start/end** (= left/right in LTR — logical properties, so layouts mirror in RTL; Bootstrap 4 used `l`/`r`) · **`x` = left+right** · **`y` = top+bottom**. Scale: `0 · .25 · .5 · 1 · 1.5 · 3` rem — **5 is the maximum that *exists*, not a guideline; `mt-6` silently does nothing.**
  - **🚨 THE VIDEO SAYS x AND y BACKWARDS — this lesson's headline finding.** Transcript: *"for both the top and the bottom, you'll use the x-axis … for the left and the right … the y-axis."* Exactly inverted; verified in the stylesheet (`.mx-3` sets left/right, `.my-3` sets top/bottom). It slips past because he gets it *right* one sentence later (*"my-3 … the y-axis"*), and every class name in the code is correct. Hook: **x runs across, y runs up and down** — same as `column-gap`/`row-gap` and `translateX`/`translateY`. **Third video error caught in this course** (after `flex: 2` = "grow 2 shrink 2", and the `col-sm-12` omission in 11.0). **Pattern: the class names and the code are reliable; the spoken explanations are not — check the stylesheet.**
  - Other verified spacing facts: **every utility carries `!important`** (cascade rule 4, used deliberately so utilities are the last word — it's why your own class loses to `mb-2`) · `mx-auto` is the centre-a-block trick, **`p-auto` doesn't exist** · **`pe-` is overloaded**: `pe-0`…`pe-5` are `padding-right` but `pe-none`/`pe-auto` are **`pointer-events`** · negative margins (`m-n1`) are **not in the stock build** (opt-in Sass flag) · **the 11.0 breakpoint ladder works on utilities too** (`mb-2 mb-lg-0`, `me-sm-3`), carrying *"there is no unset, only override"* with it · `me-auto` on the navbar is the `margin-left:auto` shove-to-the-far-end trick from flex sizing.
  - **Dark mode = one attribute:** `<html data-bs-theme="dark">`. Measured: body bg `#fff → #212529`, body text `#212529 → #adb5bd`, navbar `#f8f9fa → #2b3035`. Works because 5.3 defines everything through CSS custom properties and reassigns them in a `[data-bs-theme=dark]` block — **and because the markup asked for roles, not colours.** Works on any element, not just `<html>`.
  - **Build audited ✅** — all 5 sections present and functional (CSS+JS load · hamburger opens below 992px · dropdown opens · **carousel challenge correct** · all 11 images resolve · `.feature-icon` custom CSS copied · all text replaced). **3 things Selva should still fix himself** (all the same "invisible leftovers" family, none break the page): `alt="Example image"` on the hero image (`index.html:69`, the course solution has the same bug) · the footer's ghost `<use xlink:href="#bootstrap">` sprite pointer rendering as a 40×32 gap (`index.html:152`) · CSS `5.3.0-alpha2` vs JS `5.3.8` version mismatch.
  - Selva-speak: *"Layout puts the boxes down; Components fill them; Utilities nudge them."* · *"A component is a noun, a utility is an adjective."* · *"Looks right but doesn't move? You forgot the script tag."* · *"Copy-paste gets you the HTML, never the CSS."* · *"Read the source-file column, not the class names."* · *"Sizing a component is its parent's job."* · *"An `<img>` SVG is a locked room — your CSS has no key."* · *"x runs across, y runs up and down — the video says it backwards."* · *"5 is not a guideline, 5 is the ceiling."* · *"Ask for the role, not the colour — that's what makes dark mode free."*
