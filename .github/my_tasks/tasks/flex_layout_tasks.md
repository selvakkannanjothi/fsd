# Practice Tasks: Flexbox — Flex Layout (Order, Wrap, Justify & Align)

Based on: `course_content/FLEXBOX/flexlayout_transcript.txt`
Notes: `.github/my_tasks/concepts/concept_flex_layout.md`

## Problem Statements (With Input Data)

1. **Reorder without touching the HTML.** Given this markup, write the CSS so the visual order reads
   Orange, Red, Yellow, Green (the HTML itself must NOT change):
   ```html
   <div class="rainbow">
     <div class="red">Red</div>
     <div class="orange">Orange</div>
     <div class="yellow">Yellow</div>
     <div class="green">Green</div>
   </div>
   ```

2. **Stop the overflow.** A row of 8 fixed-width `300px` cards inside a `.container` with
   `display: flex` overflows off the right edge of the screen on a narrow window. Write the one
   declaration that lets them flow onto additional lines instead, and name which element (parent or
   child) it goes on.

3. **Center a nav bar.** You have 5 nav links inside a `.container` that is `display: flex` and full
   page width. Write the CSS that bunches all 5 links together in the exact horizontal center of the bar.

4. **Match the gaps.** Three `100px` boxes sit inside a `600px`-wide flex container (so `300px` of extra
   space total). For each `justify-content` value below, describe where the gaps land:
   ```
   a) space-between
   b) space-around
   c) space-evenly
   ```

5. **Vertically center a logo.** A `.navbar` is `display: flex`, `height: 80px`, and contains a `40px`
   tall logo image plus some normal-height nav link text. Write the one declaration that vertically
   centers everything on the cross axis.

6. **One odd item out.** In a `.container` with `align-items: flex-start`, make just the 3rd child
   behave like `align-items: center` instead — without changing the container's own `align-items` value.

7. **Two-line spacing.** A wrapped flex container produces exactly 2 rows of items with empty vertical
   space left over. Write the CSS that pushes those 2 rows apart so there's equal space above, between,
   and below them (hint: two properties are needed — one to enable wrapping, one to space the lines).

8. **Debug it.** A developer sets `align-content: space-between` on a container but sees *no visual
   change at all*. List the two possible reasons this property might be doing nothing.

## Questions and Answers

9. **Does `order` go on the parent or the child?** What is every item's default `order` value, and what
   decides the visual order when several items share that same default?

10. **What's the difference between `flex-wrap: wrap` and `wrap-reverse`?**

11. **Which axis does `justify-content` control, and which does `align-items` control**, in a
    `flex-direction: row` container? What happens to both if you switch to `flex-direction: column`?

12. **`align-items: baseline` vs `align-items: flex-start`** — when do they look identical, and when do
    they visibly differ?

13. **What's the one-sentence difference between `align-items` and `align-content`?** What precondition
    must be true for `align-content` to have any visible effect at all?

14. **How does `align-self` relate to `align-items`?** Which element does each one go on?

15. **Why does `align-items` need the container to have an explicit height** (e.g. `70vh`) before you
    can actually see it working in a row-based Flexbox?

## Self Assignments (No Answers)

16. Build the 7-colour rainbow strip from the `EX 9.1`-style lesson and use `order` to rearrange it into
    reverse rainbow order (violet → red) without touching the HTML.

17. Build a responsive card gallery: 8 cards in a flex container with `flex-wrap: wrap`, and try all six
    `justify-content` values on the same markup, noting how each one changes the result.

18. Build a `70vh`-tall flex container with 5 items of different heights/padding and cycle through every
    `align-items` value, describing in your own words how each differs from `stretch` (the default).

19. Complete all levels of [Flexbox Froggy](https://appbrewery.github.io/flexboxfroggy/) on
    **Intermediate** difficulty (no directions shown) without dropping to Beginner.

20. Open the [flex-layout demo playground](https://appbrewery.github.io/flex-layout/) and force a
    situation where `align-content` visibly does something — then break it (stop it wrapping) and
    confirm `align-content` goes back to having zero effect.

## Self-check
- [ ] I know `order` and `align-self` are child properties; `flex-wrap`, `justify-content`,
      `align-items`, `align-content` are container properties.
- [ ] I can set `order` to move an item without changing the underlying HTML.
- [ ] I know `flex-wrap: nowrap` (default, no hyphen) vs `wrap` vs `wrap-reverse`.
- [ ] I can name all 6 `justify-content` values and roughly sketch their spacing.
- [ ] I can name all 5 `align-items` values and explain `baseline` vs `flex-start`.
- [ ] I can explain why `align-items` needs a container height to be visible.
- [ ] I can explain the difference between `align-items` and `align-content`, and `align-content`'s
      wrap-only precondition.
- [ ] I completed Flexbox Froggy on Intermediate difficulty.
