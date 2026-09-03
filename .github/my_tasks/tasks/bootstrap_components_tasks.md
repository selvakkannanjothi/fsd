# Practice Tasks: Bootstrap — Components, Examples & Spacing Utilities

Based on: `course_content/11.0 Bootstrap/11.2 bootstrap_components_transript.txt`
Build folder: `course_content/11.0 Bootstrap/EX 11.2 Bootstrap Components/`
Notes: `.github/my_tasks/concepts/concept_bootstrap_components.md`

Keep beside you while answering:
Spacing scale `0 = 0 · 1 = .25rem · 2 = .5rem · 3 = 1rem · 4 = 1.5rem · 5 = 3rem`
Sides `t` top · `b` bottom · `s` start(left) · `e` end(right) · **`x` = left+right** · **`y` = top+bottom**
Breakpoints *(none)* `<576` · `sm ≥576` · `md ≥768` · `lg ≥992` · `xl ≥1200` · `xxl ≥1400`

---

## Problem Statements (With Input Data)

1. **Two classes, two jobs.** Write the markup for a large red button that says "Delete Account".
   Then say, for each class you wrote, whether it controls *shape* or *colour* — and name the one
   extra class you would add to make it an outline button instead of a filled one.

2. **Decode the spacing.** Give the exact CSS (property and rem value) for each of these, straight
   from the built Move It page:
   ```
   a) mb-2        b) px-4        c) my-5        d) pt-5
   e) me-auto     f) mb-2 mb-lg-0               g) me-sm-3
   ```

3. **⚠️ The x/y trap.** A designer asks for *"16px of breathing room above and below this card, and
   nothing on the sides."* Two answers are on the table:
   ```html
   <div class="card mx-3">…</div>
   <div class="card my-3">…</div>
   ```
   a) Which is correct?
   b) What does the *wrong* one actually do?
   c) The video's spoken definition would pick the wrong one — quote what it says and correct it in
      one sentence.

4. **Write the class, don't write the CSS.** Convert each of these hand-written rules into the single
   Bootstrap utility class that replaces it. Mark any that Bootstrap **cannot** express.
   ```css
   a) margin-top: 1rem;
   b) padding: 0.5rem;
   c) margin-left: auto; margin-right: auto;
   d) padding-top: 1.5rem; padding-bottom: 1.5rem;
   e) margin-bottom: 2.5rem;
   f) margin-bottom: 1rem;  /* but only from 768px up */
   g) padding: auto;
   ```

5. **The dead component.** You paste a Bootstrap navbar. It renders beautifully: correct font,
   correct colours, correct hamburger icon at narrow widths. Clicking the hamburger does nothing, and
   the Services dropdown does nothing either.
   a) What is missing, exactly?
   b) Where in the file does it go and why *there*?
   c) Which of these would also be broken by the same cause, and which would be fine?
      `btn-primary` colours · the carousel arrows · `col-lg-6` widths · a modal · `shadow-lg`
   d) You swap `bootstrap.bundle.min.js` for `bootstrap.min.js`. The hamburger still works but the
      dropdown does not. Why?

6. **The half-styled section.** You copy a Features section out of Bootstrap's Examples page. The
   text, columns and gaps are all correct, but where the example had blue rounded squares behind its
   icons, you have bare icons on white.
   a) Nothing is broken and no console error appears. Why not?
   b) Describe the exact DevTools step that identifies what is missing — what column are you reading?
   c) The missing rule turns out to be `.feature-icon { width: 4rem; height: 4rem; border-radius:
      0.75rem; }`. How can you tell that rule is *not* part of Bootstrap without searching for it?

7. **The invisible icon.** You copy this straight out of a Bootstrap Examples page into your own file:
   ```html
   <svg class="bi" width="30" height="30"><use xlink:href="#briefcase"></use></svg>
   ```
   Nothing appears — but the layout has a 30×30 gap where it should be.
   a) What does `<use xlink:href="#briefcase">` actually point at, and why is it empty in your file?
   b) Give two different working fixes.
   c) The same bug is still live in the built Move It footer. Find it and say which line.

