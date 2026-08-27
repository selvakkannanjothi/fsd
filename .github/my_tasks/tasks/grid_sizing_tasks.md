# Practice Tasks: CSS Grid — Sizing (Fixed / Auto / Fractional / MinMax / Repeat)

Based on: `course_content/GRID/grid_sizing.txt`, `EX 10.1 Grid Sizing`
Notes: `.github/my_tasks/concepts/concept_grid_sizing.md`

## Problem Statements (With Input Data)

1. **Responsive or not?** Given this CSS, is the layout responsive to the browser window being resized?
   Would switching both values to `25rem` / `50rem` (root font-size 16px) change your answer? Would
   *zooming* the browser change anything in the `rem` version?
   ```css
   .container {
     display: grid;
     grid-template-columns: 400px 800px;
   }
   ```

2. **Shorthand round-trip.**
   a) Rewrite this as a single `grid-template` shorthand line:
      ```css
      grid-template-rows: 100px 200px;
      grid-template-columns: 400px 800px;
      ```
   b) Split this shorthand back into the two longhand properties:
      ```css
      grid-template: 1fr 2fr / 250px auto;
      ```

3. **`auto` column arithmetic.** Ignore `gap`/padding for this one.
   ```css
   .container {
     width: 1000px;
     display: grid;
     grid-template-columns: 200px auto;
   }
   ```
   What is column 2's pixel width? Now the container shrinks to `600px` wide — what is column 2's
   width now?

4. **`auto` row contrast.**
   ```css
   .container {
     display: grid;
     grid-template-rows: 100px auto;
   }
   ```
   Row 2 holds a `<div>` with one short line of text (needs ~20px). Later, that div is replaced with a
   long paragraph that wraps to ~150px tall. What is row 2's height in each case? Does row 1's height
   change in either case? Why not?

5. **The `fr` sibling gotcha.**
   ```css
   .container {
     display: grid;
     grid-template-rows: 1fr 1fr;
   }
   ```
   Row 1's content only needs about 40px. Row 2's content is a large block of text that needs about
   300px. Because both rows share a `1fr : 1fr` ratio, predict — in words, not exact pixels — what
   happens to row 1's rendered height, and explain *why* using the ratio rule from §4 of the concept
   notes.

6. **Clamp logic.** For `grid-template-columns: minmax(400px, 800px) 1fr;`, suppose the grid algorithm
   would naturally hand column 1 each of these amounts of space if it were unclamped. State the actual
   rendered width in each case:
   ```
   a) 300px
   b) 550px
   c) 900px
   ```

7. **`repeat()` round-trip (non-`fr` version).**
   a) Rewrite using `repeat()`:
      ```css
      grid-template-columns: 150px 150px 150px 150px;
      grid-template-rows: 1fr 1fr 1fr;
      ```
   b) Expand this back out longhand:
      ```css
      grid-template-columns: repeat(3, 2fr);
      ```

8. **Fewer items than cells.**
   ```css
   .container {
     display: grid;
     grid-template-columns: 100px 100px 100px;
     grid-template-rows: 100px 100px;
   }
   ```
   Only 5 `<div>` children exist (the template has 6 cells). Describe which cell(s) end up empty, and
   confirm whether Grid fills row-by-row or column-by-column first.

9. **More items than cells.**
   ```css
   .container {
     display: grid;
     grid-template-columns: 200px 200px;
     grid-template-rows: 200px 200px;
   }
   ```
   There are 6 `<div>` children (2 more than the 4 template cells).
   a) With no `grid-auto-rows` set, what decides item 5 & 6's box **width**? What decides their **height**?
   b) Now add `grid-auto-rows: 150px;` — what is item 5 & 6's height now?

