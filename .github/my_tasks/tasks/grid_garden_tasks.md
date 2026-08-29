# Practice Tasks: Grid Garden (28-Level Reinforcement)

Based on: <https://appbrewery.github.io/gridgarden/>
Notes: `.github/my_tasks/concepts/concept_grid_garden.md`
Completion: **28/28 verified on 2026-08-29**

## Problem Statements (With Input Data)

1. **Positive lines.** In a five-column grid, write the rule that places an item from vertical line 2
   through vertical line 5. State how many tracks it covers.

2. **Negative lines.** Write the same placement using the final line (`-1`) as the end address.

3. **Reverse direction is valid.** Predict the occupied columns:
   ```css
   .item { grid-column-start: 5; grid-column-end: 2; }
   ```

4. **Destination vs count.** Explain the difference and draw both results:
   ```css
   grid-column: 2 / 5;
   grid-column: 2 / span 3;
   ```

5. **Two axes.** Place an item over rows 2-4 and columns 3-6 using:
   a) `grid-row` + `grid-column`; b) `grid-area`.

6. **Decode the rectangle.** Draw the region selected by:
   ```css
   grid-area: 1 / 2 / 4 / 6;
   ```

7. **Ordering.** Five items default to `order: 0`. Give `.poison` a value that moves it after all the
   others, then a value that moves it before all the others.

8. **Percentage tracks.** Write eight equal percentage columns without `repeat()`, then refactor the
   line with `repeat()`.

9. **Mixed units.** Given a 1000px-wide grid with `font-size: 16px`, calculate the first three tracks:
   ```css
   grid-template-columns: 100px 3em 40%;
   ```
   State what happens to any unused width.

10. **Fixed-first arithmetic.** A grid is `1100px` wide with no gap:
    ```css
    grid-template-columns: 50px 1fr 1fr 1fr 50px;
    ```
    Calculate every column width.

11. **Ratio after subtraction.** A grid is `1075px` wide with no gap:
    ```css
    grid-template-columns: 75px 3fr 2fr;
    ```
    Calculate all three widths and show the subtract-then-share steps.

12. **Zero tracks on purpose.** Explain why `grid-template-rows: 50px 0 0 0 1fr` can be correct. Contrast
    it with the earlier accidental blank-board bug caused by `1fr` rows in a zero-height container.

13. **Shorthand decoding.** Expand each into explicit rows and columns:
    ```css
    a) grid-template: 60% 40% / 200px;
    b) grid-template: 1fr 50px / 20% 1fr;
    ```

14. **Gap-aware arithmetic.** A 1000px grid has five columns, four `10px` gaps, fixed outside columns
    of `50px`, and three equal `1fr` middle columns. Calculate the middle column width.

## Questions and Answers

15. What is the difference between a grid track and a grid line?

16. Why does a five-column grid have six vertical line addresses?

17. What does `-1` identify on either axis?

18. Can `span` use a negative number? What is `span` expressing?

19. State the `grid-area` value order without looking.

20. State the `grid-template` shorthand order without looking. Why is it easy to confuse with
    `grid-area`?

21. What does `order` control during Grid auto-placement? Why does it not replace `grid-column`?

22. With `50px 1fr 2fr`, which values are resolved first and how is the remaining space divided?

23. Why are `fr` units ratios rather than pixel values?

24. What exact evidence showed that all 28 Grid Garden levels were completed?

## Self Assignments (No Answers)

25. Reset Grid Garden and complete all 28 levels yourself without opening the solution table. Record
    the three levels where you pause longest and explain the confusion behind each one.

26. Complete levels 1-17 a second time using the most compact valid shorthand whenever the game allows
    it. Compare clarity against the property's longhand form.

27. On paper, reproduce the 28-level solution ladder from memory in four groups: lines (1-9),
    shorthands/areas (10-17), order (18-19), tracks (20-28).

28. Build a mini "garden" with 5 x 5 cells, carrots and weeds represented by emoji, and two overlay
    items named `#water` and `#poison`. Recreate any five Grid Garden levels locally.

29. Make a calculator table for fixed + `fr` layouts. Test at least five container widths and include
    gaps in every calculation.

30. Create one deliberately wrong answer for each category - line direction, `span`, `grid-area`,
    `order`, and `grid-template` - then use DevTools to explain exactly why each visual result is wrong.

## Self-check

- [ ] I completed Grid Garden 28/28 myself after reviewing the notes.
- [ ] I can use positive/negative grid lines without trial and error.
- [ ] I know the difference between an end line and `span`.
- [ ] I can recite the four-value `grid-area` order.
- [ ] I can recite the `grid-template: rows / columns` order.
- [ ] I calculate fixed tracks and gaps before sharing remaining space with `fr`.
- [ ] I know when zero-sized tracks are intentional versus accidental.
