# Practice Tasks: EX 10.3 Mondrian Grid Project

Based on: `course_content/GRID/EX 10.3 Mondrian Project/`
Notes: `.github/my_tasks/concepts/concept_mondrian_project.md`

## Problem Statements (With Input Data)

1. **Track arithmetic.** Verify that this layout totals exactly `748px` on both axes:
   ```css
   grid-template-columns: 320px 198px 153px 50px;
   grid-template-rows: 414px 130px 155px 22px;
   gap: 9px;
   ```
   Show the sum of four tracks plus three gaps for each axis.

2. **Find the two-pixel bug.** Repeat the height calculation with the final row set to `20px`. Explain
   why a fixed `height: 748px` no longer matches the explicit track system.

3. **Paint the lines.** Write the minimum container/item CSS that creates `9px` black seams between
   off-white grid items without borders on every item.

4. **Place four merged regions.** Using only the requirements below, write the cleanest rules:
   ```text
   white1: row 1, final three columns
   white2: first column, rows 2 and 3
   white3: rows 2-3 and columns 2-3
   white4: final column, rows 3 and 4
   ```

5. **Decode the project area.** Explain the exact tracks covered by:
   ```css
   .white3 { grid-area: 2 / 2 / 4 / 4; }
   ```

6. **Border ownership.** The blue panel needs a normal `9px` seam plus an additional `10px` black line
   under the blue paint. Which black area comes from the container and which comes from the item?

7. **Center safely.** Write the body rule that centers the 748px artwork in both axes and still allows
   the page to grow/scroll if content later becomes taller than the viewport.

8. **Refactor repetition.** Several white panels repeat `background-color: #F0F1EC`. Refactor them to
   a shared `.item` rule while keeping colour overrides for red, blue, yellow, and black.

9. **Choose the layout tool.** Explain why Grid should create the painting and Flexbox should center
   the completed painting. What would become harder if their jobs were reversed?

10. **Audit the local attempt.** Without editing `course_content/`, copy the Mondrian `index.html` to a
    practice folder, fix the final row and body centering, and compare it pixel-for-pixel with `goal.png`.

## Questions and Answers

11. Why does the painting need four columns even though the top appears to have only two large blocks?

12. Why can a CSS grid line not simply receive `background-color: black`?

13. How does `gap` reveal the grid container's background?

14. Why is "one div per visual region" a useful starting model for this project?

15. When is `span` clearer than `grid-area`, and when is `grid-area` clearer than `span`?

16. What is the correct four-value order for `grid-area`?

17. What box-model feature creates the special line under the blue panel?

18. Why should colours usually be applied after the geometry matches?

19. Which DevTools Grid overlay option lets you verify exact computed track sizes?

20. State the complete design-to-grid workflow in five or more steps.

## Self Assignments (No Answers)

21. Complete the local Mondrian project yourself from a blank file using only `dimensions.png`. Check
    `solution.html` only after your screenshot matches the goal.

22. Rebuild the same painting using named grid areas. Compare the readability and amount of CSS with
    the numeric-line version.

23. Choose another Mondrian composition, draw its grid boundaries on paper, estimate every track, and
    recreate it with Grid. Use CSS custom properties for the colour palette.

24. Make the 748px project responsive: preserve the same proportions inside a square whose width is
    `min(90vw, 748px)`. Record which fixed-pixel details need rethinking.

25. Add an on-page toggle that shows/hides grid line numbers or labels each painted region. Do not
    change the visual output when the debug mode is off.

26. Print the finished artwork to PDF and compare its proportions against the reference image at high
    zoom. Correct every visible seam or two-pixel mismatch.

27. Create a second version that uses borders instead of a black container plus `gap`. Compare the
    CSS complexity and identify edge/double-border problems.

## Self-check

- [ ] I derive tracks from every visible boundary before writing placement rules.
- [ ] I can prove that tracks + gaps equal the 748px frame.
- [ ] I know the black seams belong to the grid container background.
- [ ] I can mix `span` and `grid-area` intentionally.
- [ ] I use Grid for the artwork and Flexbox for viewport centering.
- [ ] I fixed the local project's centering and 22px final row myself.
- [ ] My final output matches `goal.png` at pixel level.
