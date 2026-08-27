# Practice Tasks: CSS Grid — `display: grid`

Based on: `course_content/GRID/grid_display.txt`, `EX 10.0 Display Grid`
Notes: `.github/my_tasks/concepts/concept_grid_display.md`

## Problem Statements (With Input Data)

1. **Debug the blank page.** This renders nothing at all in the browser, even though all 64 divs are
   present in the HTML and have background colours. Explain in one sentence *why*, then give two
   different one-line fixes.
   ```css
   .container {
     display: grid;
     grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
     grid-template-rows:    1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
   }
   .white { background-color: #f0d9b5; }
   .black { background-color: #b58863; }
   ```

2. **Do the arithmetic.** Given the CSS below, state the exact pixel width and height of a single grid
   cell. Show the calculation.
   ```css
   .container {
     width: 800px;
     height: 800px;
     display: grid;
     grid-template-columns: repeat(8, 1fr);
     grid-template-rows: repeat(8, 1fr);
   }
   ```

3. **Predict the track sizes.** A grid container is `900px` wide with no `gap`. For each of these,
   write the final pixel width of every column:
   ```
   a) grid-template-columns: 1fr 2fr;
   b) grid-template-columns: 1fr 1fr 1fr;
   c) grid-template-columns: 1fr 2fr 3fr;
   d) grid-template-columns: 300px 1fr 1fr;
   ```

4. **Compress it.** Rewrite each of these using `repeat()`:
   ```
   a) grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
   b) grid-template-rows: 100px 100px 100px;
   c) grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
   ```

5. **Which tool?** For each layout, say whether you'd reach for **Flexbox**, **Grid**, or **both nested**,
   and justify it in one line:
   ```
   a) A horizontal nav bar with 5 links and even spacing
   b) A photo gallery, 4 columns × 3 rows, all tiles aligned
   c) A dashboard: header across the top, sidebar left, main panel right, footer across the bottom
   d) A row of 3 pricing cards that stack on mobile (you built this in EX 9.4)
   e) A weather panel inside a dashboard tile: icon on top, temperature under it, label under that
   ```

6. **Recreate the demo.** Write the complete `<style>` block that produces a 2-column, 2-row grid where
   the right column is twice as wide as the left, both rows are equal height, and there's a `10px`
   gutter between every track.

7. **Delete the redundant line.** One of these declarations is doing nothing. Identify it and explain why
   the board still renders correctly without it.
   ```css
   .container {
     width: 800px;
     display: grid;
     grid-template-columns: repeat(8, 100px);
     grid-template-rows: repeat(8, 100px);
   }
   .white, .black { width: 100px; height: 100px; }
   ```

8. **Why the gaps?** A student builds the chessboard with `repeat(8, 1fr)` for columns and `100px`
   squares, but **forgets** `width: 800px` on the container. On a 1440px-wide monitor they see the
   squares spread out with white space between them. Explain exactly what is 800px wide, what is
   1440px wide, and what is holding the gaps.

9. **Convert the units.** Take the working chessboard and change it so the board is **640px** total with
   80px squares — but only edit **one line** of CSS. Which solution style (size-the-container or
   size-the-children) makes this possible, and why?

## Questions and Answers

10. **What is the one-sentence difference** between Flexbox and Grid? Name the dimension count for each.

11. **Where does `display: grid` go** — on the container or on the items? Which Flexbox property does
    this mirror exactly?

12. **What does the `fr` unit actually mean?** Why is `1fr 2fr` a *ratio* rather than a size?

13. **Which earlier Flexbox property is `fr` most similar to,** and why? Give the equivalent `flex`
    shorthand for `grid-template-columns: 1fr 2fr 3fr`.

14. **What are the two default sizing behaviours of a grid container** — one for width, one for height?
    Which of the two causes `1fr` rows to collapse to zero?

15. **If you only declare `grid-template-columns`** and drop in 64 items, what does Grid do with the
    leftover items? Is the result still a chessboard?

16. **How wide/tall is a grid item** that has no `width` or `height` set? Which Flexbox default value is
    this the same idea as?

17. **True or false:** "Grid is more powerful than Flexbox, so Flexbox was a waste of time." Correct the
    statement and give one concrete example of the two being used together.

18. **Name two ways** Grid and Flexbox can be nested, and say which one the transcript's weather-site
    example uses.

19. **Behaviour under resize:** describe what Grid does versus what Flexbox does when you drag the browser
    window narrower. Which one keeps gaps perfectly aligned, and why?

20. **`gap` in Grid vs `gap` in Flexbox** — is it a new property or one you already know? What does it
    space out in a grid?

## Self Assignments (No Answers)

21. Rebuild the **chessboard from memory** in a blank file — no peeking. Use `repeat()`, then add
    `gap: 2px` and describe how the board changes and whether it's still 800px.

22. Play with <https://appbrewery.github.io/grid-vs-flexbox/>. Resize the window slowly and write down
    **three** concrete behavioural differences you can see between the grid and the flexbox — beyond
    the ones listed in the notes.

23. Open a real 2D site in DevTools (try a news homepage or the Swiss weather site from the lesson).
    Find the element with `display: grid`, read its `grid-template-columns` in the Computed tab, and
    write down what the values translate to. Toggle `display: grid` off to watch the layout collapse.

24. Build a **4×3 photo gallery** with Grid: 12 tiles, equal columns, `gap: 1rem`, and a fixed container
    width. Then add a hover effect. Note how much less CSS this needs than a flexbox version would.

25. Take the **EX 9.4 Pricing Table** you already built and rebuild the card row using Grid instead of
    Flexbox (`grid-template-columns: repeat(3, 1fr)`). Then make it stack on mobile by changing the
    template to `1fr` inside the media query. Compare the two approaches — which reads more clearly?

26. Deliberately break a grid: set `grid-template-rows: 1fr` on a container with no height, confirm the
    collapse in DevTools, then fix it **three** different ways (container height, child height,
    `min-height`). Record which one you'd default to and why.

27. Sketch (on paper) the layout of any website you use daily. Draw the grid lines over it. Count the
    columns and rows, then write the `grid-template-columns` / `grid-template-rows` you'd start with.

## Self-check

- [ ] I can state the 1D vs 2D distinction between Flexbox and Grid without hesitating.
- [ ] I know `display: grid` goes on the **container**.
- [ ] I can explain `fr` as a ratio and calculate real pixel values from it.
- [ ] I know why `1fr` rows collapse to `0px` and can name both fixes.
- [ ] I know a grid container is **full width but content height** by default.
- [ ] I can use `repeat(n, size)` fluently.
- [ ] I know grid items **stretch to fill their cell** on both axes.
- [ ] I can name a case for Flexbox-inside-Grid and Grid-inside-Flexbox.
- [ ] I completed EX 10.0 (Chessboard) — **10/10**.
