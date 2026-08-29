# Practice Tasks: CSS Grid Placement

Based on: `course_content/GRID/EX 10.2 Grid Placement/`
Notes: `.github/my_tasks/concepts/concept_grid_placement.md`

## Problem Statements (With Input Data)

1. **Count lines, not tracks.** A grid has `grid-template-columns: repeat(4, 1fr)` and
   `grid-template-rows: repeat(3, 100px)`. State the number of vertical and horizontal grid lines.

2. **Place a header.** Write the item rule for a header that starts at column line 1, ends at column
   line 5, and occupies only the first row.

3. **Same shape, two syntaxes.** Express this area once with `grid-column` + `grid-row`, and once with
   `grid-area`:
   ```text
   row-start: 2, column-start: 1, row-end: 4, column-end: 3
   ```

4. **Use the far edge.** In a grid whose column count may change, place a sidebar in the final two
   columns using negative line numbers.

5. **Line or span?** Write the cleanest rule for each requirement:
   ```text
   a) Start at column line 2 and end at line 5
   b) Start at column line 2 and occupy 3 columns
   c) Wherever auto-placement puts the item, occupy 2 rows
   ```

6. **Debug the swapped rectangle.** The intended area is rows 2-4 and columns 3-6, but this CSS draws
   the wrong shape. Correct it and name the ordering rule.
   ```css
   .hero { grid-area: 3 / 2 / 6 / 4; }
   ```

7. **Separate sequence from size.** Explain why this does not make the astronaut two columns wide,
   then add the missing declaration:
   ```css
   .astronaut { order: 1; }
   ```

8. **Build the EX 10.2 goal.** Given three grid items (`.cowboy`, `.astronaut`, `.book`) in a
   3-column x 2-row grid, write placement CSS so cowboy fills row 1 columns 1-2, astronaut fills row 2
   columns 1-2, and book fills column 3 across both rows.

9. **Intentional overlap.** Place `.panel-a` over rows 1-3 / columns 1-3 and `.panel-b` over rows 2-4 /
   columns 2-4. Add one property that guarantees `.panel-b` paints on top.

10. **Grid outside, Flexbox inside.** Write the minimum CSS needed to make each `.item` center its text
    horizontally and vertically without changing the grid container's track layout.

## Questions and Answers

11. A grid has 5 columns. How many vertical lines does it have, and why?

12. What does `grid-column: 2 / 5` mean? How many column tracks does it occupy?

13. What does `grid-column: 2 / span 3` mean, and how is that different from `2 / 3`?

14. What do `-1`, `-2`, and `-3` mean when used as grid line numbers?

15. State the four values accepted by `grid-area` in the correct order.

16. Can a `grid-column-end` value be smaller than `grid-column-start`? What area is selected?

17. What is Grid's default auto-placement direction for normal horizontal writing mode?

18. What does `order` change, and what three things does it **not** change?

19. Why is visual reordering with `order` an accessibility concern?

20. When two explicitly placed grid items overlap, what controls which one is visible on top?

## Self Assignments (No Answers)

21. Correct only the CSS in a copy of `exercise2.html` so it matches `goal2.png`. Do not inspect
    `solution2.html` until you have compared the result visually.

22. Rebuild all three EX 10.2 goals from blank HTML and CSS. For goal 3, create one version using
    `grid-row: span 2` and another using a four-value `grid-area`.

23. Build a dashboard with a header, sidebar, main panel, two small widgets, and footer. First place
    everything with line numbers; then refactor two shapes to use `span`.

24. Create two overlapping cards with Grid. Toggle `z-index` and source order in DevTools and write
    down which layer wins in each case.

25. Create a four-column grid and make the final item always fill the last two columns using negative
    lines. Change the template to six columns and confirm the rule still targets the far edge.

26. Draw a 5 x 4 grid on paper, number every line, and write five `grid-area` addresses. Translate each
    address into `grid-row` + `grid-column` longhand without looking at the notes.

27. Accessibility drill: build a row of three links, reverse them visually with `order`, then press
    Tab. Record the difference between the visual order and focus order and restore a logical DOM.

## Self-check

- [ ] I count grid lines instead of counting only cells.
- [ ] I can use positive and negative line numbers.
- [ ] I know when to use an end line and when to use `span`.
- [ ] I can write `grid-column`, `grid-row`, and `grid-area` from memory.
- [ ] I remember `grid-area` as row / column / row / column.
- [ ] I know `order` changes sequence but not size or explicit position.
- [ ] I can use Flexbox inside a grid item for centering.
- [ ] I corrected EX 10.2 exercise 2 myself.
