# Multi-Page Websites — File Paths, Web Pages, Boilerplate, Portfolio & Hosting

Source transcripts: `course_content/Multi Page websites/file_path_transcripts.txt`,
`web_page_transcript.txt`, `html_boilerplate.txt`, `portfolio_project_transcripts.txt`,
`host_your_site_free.txt`
Practice exercises: `EX 4.0 File Paths` → `EX 4.3 HTML Portfolio Project`

## The problem this solves

So far every site has been a single `index.html`. Real websites have **many pages** (Home, About,
Contact) and pull in **many resources** (images, other HTML files). To connect all of that you need one
foundational skill — **file paths** — plus a **standard page skeleton** (the boilerplate) and finally a
way to get the finished site **off your laptop and onto the public Internet** (hosting). This block ties
the whole HTML unit together into a real, shareable, multi-page portfolio.

---

## 1. File paths — the core skill (`EX 4.0`)

A **file path** is a unique location for a file or folder on a computer — the same idea as directions to
a place in the world (Country → City → Street → Café). The starting point of the whole filing system is
the **root**, i.e. your hard drive (`C:` on Windows, `Macintosh HD` on Mac).

There are **two kinds** of path:

### Absolute path — relative to the *root*
Always starts from the hard drive and traverses down. Works no matter where you currently are in the file
system.
- Windows: `C:\Project\Images\cat.png`
- Mac: `/Users/you/Project/Images/cat.png`

### Relative path — relative to the *file you're writing code in*
Starts from the current file's location. **This is what we use in web development**, because:
1. It's usually shorter.
2. It stays valid even if you move the whole project folder somewhere else (the internal journey doesn't
   change).

### The special characters (memorize these)

| Symbol | Meaning | Example |
|---|---|---|
| `./` | **current directory** — the folder this file lives in | `./cat.png` |
| `../` | **go up one level** to the parent folder | `../essay.docx` |
| `../../` | go up two levels (chain as many as needed) | `../../dog.png` |
| *(nothing)* | also means current directory | `cat.png` |

- You *can* omit `./` for something in the same folder (`dog.png`), but it doesn't always work — so the
  lesson recommends **always writing `./`** for the current directory. Works 100% of the time.
- **Debugging trick from the exercise**: use VS Code's **autosuggest dropdown** while typing a path. If
  the suggestions don't show the folder you expect (e.g. you typed `..` but wanted `.`), that's an early
  warning your path is wrong — fix the special character before continuing. Also fewer typos than typing
  the whole path by hand.
- **How to find where a file actually lives** in VS Code: collapse folders one by one. When a file
  disappears on collapsing a folder, that folder is its parent.
- A **broken image** in the preview = a wrong file path. That's your signal to rethink the path.

> Worked example from `EX 4.0` (writing code inside `Folder0/index.html`):
> - `./rabbit.png` — rabbit is in the same folder
> - `./Folder3/cat.png` — down into a subfolder
> - `../dog.png` — up one level to the grandparent folder
> - `../Folder1/fish.png` — up one, then into a sibling folder
> - `../Folder1/Folder2/bird.png` — up one, then two levels down

---

## 2. Web pages & multi-page sites (`EX 4.1`)

A multi-page site is just **several `.html` files in the same project**, linked together with anchor tags
(`<a>`) whose `href` is a **relative file path to another HTML file** (not just to a website on the
Internet).

```html
<!-- inside index.html, linking to the About page -->
<a href="./public/about.html">About</a>
```

- Clicking the link **navigates the browser to that HTML file** (redirects to `about.html`).
- **Convention for organizing pages**: keep `index.html` (the home page) at the top level, and put
  **every other page inside a `public/` folder**. Images/assets go in `assets/images/`.
- **An image can itself be a link** — nest the `<img>` *inside* the `<a>` instead of link text:
  ```html
  <a href="./public/about.html">
    <img src="./assets/images/cat.png" alt="Me" />
  </a>
  ```