8. **The carousel challenge (do it from the brief, don't look at the answer).** You paste Bootstrap's
   carousel-with-indicators snippet in. It works, but it spans the full window width and is taller
   than the screen — the sections above it are all neatly inset.
   a) What single wrapper fixes both problems?
   b) Why does fixing the *width* also fix the *height*? (Look at `class="d-block w-100"` on the
      slide images.)
   c) State the general rule this is an instance of, in one sentence.

9. **`<img>` vs inline `<svg>`.** You have `<img src="./briefcase.svg" alt="briefcase">` inside a
   button, and you want the icon to turn white when the button is hovered.
   a) Will `button:hover img { fill: white; }` work? Why or why not?
   b) Which of the three ways to include an SVG *does* let you do this, and what makes it different?
   c) Bootstrap ships `.icon-link > .bi { width: 1em; height: 1em; }`. The Move It chevrons carry
      `class`-less `<img>` tags and render at 16×16 instead. Explain in one sentence, and say what
      this forces the video to do on every single icon.

10. **Roles vs colours.** You build a page with `style="background-color: white; color: black"` on
    every section. Your colleague builds the same page with `bg-body` and `text-body`. Someone then
    adds `data-bs-theme="dark"` to the `<html>` tag.
    a) What happens to each page?
    b) Explain the mechanism — what is Bootstrap 5.3 actually reassigning?
    c) Why does this make `success` a better class name than `green`?

11. **Predict the render.** For each, say what the user sees. All of Bootstrap's CSS and JS are loaded.
    ```html
    a) <button class="btn-success">Ok</button>
    b) <button class="btn">Ok</button>
    c) <div class="mt-6">Content</div>
    d) <a class="nav-link dropdown-toggle" href="#">Services</a>   <!-- data-bs-toggle removed -->
    e) <div class="card p-auto">Content</div>
    ```

12. **Your own CSS loses.** You write `.my-footer { margin-bottom: 40px; }` and apply it to a div that
    already has Bootstrap's `mb-2`. The margin comes out as 8px.
    a) Why did your rule lose, given it is later in the cascade and equally specific?
    b) Give two ways to win, and say which one is the better habit.

13. **Read the real markup.** Line from the built Move It hero:
    ```html
    <div class="d-grid gap-2 d-sm-flex justify-content-sm-center mb-5">
    ```
    Separate every class into *component* vs *utility*, and describe the layout at 400px versus at
    800px. (`d-grid` = `display: grid`, `d-sm-flex` = `display: flex` from 576px up.)

14. **Extraction discipline.** You are on Bootstrap's Examples → Heroes page and want the hero
    section. You right-click the `<h1>`, choose Copy element, paste it — and get only the heading.
    a) What step did you skip?
    b) What is the risk of overshooting in the other direction?
    c) What is the visual signal that tells you when you have hovered to exactly the right node?

15. **Rebuild it without Bootstrap.** Write the plain CSS that reproduces this line's effect:
    ```html
    <div class="col-lg-6 mx-auto px-4 py-5">…</div>
    ```
    Then say in one sentence what Bootstrap actually bought you here — and one thing it cost you.

---

## Questions and Answers

**Q1. What is the difference between a Component and a Utility?**
A component is a *noun* — a pre-built thing with structure and often behaviour (`navbar`, `carousel`,
`card`, `btn`). A utility is an *adjective* — a single-property tweak (`mt-3`, `d-flex`,
`text-center`, `shadow-lg`). Real markup is one component class plus a handful of utility classes.
Layout (`container`/`row`/`col`) is the third toolbox, from lesson 11.0.

**Q2. Why does a Bootstrap button need two classes?**
`btn` is the *shape* — padding, font, radius, hover, focus ring. `btn-success` is the *colour role*.
Splitting them means one shape × nine colours, instead of nine duplicated rule blocks. The same
split repeats across Bootstrap: `alert` + `alert-danger`, `text-bg-primary`, `border-warning`.

**Q3. Are the colour names colours or roles?**
Roles. `primary` happens to be blue, `success` happens to be green — but the names describe the
*job* (main action / it worked / careful / destructive). That indirection is what makes §9's dark
mode free: a class called `btn-green` could not follow you into a dark theme.

