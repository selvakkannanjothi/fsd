# How Do Websites Actually Work?

## The problem this solves

From the last lesson, you know your browser can find a server's IP address (via DNS) and send it a request directly. But once that request lands — **what does the server actually send back?** A website needs to show *content*, look a certain *way*, and let you *do* things. That's too many jobs for one file, so the answer is three separate file types, each responsible for exactly one job.

## The house analogy

| File type | House equivalent | Job |
|---|---|---|
| **HTML** | The bricks / raw materials | Content — text, images, buttons, links |
| **CSS** | Paint, wall color, door shape | Styling — how everything looks |
| **JavaScript** | Light bulbs, a working cooker | Functionality — things the user can *do* |

## The three files, in detail

### HTML — the content
Contains the actual "stuff" on the page: headings, paragraphs, images, buttons, links. If a website was a house, HTML is the physical structure — remove it and there's nothing left to look at or style.

### CSS — the styling
Targets the HTML elements and decides how they look: background color, rounded corners, fonts, spacing. CSS never adds or removes content — it only restyles what HTML already put there.

### JavaScript — the functionality
Turns a static page (pretty but inert) into something interactive: submitting a form, sending an email in Gmail, posting a photo on Instagram. Without JS, a page can be looked at but not really used.

## How the browser assembles them

1. Browser requests a page (after DNS resolves the IP, per the previous lesson).
2. Server sends back HTML, CSS, and JavaScript files.
3. Browser loads **HTML** first → you see raw content (e.g. Google's logo image, two buttons, a search box).
4. Browser applies **CSS** → same content, now styled to look the way the site intends (button shape, colors, layout) — no new elements appear, existing ones just look different.
5. Browser runs **JavaScript** → the page becomes interactive (e.g. typing a search term and getting results).

```
Server sends: HTML + CSS + JS
      │
      ▼
Browser renders HTML  →  raw content only
      │
      ▼
Browser applies CSS   →  content now styled
      │
      ▼
Browser runs JS       →  page becomes interactive
```

## Seeing this live: Chrome DevTools

- Right-click any element on a page → **Inspect** → opens **Chrome DevTools**, highlighting the exact HTML responsible for that element.
- You can double-click a value (e.g. a button's text, or its `aria-label`) and edit it directly in DevTools.
  - Note: `aria-label` is metadata for screen readers (accessibility), not something you'll see rendered on screen — different from the visible text.
- This only changes **your local, in-browser copy** of the page. Hitting refresh re-requests the HTML/CSS/JS from the server, so the original content comes right back.
- This is a good way to *prove to yourself* that a "website" isn't a fixed thing living on the server screen — it's a set of files your browser downloads and renders every time, and you can temporarily reshape that render however you like.

## Key terms glossary

- **HTML (HyperText Markup Language)**: defines the content/structure of a webpage.
- **CSS (Cascading Style Sheets)**: defines the visual styling of HTML content.
- **JavaScript**: adds interactivity/functionality to a webpage.
- **Chrome DevTools**: browser built-in tool suite for inspecting/editing a page's HTML, CSS, and JS live (locally only).

## Why this matters going forward

Every website you'll ever build is just these three file types working together. The rest of this course is essentially: learn HTML properly, then CSS, then JavaScript — in that order, matching the order the browser itself processes them.