10. **`EX 10.1` — write the full solution.** Using only the requirements below (don't peek at the concept
    notes' worked solution first), write the complete `.grid-container` CSS:
    ```
    Row 1: 1fr
    Row 2: 1fr (same height as row 1)
    Row 3: 2fr (double rows 1-2)
    Row 4 (not part of the template): fixed 50px
    Column 1: expands to fill available space, shrinks down to content minimum
    Column 2: fixed 400px
    Column 3: flexible between 200px and 500px
    ```

## Questions and Answers

11. In one sentence, why doesn't switching `px` to `rem` make a grid responsive to the browser
    **window** being resized?

12. Why does the instructor deliberately avoid the `grid-template` shorthand while teaching, even
    though it's completely valid CSS?

13. State the `auto`-on-a-row vs `auto`-on-a-column difference in one sentence each.

14. Which earlier trap (from `EX 10.0`, the chessboard) does this row/column asymmetry rhyme with?
    What's the one-line rule that unifies both traps?

15. Why can growing the content of **one** `fr` row cause a sibling `fr` row — whose own content never
    changed — to also grow taller?

16. Which two Flexbox properties does `minmax()` combine into a single Grid function? Which argument is
    the floor and which is the ceiling?

17. If a grid template declares 6 cells but only 4 items exist in the HTML, what happens to the other
    2 cells? Are they invisible boxes sitting there, or something else entirely?

18. When Grid creates an implicit row for extra items, what decides that row's default **width**? What
    decides its default **height**?

19. What exactly does `grid-auto-rows` override? Give one real scenario (from the transcript) where
    you'd actually need it.

20. Name the two Chrome DevTools "Layout pane" options that let you read a track's exact computed pixel
    size without doing any math yourself.

## Self Assignments (No Answers)

21. Open `course_content/GRID/EX 10.1 Grid Sizing/test.html` in a browser. **Before** checking the
    concept notes' worked solution, write the `.grid-container` CSS yourself in the textarea, click
    Apply CSS, and compare against the green reference box. Only then check §9 of
    `concept_grid_sizing.md`.

22. Build a 2-column grid (`auto 300px`) and record the `auto` column's rendered pixel width (via
    DevTools) at three different window widths. Confirm each number equals the container's width minus
    300px.

23. Recreate the transcript's own "sibling `fr` row" experiment: a `grid-template-rows: 1fr 1fr`
    container, a one-word row 1 and a short-paragraph row 2. Note row 1's height, then paste ~10x more
    text into row 2 and note row 1's new height. Explain the result out loud using the ratio rule.

24. Build a 3-column grid `minmax(400px, 800px) 1fr 1fr` and slowly shrink/grow the browser window
    until you can see column 1 hit **both** its floor and its ceiling. Note the window widths where
    each clamp kicks in.

25. Build a `2×2` template grid, then use extra HTML (or a couple of lines of JS) to push in a 5th and
    6th item. Observe the implicit row's size with `grid-auto-rows` unset, then set
    `grid-auto-rows: 250px` and observe again.

26. From memory (no peeking until stuck), rebuild the Grid Sizing demo's five pages — fixed / auto /
    fractional / minmax / repeat — in one blank HTML file, then compare side-by-side against
    <https://appbrewery.github.io/grid-sizing>.

27. DevTools scavenger hunt: find any real website using CSS Grid, open the Layout pane, enable
    **Show track sizes**, and write down the exact computed pixel size of every row/column you find.

## Self-check

- [ ] I can explain why `rem` tracks are relative to root font-size but still not "responsive" to window size.
- [ ] I know `grid-template` is valid shorthand, and why the course avoids it for now.
- [ ] I can state the `auto` row vs `auto` column asymmetry without hesitating, and link it to `EX 10.0`'s trap.
- [ ] I can predict what happens to an `fr` row's height when a sibling `fr` row's content grows.
- [ ] I can explain `minmax()` as a single-function floor + ceiling, and map it back to Flexbox's `min`/`max-width`.
- [ ] I know what happens to leftover cells when there are too few items.
- [ ] I know the two default rules for an implicit row's size, and how `grid-auto-rows` overrides the height one.
- [ ] I can use the DevTools grid overlay ("Show track sizes") to read exact track sizes.
- [ ] I attempted `EX 10.1 Grid Sizing` myself in `test.html` before checking the worked solution.