**Q4. Why two CDN links, and what breaks if you skip one?**
CSS gives **looks**, JS gives **behaviour**. Skip the CSS and you get an unstyled wall of text —
obvious. Skip the JS and everything *looks* perfect and nothing *moves*: hamburger, dropdowns,
carousel, modals, tooltips, accordion are all dead. That second failure is the sneaky one, because
nothing errors.
**The rule: looks right but doesn't move → you forgot the script tag.**

**Q5. Why does the script tag go just before `</body>`?**
So all the HTML exists before the script runs and tries to wire it up. Same reason scripts generally
go at the bottom: the browser parses top-to-bottom.

**Q6. What does `bundle` mean in `bootstrap.bundle.min.js`?**
It includes **Popper.js**, the positioning engine that dropdowns, tooltips and popovers need to place
themselves relative to their trigger. Plain `bootstrap.min.js` does not include it — collapse still
works, dropdowns do not.

**Q7. What are the `data-bs-*` attributes for?**
They are how pasted HTML *talks to* Bootstrap's JavaScript without you writing any:
`data-bs-toggle="collapse"` (what kind of behaviour), `data-bs-target="#navbarSupportedContent"`
(which element to act on), `data-bs-slide="next"` (which action). Delete one while "tidying up" a
snippet and the component silently goes quiet.

**Q8. Docs → Components vs Examples — what is the difference and which should I reach for?**
Components gives you *one* thing with all its variants and its API. **Examples gives you whole page
sections** — a hero that already contains a heading, a paragraph, two buttons and an image, spaced
and laid out. For building a page fast, Examples is the better shop, and it is the one beginners
never find because it is not in the main docs nav. Move It's navbar layout, hero, features and footer
all came from Examples; only the buttons and carousel came from Components.

**Q9. What is the extraction workflow, in order?**
Find the section on the Examples page → right-click → Inspect → **hover upward through the DOM tree
watching the blue highlight** until it covers exactly the region you want → right-click that node →
Copy → Copy element → paste → replace `src`, `alt` and text. **Step 3 is the actual skill**: too
shallow gets a fragment, too deep drags in the example page's own layout wrapper.

**Q10. ⭐ What does copy-paste NOT give you?**
Three kinds of debt:
1. **Custom CSS** — rules that were never Bootstrap's (`.feature-icon`). You get the HTML; the
   stylesheet stays behind.
2. **Sprite icons** — `<use xlink:href="#briefcase">` points at a `<symbol>` defined on *that* page.
   In your file it points at nothing and renders as an empty box of the right size.
3. **Placeholder content** — `src`, body copy, and especially `alt`, which never shows up when you
   look at the page and therefore survives.

**Q11. How do I tell whether a missing rule is Bootstrap's or the example page's own?**
Inspect the element on the *example* site and **read the source-file column** on the right of the
Styles pane. Rules from `bootstrap.css` / `utilities.css` came with Bootstrap — you already have
them. Rules from any other filename are that page's custom CSS and you must copy them yourself.
**Read the source-file column, not the class names.**

**Q12. Why is `.feature-icon` needed at all when the div already has six Bootstrap classes?**
The Bootstrap classes (`d-inline-flex`, `align-items-center`, `justify-content-center`,
`text-bg-primary`, `bg-gradient`, `fs-2`, `mb-3`) colour and centre the box — but nothing gives it a
*size or a corner radius*. `.feature-icon { width: 4rem; height: 4rem; border-radius: 0.75rem }` is
the one hand-written rule that makes it a rounded square. Verified: `feature-icon` appears nowhere in
`bootstrap@5.3.0-alpha2`.

**Q13. ⭐ The carousel is full-bleed and too tall. What fixes it?**
Wrap it in `<div class="container">`. Not a carousel property — a **layout** answer from lesson 11.0.
`.container` caps the width at 540/720/960/1140/1320px; the slide images are `d-block w-100`
(`width: 100%`), so they take the container's width, line up with everything above, and the height
follows from the aspect ratio.
**The general rule: sizing a component is usually its parent's job.** Bootstrap components are
`width: 100%` by design precisely so the container decides. Same idea as *"you don't size the chess
squares, you size the board"* from EX 10.0.

