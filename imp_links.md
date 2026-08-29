# Important Links

Running collection of reference/useful links gathered while working through the FSD course. Append new links here as they come up in lessons.

## Flexbox
- [A Complete Guide to Flexbox (CSS-Tricks)](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) — full flexbox property reference
- [MDN: Universal selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors) — from `EX 9.1 Flex Direction`
- [MDN: CSS Combinators](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Combinators) — from `EX 9.1 Flex Direction`
- [Flex Layout demo playground (appbrewery)](https://appbrewery.github.io/flex-layout/) — play with order/wrap/justify/align live, from `flexlayout_transcript.txt`
- [Flexbox Froggy](https://appbrewery.github.io/flexboxfroggy/) — interactive game to practice flex properties, from `flexlayout_transcript.txt`

### Flex Sizing (grow / shrink / basis) — ⚠️ weak area, keep these handy
- [Flexbox Sizing Exercise (appbrewery)](https://appbrewery.github.io/flexbox-sizing-exercise/) — **the lesson's own exercise**: make the blue flexbox behave like the green one (items 200/200/400), from `flexsizing_transcript.txt`
- [MDN: `flex` shorthand](https://developer.mozilla.org/en-US/docs/Web/CSS/flex) — the authoritative list of what `flex: 1` / `auto` / `none` / `initial` expand to
- [MDN: `flex-basis`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis) · [`flex-grow`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-grow) · [`flex-shrink`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink)
- [MDN: Controlling ratios of flex items along the main axis](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Controlling_ratios_of_flex_items_along_the_main_axis) — the single best page on grow/shrink/basis
- [MDN: `min-width`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-width) — note the `auto` value, the hidden shrink floor on flex items
- [Josh Comeau — An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/) — best visual explanation of the grow/shrink algorithm anywhere
- [CSS-Tricks — Flexbox and Truncated Text](https://css-tricks.com/flexbox-truncated-text/) — the `min-width: 0` bug, written up properly
- [Flexbox Defense](http://www.flexboxdefense.com/) — tower-defense game, drills `justify-content`/`align-items` under pressure
- [What The Flexbox?! (Wes Bos, free)](https://flexbox.io/) — 20 short videos, good second pass
- [Can I Use — Flexbox](https://caniuse.com/flexbox) — browser support check
- Local cheat sheet poster: `course_content/FLEXBOX/css-flexbox-poster.png` · course formula slide: `course_content/FLEXBOX/flexbox_sizing_formula.png`

### EX 9.4 Pricing Table Project (section capstone)
- [MDN: `list-style`](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style) — bullets live on the `<ul>`; so does the default `padding-left: 40px`
- [MDN: CSS values and units](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Values_and_units) — `px` / `em` / `rem` / `%` / `vw` / `vh`, and why axes matter
- [MDN: `min-height`](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height) — `min-height: 100vh` is the safer idiom than `height: 100vh` for full-screen sections
- [MDN: Centering in CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_box_alignment/Box_alignment_in_flexbox) — box alignment in flexbox, the "centre anything" recipe
- [Google Font: Sono](https://fonts.google.com/specimen/Sono) — the font used by the pricing table starter file

## CSS Grid
- [Grid vs Flexbox side-by-side demo (appbrewery)](https://appbrewery.github.io/grid-vs-flexbox/) — **the lesson's own demo**: resize the window and watch grid snap to lines while flexbox squishes, from `grid_display.txt`
- [A Complete Guide to CSS Grid (CSS-Tricks)](https://css-tricks.com/snippets/css/complete-guide-grid/) — the Grid counterpart to the flexbox cheat sheet; separates container vs item properties
- [MDN: CSS grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout) — the module landing page, start here for anything grid
- [MDN: `grid-template-columns`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns) · [`grid-template-rows`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows)
- [MDN: the `<flex>` (`fr`) unit](https://developer.mozilla.org/en-US/docs/Web/CSS/flex_value) — what `1fr` actually resolves to, and why it needs available space
- [MDN: `repeat()`](https://developer.mozilla.org/en-US/docs/Web/CSS/repeat) — `repeat(8, 1fr)` instead of writing `1fr` eight times
- [MDN: `gap`](https://developer.mozilla.org/en-US/docs/Web/CSS/gap) — same property as in flexbox, spaces both rows and columns in a grid
- [Josh Comeau — An Interactive Guide to CSS Grid](https://www.joshwcomeau.com/css/interactive-guide-to-grid/) — best visual explanation of grid anywhere, the grid twin of his flexbox guide
- [Grid Garden - App Brewery course version](https://appbrewery.github.io/gridgarden/) — **completed 28/28 on 2026-08-29**; drills line placement, negative lines, `span`, `grid-area`, `order`, track sizing, `fr`, and `grid-template`
- [Grid Garden - original](https://cssgridgarden.com/) — the original Grid equivalent of Flexbox Froggy
- [Grid by Example (Rachel Andrew)](https://gridbyexample.com/) — copy-paste layout patterns from one of the spec authors
- [Can I Use — CSS Grid](https://caniuse.com/css-grid) — browser support check

### Grid Sizing (fixed / auto / fr / minmax / repeat / implicit tracks)
- [Grid Sizing demo (appbrewery)](https://appbrewery.github.io/grid-sizing) — **the lesson's own demo**: fixed/auto/fractional/minmax/repeat playground + the "Test" page exercise (`EX 10.1`), from `grid_sizing.txt`
- [MDN: `grid-template`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template) — the `rows / columns` shorthand (recognise it, don't write it yet)
- [MDN: `minmax()`](https://developer.mozilla.org/en-US/docs/Web/CSS/minmax) — one function combining a track's floor and ceiling
- [MDN: `grid-auto-rows`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-rows) · [`grid-auto-columns`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-columns) — sizing implicitly-created tracks
- [Chrome DevTools — Inspect CSS grid layouts](https://developer.chrome.com/docs/devtools/css/grid/) — the "grid" badge, overlay, and **Show track sizes** to read exact computed pixel values

### Grid Placement + Grid Garden
- [MDN: `grid-column`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column) · [`grid-row`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-row) — line-based start/end shorthands and `span`
- [MDN: `grid-area`](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-area) — `row-start / column-start / row-end / column-end`
- [MDN: `order`](https://developer.mozilla.org/en-US/docs/Web/CSS/order) — visual auto-placement order and the accessibility warning about DOM/focus order
- [Flexbox Froggy](https://codepip.com/games/flexbox-froggy/) — linked from the Grid Garden completion screen; companion practice for one-dimensional layout
- [Codepip coding games](https://codepip.com/) — additional CSS/HTML coding games linked from the Grid Garden completion screen

## HTML Reference
- [MDN: `<a>` anchor element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a) — from `html_part6.txt`
- [MDN: `<img>` element (height attribute)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-height) — from `EX 4.3 HTML Portfolio Project`

## CSS Reference
- [MDN: CSS named colors](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/named-color) — from `css_colors.txt`
- [MDN: `height` property](https://developer.mozilla.org/en-US/docs/Web/CSS/height) — from `EX 5.4 Color Vocab Project`
- [MDN: `width` property](https://developer.mozilla.org/en-US/docs/Web/CSS/width) — from `EX 5.4 Color Vocab Project`
- [MDN: `text-transform` property](https://developer.mozilla.org/en-US/docs/Web/CSS/text-transform) — from `EX 6.4 Motivation Meme Project`
- [RGB Mixer (csfieldguide.org.nz)](https://www.csfieldguide.org.nz/en/interactives/rgb-mixer/) — interactive color mixer, from `css_colors.txt`
- [Bootstrap 5.0.2 CSS CDN](https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css) — from `EX 8.2 Responsiveness`

## Fonts
- [Google Font: Caveat](https://fonts.google.com/specimen/Caveat) — from `EX 6.1 Font Properties`
- [Google Font: Libre Baskerville](https://fonts.google.com/specimen/Libre+Baskerville) — from `EX 6.4 Motivation Meme Project`

## CSS Art / Inspiration
- [Diana Adrian — Pure CSS Lace Portfolio](https://diana-adrianne.com/purecss-lace/) — from `css_flag_project.txt`
- [Simpsons made entirely in CSS](https://pattle.github.io/simpsons-in-css/) — from `css_flag_project.txt`
- [Flag of Laos reference](https://appbrewery.github.io/flag-of-laos/) — from `EX 7.3 CSS Flag Project`
- [CSS Inspection practice site](https://appbrewery.github.io/css-inspection/) — from `font_properties_practice_website.txt`

## Internet Fundamentals
- [nslookup.io](https://nslookup.io) — look up a website's IP address
- [Submarine Cable Map](https://submarinecablemap.com) — explore the physical undersea internet cables

## Exercise Sample Data
Links used as sample data/content inside practice exercises (not learning references, kept here for completeness since the repo was scanned for all links).
- https://www.producthunt.com/
- https://smashthewalls.com/
- https://www.wordle.net/ / https://www.nytimes.com/games/wordle
- https://hackertyper.net/ / https://hackertyper.com/
- https://stellarium-web.org/
- https://www.google.com/maps/@35.7040744,139.5577317,3a,75y,289.6h,87.01t,0.72r/data=!3m6!1e1!3m4!1sgT28ssf0BB2LxZ63JNcL1w!2e0!7i13312!8i6656 (birthday invite location link)
- https://raw.githubusercontent.com/appbrewery/webdev/main/kitten.jpeg
- https://raw.githubusercontent.com/appbrewery/webdev/main/puppy.gif
- https://raw.githubusercontent.com/appbrewery/webdev/main/birthday-cake3.4.jpeg
