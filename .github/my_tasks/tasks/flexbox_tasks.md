# Practice Tasks: Flexbox — Display Flex & Flex Direction

Based on: `course_content/FLEXBOX/flexbox_transcript.txt`, `EX 9.0 Display Flex`, `EX 9.1 Flex Direction`
Notes: `.github/my_tasks/concepts/concept_flexbox.md`

## Problem Statements (With Input Data)

1. **Turn a list into a nav bar.** You have this markup — every link currently sits on its own line.
   Write the CSS needed to lay them out horizontally with a 10px gap between items and no bullet points.
   ```html
   <div class="container">
     <p>Page Layout Methods</p>
     <li><a href="./html-table.html">HTML Table</a></li>
     <li><a href="./inline-block.html">Inline-Block</a></li>
     <li><a href="./float.html">Float</a></li>
     <li><a href="./flex.html">Flexbox</a></li>
   </div>
   ```
   (Hint: which element do you put `display: flex` on — the container or the children?)

2. **Predict the width.** Two identical containers hold the same three 100px boxes. One has
   `display: flex`, the other `display: inline-flex`, and both have `border: 5px solid gold`.
   Describe exactly how the two gold borders look different on the page, and say which "old" display
   value each one behaves like.

3. **Write the selector.** Given `<div class="container">` with seven direct-child `<div>`s, write the
   selector that gives **every direct child** a `flex-basis: 100px` — without caring what tag each child
   is, and without accidentally matching a `<div>` nested deeper inside one of them later.

4. **Selector match count.** For this HTML, state how many elements each selector matches:
   ```html
   <div class="container">
     <div class="red">Red<div class="inner">Inner</div></div>
     <div class="blue">Blue</div>
     <p class="note">Note</p>
   </div>
   ```
   ```
   a) .container div
   b) .container > div
   c) .container > *
   d) .container p
   ```

5. **Flip the axis.** Take the exercise container from Q3 (seven coloured boxes laid out in a row) and
   write the one declaration that stacks them vertically instead. What is the default value of that
   property?

6. **Gap units.** Rewrite `gap: 10px` so the gap scales with the site's root font size instead of being
   fixed. Given `html { font-size: 16px; }`, what pixel gap does `gap: 1rem` produce?

7. **Spot the legacy hack.** For each old layout technique below, say (a) what it was originally designed
   for, and (b) why it's a poor choice for whole-page layout today:
   ```
   a) <table> / <tr> / <td>
   b) display: inline-block
   c) position: absolute
   d) float: left
   ```

8. **Refactor.** Rewrite this old float-based three-column layout using Flexbox. Aim for the fewest
   lines possible.
   ```css
   .col { float: left; width: 33%; }
   .footer { clear: both; }
   ```

## Questions and Answers

9. **Where does `display: flex` go** — on the parent container or on the items you want laid out? Why
   does that make sense given the name "flex container"?

10. **What happens to a child's own `display` value** (say a `<span>` that is normally `inline`, or a
    `<li>` that is normally `list-item`) once its parent becomes `display: flex`?

11. **`flex` vs `inline-flex`** — state the one difference in a single sentence, and name the
    non-flex pair it mirrors.

12. **Why is `<table>` still valid HTML** if it's a "no-no" for layout? When *should* you reach for it?

13. **Why is `.container > *` often safer** than `.container div` when styling flex items? Give a
    concrete scenario where `.container div` would produce a bug.

14. **How wide are flex items by default** if you don't set any width or `flex-basis` on them?

15. **Name the tools** the transcript lists as the *right* choices for overall page structure today
    (instead of float/absolute hacks).

## Self Assignments (No Answers)

16. Build a **horizontal nav bar** from scratch: a `<nav>` containing 5 links (Home, About, Services,
    Blog, Contact). Use Flexbox with a gap, remove bullet/underline styling, add a background colour and
    padding, and make the whole bar hug its content using `inline-flex` — then switch it to `flex` and
    note the visual difference in your own words.

17. Recreate the **7-colour stripe stack** from `EX 9.1` from memory: one container, seven coloured
    child `<div>`s, `flex-direction: column`, each child `flex-basis: 100px`, white text, a gold border.
    Then change `flex-direction` to `row` and observe how `flex-basis` now controls a different dimension.

18. Open the `EX 9.0` folder's `html-table.html`, `inline-block.html`, `absolute-position.html` and
    `float.html` side by side with `flex.html`. Count the lines of CSS each layout method needs and write
    a one-paragraph comparison of which was hardest to reason about and why.

19. Take any page you've already built (Motivational Poster, Color Vocab, or your Portfolio) and convert
    one section of its layout to Flexbox. Delete any `float`, `position: absolute` or `inline-block`
    hacks you used there.

20. In DevTools, inspect a real website's nav bar (e.g. github.com). Find the element with
    `display: flex` in the Styles tab, then toggle it off and on to see the layout collapse and rebuild.
    Note which other flex properties that site uses that you haven't learned yet.

## Self-check

- [ ] I know `display: flex` goes on the **container**, not the items.
- [ ] I can explain `flex` vs `inline-flex` and which of `block`/`inline-block` each mirrors.
- [ ] I know a flex container overrides its children's own default `display` values.
- [ ] I can use `gap` with both `px` and `rem`.
- [ ] I can pick between `.container div`, `.container > div` and `.container > *` and justify it.
- [ ] I know `flex-direction: row` is the default and `column` stacks items vertically.
- [ ] I can explain why table/inline-block/absolute/float are legacy choices for page layout.
- [ ] I completed EX 9.0 (Display Flex nav bar) and EX 9.1 (Flex Direction).