**Q14. What is the spacing formula?**
`{property}{sides}-{size}`, with an optional breakpoint infix: `{property}{sides}-{breakpoint}-{size}`.
`m` = margin (outside the border), `p` = padding (inside it).

**Q15. 🚨 What do `x` and `y` mean — and what does the video say?**
**`x` = horizontal = left + right. `y` = vertical = top + bottom.** Verified in the stylesheet:
```css
.mx-3 { margin-right: 1rem !important; margin-left:   1rem !important; }
.my-3 { margin-top:   1rem !important; margin-bottom: 1rem !important; }
```
**The video says this backwards** — *"for both the top and the bottom, you'll use the x-axis … for
the left and the right … the y-axis."* It then gets it right one sentence later (*"my-3 … the
y-axis"*), which is why it slips past. Memory hook: same x/y as a graph — **x runs across, y runs up
and down**; identical to `column-gap`/`row-gap` and `translateX`/`translateY`.
*Third video error caught in this course, after `flex: 2` and the `col-sm-12` omission. **The class
names and the code are reliable; the spoken explanations are not.***

**Q16. What are `s` and `e`, and why not `l` and `r`?**
**s**tart and **e**nd — logical properties, so `ms-3` is `margin-left` in a left-to-right language and
`margin-right` in Arabic or Hebrew. The layout mirrors itself for free. Bootstrap 4 used `l`/`r`;
Bootstrap 5 switched. So `me-auto` on the navbar means "margin at the *end*: auto", which is what
pushes the search form to the far edge.

**Q17. What are the six sizes, and is there a 6?**
`0 = 0 · 1 = .25rem (4px) · 2 = .5rem (8px) · 3 = 1rem (16px) · 4 = 1.5rem (24px) · 5 = 3rem (48px)`,
plus `-auto` for margins only. **There is no `-6`** — the transcript's *"5 is usually the maximum
you'll need"* undersells it: 5 is the maximum that *exists*. `mt-6` silently does nothing. Off-scale
spacing is one of the things you still write your own CSS for.

**Q18. Why do spacing utilities always beat my own CSS?**
Every one of them carries `!important` — cascade rule 4 from `concept_css.md`, used on purpose so
utilities are the last word. To win: raise your specificity (`.card.my-footer { … }`), use
`!important` yourself (avoid), or — better — **just use the utility class and stop fighting it**.

**Q19. What does `mx-auto` do, and does `p-auto` exist?**
`mx-auto` = `margin-left: auto; margin-right: auto` — the classic centre-a-block trick, used in the
Move It hero on `<div class="col-lg-6 mx-auto">`. `my-auto` exists too. **`p-auto` does not** —
padding cannot be `auto`. Two related traps: `pe-0`…`pe-5` are `padding-right`, but `pe-none` /
`pe-auto` are **`pointer-events`**; and negative margins (`m-n1`) are **not in the stock build** —
they are an opt-in Sass flag.

**Q20. Do the breakpoints from lesson 11.0 work on utilities?**
Yes — that is the real payoff. `mb-2 mb-lg-0` = 0.5rem bottom margin, removed from 992px up.
`me-sm-3` = margin-right 1rem from 576px up. **Every rule from 11.0 comes with it**, including
min-width directionality and *"there is no unset, only override"* — a `mb-2` with nothing above it
keeps applying on a TV.

**Q21. How does dark mode work with one attribute?**
`<html data-bs-theme="dark">`. Bootstrap 5.3 defines everything through CSS custom properties
(`--bs-body-bg`, `--bs-emphasis-color`, …) and ships a `[data-bs-theme=dark] { … }` block that
reassigns them. Measured: body bg `#fff → #212529`, body text `#212529 → #adb5bd`, navbar
`#f8f9fa → #2b3035`. It works *because* your markup asked for roles (`text-bg-primary`,
`bg-body-tertiary`) rather than hard-coded colours — `style="background: white"` would not move.
It can go on any element, not just `<html>`.

