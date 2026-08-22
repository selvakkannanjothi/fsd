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
AGENTS.md                                     # This file - agent memory
CLAUDE.md                                     # Pointer to AGENTS.md, kept in sync
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
- [ ] CSS — Flexbox sizing (`flex-grow`/`flex-shrink`/`flex-basis`), Grid, responsive design
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
