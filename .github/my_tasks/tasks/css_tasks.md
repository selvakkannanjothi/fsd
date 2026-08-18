# Practice Tasks: CSS — Styling, Selectors, Cascade, Box Model, Layout & Projects

Based on: `course_content/CSS/` transcripts, `EX 5.1`, `EX 5.3`, `EX 5.4`, `8.0 CSS Display`,
CSS Positioning, Flag of Laos & Motivational Poster projects
Notes: `.github/my_tasks/concepts/concept_css.md`

## Problem Statements (With Input Data)

1. **Three ways, one heading.** You have an `<h1>` on three separate pages. Write the code to turn it
   (a) blue using **inline**, (b) red using **internal**, (c) green using **external** CSS. Include the
   `<link>` for the external case and name the file `style.css`.

2. **Write the selector only.** For each requirement, write the correct selector (the property/value is
   given — you supply the part before the `{`):
   ```
   a) every <p>                              → color: red;
   b) all elements with class "big"          → font-size: 2rem;
   c) the single element with id "main"      → color: green;
   d) <li> elements whose value attribute = 4 → color: blue;
   e) absolutely everything                  → text-align: center;
   ```

3. **Combinators.** Given a `<div class="box">` that directly contains a `<p>` and a `<ul>`, and the
   `<ul>` contains `<li>` items (some with `class="done"`), write selectors to:
   ```
   a) turn h1 AND h2 blueviolet
   b) turn only the direct-child <p> of .box firebrick
   c) turn every <li> inside .box (any depth) blue
   d) turn only the <li> items that have class "done" seagreen
   ```

4. **Predict the cascade winner.** For each conflict, name the winning color and the *category* that
   decides it (Position / Specificity / Type / Importance):
   ```
   a) In style.css:  h1.title { color: green; }   and   h1#name { color: red; }
   b) In style.css:  .a { color: green; }   then lower down   .b { color: blue; }   (element has both classes)
   c) #name { color: red; } in style.css   vs   style="color: blue" inline
   d) p { color: black !important; } in style.css   vs   style="color: pink" inline
   ```

5. **Font sizing with em vs rem.** Given `html { font-size: 20px; }`, `footer { font-size: 40px; }`, and
   an `<h2>` inside the footer:
   ```
   a) If h2 { font-size: 2em; }  → what px?
   b) If h2 { font-size: 2rem; } → what px?
   c) The footer changes to 80px. What is each h2 now?
   ```

6. **Box model math.** A `<div>` has `width: 200px`, `padding: 20px` (all sides), and
   `border: 10px solid black`. How many pixels of `margin-left` must the *next* box have to sit exactly
   corner-to-corner beside it? Show the arithmetic.

7. **Box model shorthand.** Write single-line declarations for: (a) padding 10px top/bottom and 40px
   left/right; (b) a border-width of 20px top & bottom but 10px left & right; (c) margin 0 on all sides.

8. **Display layout.** You have three `200px × 200px` squares. Write the one CSS property that lays them
   out (a) side by side on one row, (b) stacked vertically. Why does plain `inline` fail for squares?

9. **Rectangle + circle.** Recreate the positioning exercise: a `.blue-box` 500px wide × 300px tall
   placed 200px from the top and left of the page, containing a `.red-circle` (200×200) positioned
   relative to the box, 250px from its left and 150px from its top. Write the CSS (include how you make
   the circle a circle).

## Questions and Answers

10. **Define in your own words** (1-2 sentences each): CSS · the "cascade" · a CSS rule (property vs
    value) · a selector.

11. **When would you choose** inline vs internal vs external CSS? Give the ideal use case for each.

12. **Class vs ID** — what's the one rule about how many elements each may apply to, and which symbol
    selects each?

13. **`>` vs space** — explain the difference between `.box > p` and `.box p`, and give a case where they
    select different elements.

14. **State the cascade order** (the four categories) and, within Specificity, the order from most to
    least specific.

15. **Why prefer `rem` over `em`** for font sizes? What is each one relative to?

16. **The border gotcha** — if you add a 30px border to a 200px-wide box, what is the box's width now, and
    why?

17. **`position` values** — in one line each, what is each of `static`, `relative`, `absolute`, `fixed`
    positioned relative to? Which one leaves the normal document flow?

18. **The relative-parent / absolute-child idiom** — why must the parent be set to `position: relative`
    before an absolutely-positioned child will anchor to it?

19. **DevTools** — what does a **struck-out** style in the Styles pane mean, and which tab shows the final
    resolved value (and inherited properties)?

## Self Assignments (No Answers)

20. **Complete EX 5.1 (Adding CSS).** Make the three pages' `<h1>`s blue/red/green using the three
    different methods; verify against the solution preview.

21. **Complete EX 5.3 (CSS Selectors).** Solve all five TODOs in `style.css` (don't touch `index.html`);
    match `goal.png`.

22. **Complete EX 5.4 (Color Vocab Project).** Create and correctly link `style.css`, size all images to
    200×200, set flashcard titles to `font-weight: normal` via a class, and colour each title to match
    its word. Try it in a language other than Spanish.

23. **Complete 8.0 CSS Display.** Line the three squares up horizontally, then vertically, changing only
    the `display` property.

24. **Build the Flag of Laos.** Pure HTML/CSS, without editing the HTML — target elements with combined
    selectors, use relative-parent/absolute-child positioning and `border-radius: 50%`, and pull the exact
    hex colours from DevTools CSS Overview. Then try your own country's flag.

25. **Build the Motivational Poster.** Bordered image on a black background, big uppercase title in a
    Google Font (discover `text-transform` yourself from MDN), centred by the width/margin trick. Use your
    own image and caption.

26. **Inspect a real site.** Open a website you like, use DevTools → CSS Overview to capture its colours
    and fonts, and note down one palette + font pairing you'd reuse.

27. **Locator crossover.** Pick 5 elements on any page and write a CSS selector for each — then compare to
    how you'd target them with a Selenium/Cypress CSS locator. Note where the syntax is identical.

## Self-check

- [ ] I can write element / class / id / attribute / universal selectors from memory.
- [ ] I know `.box > p` vs `.box p` vs `li.done` and never confuse the spacing rules.
- [ ] I can walk the cascade (Position → Specificity → Type → Importance) to explain any style conflict.
- [ ] I understand the box model layers and that border/padding grow the box outward.
- [ ] I know when to use `block` / `inline` / `inline-block`, and why inline can't be sized.
- [ ] I can use `position: relative` + `absolute` to place a child precisely inside a parent.
- [ ] I can make a circle with `border-radius: 50%`.
- [ ] I completed EX 5.1, 5.3, 5.4, 8.0 Display, the positioning exercise, the Flag of Laos, and the Poster.