**Q22. ⭐ What actually changes when you use `<img src="icon.svg">` instead of inline `<svg>`?**
**An `<img>`-loaded SVG is a separate, isolated document — your page's CSS cannot reach inside it.**
Two consequences, both measurable on the built page:
1. Bootstrap's `.icon-link > .bi { width: 1em; height: 1em }` cannot apply, so the chevron renders at
   its intrinsic **16×16**. **That is why the video hand-writes `height="30"` on every single icon** —
   with inline SVG, Bootstrap would have sized them.
2. You cannot recolour it. `fill="currentColor"` resolves inside the SVG's own document, so a parent's
   `color` does nothing. Inline `<svg>` *does* inherit `currentColor` — which is the whole reason
   Bootstrap Icons ship with it.
The one thing that crosses the boundary is the light/dark **colour scheme**, so the icons do flip
black↔white in dark mode — verified on the built page with the same unchanged `<img>` tag.
**Choose inline `<svg>` whenever the icon must change colour with context, size from CSS, or animate.**

**Q23. What is still worth fixing in the built Move It page?**
Three invisible leftovers, none of which break it: (1) `alt="Example image"` on the hero image —
placeholder alt survives because it is never on screen; (2) the footer's
`<svg><use xlink:href="#bootstrap"></use></svg>`, a sprite pointer with no matching symbol, rendering
as a 40×32 gap; (3) CSS at `5.3.0-alpha2` but JS at `5.3.8` — works, but should be one version.

---

## Self Assignments (No Answers)

1. **Fix the three audit items** in `EX 11.2 Bootstrap Components/index.html`: write real `alt` text
   for the hero image, replace or delete the footer's ghost SVG, and align the CSS and JS versions on
   one stable 5.3.x release. Reload and confirm nothing broke.

2. **Add the missing warm-up.** Drop a `btn btn-success` "Ok" button into the page, then build a row
   of all nine colour roles side by side (`primary` → `dark`) and screenshot it as your own colour
   reference. Add the `-outline-` variants underneath.

3. **Prove the x/y correction to yourself.** Put two identical cards side by side, give one `mx-4`
   and the other `my-4`, and read the computed margins in DevTools. Screenshot it into the concept
   file if it helps it stick — this is the kind of error that comes back if it is only read once.

4. **Kill the script tag.** Comment out the `<script>` in the built page, reload, and write down
   exactly which parts still work and which die. Then restore it. This is the fastest way to make
   Q4's rule permanent.

5. **Swap one icon to inline SVG.** Convert one feature icon from `<img src="briefcase.svg">` to a
   pasted inline `<svg class="bi">`, remove its `height` attribute, and see whether Bootstrap sizes
   it for you. Then try setting `fill` from your own CSS on both versions and compare.

6. **Add a section the lesson never built.** Pick either **Cards** or **Accordion** from Docs →
   Components and add a "What our customers say" section to Move It between Features and the
   carousel. Constraint: use only Bootstrap classes plus at most one custom CSS rule — and write down
   what that one rule had to do.

7. **Spacing-only refactor.** Find every place in the built page where spacing is doing work, and
   write out what each class means in plain CSS in a comment above it. Then change exactly one value
   (e.g. `my-5` → `my-3` on the hero) and describe what moved.

8. **Dark mode for real.** Add `data-bs-theme="dark"` to `<html>` and audit the whole page top to
   bottom. Note anything that looks wrong or unreadable in dark mode — those are the spots where the
   markup asked for a colour instead of a role. Then try putting `data-bs-theme="dark"` on a *single*
   section instead and see what happens.

9. **Build "Move It" a second page from scratch** — a Contact page — using only Examples snippets:
   the same navbar, a Bootstrap form, and the same footer. Link the two pages with the file-path
   rules from `concept_multi_page_websites.md`. Time yourself; that number is the real argument for
   Bootstrap.

10. **Read the stylesheet, not the video.** Open `bootstrap@5.3.x/dist/css/bootstrap.css`, search for
    `.btn-success`, and write down where each of its colours comes from. Then do the same for
    `.carousel-item`. Aim to be able to say what a class does *before* you paste it.

11. **Prep for 11.3 TinDog.** Skim `course_content/11.0 Bootstrap/11.3+TinDog+Project/` and its
    `goal images/`, then list — before starting — which Bootstrap component you would reach for in
    each section of that design. Compare your list against what you actually end up using.