- **Common quiz mistakes** to avoid (all from the lesson's QR quiz):
  - Using `../` when the target is in the *current* directory (that jumps too far up).
  - Using `href` on an `<img>` — images use **`src`**, `href` is **only** for `<a>`.
  - Using an `<a>` when you actually want to *display* an image (an anchor links, it doesn't show a
    picture).

---

## 3. The HTML boilerplate — standard page skeleton (`html_boilerplate.txt`)

Every HTML file starts from the same skeleton, just like a formal letter has a fixed structure. Food
analogy from the lesson: the whole thing is a **hamburger** — `<html>` is the bun, and everything is
sandwiched inside.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Website</title>
  </head>
  <body>
    <!-- all visible content goes here -->
  </body>
</html>
```

Line by line:
- **`<!DOCTYPE html>`** — declaration (not a normal element) telling the browser the file is **HTML5**
  (the latest version).
- **`<html lang="en">`** — the **root** element; everything else nests inside it. `lang` tells screen
  readers which language to pronounce — matters for accessibility, invisible to sighted users.
- **`<head>`** — info *about* the page that is **not displayed** to the user:
  - `<meta charset="UTF-8">` — character encoding, so emojis/symbols render correctly. Include as-is by
    convention.
  - `<title>` — text shown in the **browser tab** (and used by search engines / bookmarks).
- **`<body>`** — **all visible content**: headings, paragraphs, images, links, etc. This is where you
  spend most of your time.
- **`viewport` meta** — tells the browser how to size the page relative to the screen (essential for
  mobile). Keep it.
- **`X-UA-Compatible` meta** — legacy Internet Explorer compatibility. IE is deprecated, so this line can
  be **deleted** to keep code clean.

Key ideas reinforced here:
- **Nesting** — `<head>` and `<body>` sit inside `<html>`; indent each level by 2 spaces so the
  opening/closing tags visibly line up (purely for humans — no effect on rendering).
- **VS Code shortcut**: in a file saved with a **`.html`** extension, type `!` then **Enter** (Emmet) to
  auto-generate the entire boilerplate. Won't work on non-`.html` files.

---

## 4. Portfolio project — putting it together (`EX 4.3`)

The capstone: a simple **HTML-only web-developer portfolio** that shows off the earlier Movie Ranking
(Section 2) and Birthday Invite (Section 3) projects, plus About Me / Contact Me pages. Real developers
split a big task into small steps — here, a **7-step to-do list**:

1. Create the HTML **boilerplate** (from lesson 3).
2. Change the `<title>`.
3. Move your previous projects' HTML into the **`public/`** folder (use *your* customized code).
4. **Screenshot** each project, drop into `assets/images/`, rename sensibly (fallback images are provided).
5. Add **titles/subtitles** (`h1`/`h2`), `<hr />` separators.
6. Add **anchor links** to each project page (`./public/movie-ranking.html`, etc.).
7. Add **preview images** for each project, then About Me / Contact Me links at the bottom.

- **Sizing hint**: raw screenshots are huge. Set `height="200"` on the `<img>` (200px tall) and the
  browser auto-computes the width to keep proportions. (Look up the attribute on MDN.)
- This is intentionally unstyled — **CSS comes next** and will make it beautiful without changing this
  structure.

---

## 5. Web hosting — going live with GitHub Pages (`host_your_site_free.txt`)

**Web hosting** = putting all your site's files onto a **web server** (a computer permanently connected to
the Internet) so anyone, anywhere, can access it 24/7. Until now the site only runs in **local
development** (files live only on your machine). Hosting = copying those files to an always-on server.

Free hosting via **GitHub Pages**:
1. Sign up / sign in at **github.com**.
2. Create a **new repository**, name it e.g. `html-portfolio`.
3. Make it **Public** (required for free Pages hosting) and tick **Add a README file**.
4. **Add file → Upload files** → drag in the **contents** of your project folder (⚠️ *not* the folder
   itself — its contents), then **Commit changes**.
5. Verify all files/folders (especially `index.html`, `assets/`, `public/`) uploaded correctly.
6. **Settings → Pages → Branch**: change from `none` to **`main`**, **Save**.
7. Refresh a few times (can take **1–10 min**); a box appears with your **live URL** → **Visit site**.

Critical gotchas:
- The home page **must** be named **`index.html`** (lowercase i) — GitHub Pages looks for exactly that
  file to render the home page. Not `home.html`, not `me.html`.
- Errors like *"No server is currently available"* during setup are normal — just wait and retry.
- Share the final URL anywhere in the world.

---

## Quick reference

| Concept | Key takeaway |
|---|---|
| Absolute path | From root (`C:\...`); works anywhere but breaks if project moves |
| Relative path | From current file; **use this in web dev** |
| `./` | Current directory (always write it for same-folder files) |
| `../` | Go up one level (chain for more) |
| `href` vs `src` | `href` = links (`<a>`); `src` = resources (`<img>`) |
| `public/` folder | Convention for all non-home HTML pages |
| Boilerplate | `<!DOCTYPE html>` → `<html>` → `<head>` (invisible info) + `<body>` (visible content) |
| `!` + Enter | VS Code Emmet shortcut to generate boilerplate (`.html` files only) |
| `index.html` | Must be the exact home-page filename for GitHub Pages |
| Hosting | Upload file **contents** to a public repo → Settings → Pages → `main` branch |

## Why this matters going forward

File paths underpin **everything** from here on — linking a CSS stylesheet (`<link href="./style.css">`),
importing images, loading JavaScript files, and referencing assets in frameworks all use the exact same
`./` / `../` rules. The boilerplate is the starting point of every future page. And now that the portfolio
is live on GitHub Pages, the CSS you learn next can be pushed live the same way — instantly visible to the
whole world.
