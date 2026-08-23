# Practice Tasks: Flexbox — Flex Sizing (`flex-grow` / `flex-shrink` / `flex-basis`)

Based on: lesson `9. Flexbox → 57. Flex Sizing`
Notes: `.github/my_tasks/concepts/concept_flex_sizing.md` · Hard copy: `flexbox_master_notes.pdf`

> ⚠️ **Weak area.** Do the "Rapid fire" section below every revision — target: all 12 in under 3 minutes.

---

## Rapid fire (say the final width out loud, then check §Quick self-check in the notes)

| # | Setup | Your answer |
|---|---|---|
| R1 | `width: 300px; flex-basis: 100px;` in a row container | |
| R2 | `flex-basis: 200px; max-width: 100px;` | |
| R3 | `flex-basis: 50px; max-width: 200px;` | |
| R4 | `flex-basis: 200px; min-width: 300px;` | |
| R5 | `flex-basis: 400px; min-width: 300px;` | |
| R6 | `flex-basis: 400px; max-width: 300px;` | |
| R7 | `min-width: 300px; max-width: 100px;` | |
| R8 | `flex: 0 0 100px;` — window shrunk to 50px | |
| R9 | `flex: 1 0 100px;` — window shrunk to 50px | |
| R10 | `flex: 0 1 100px;` — window widened to 2000px | |
| R11 | `flex: 2` — write the three longhand values | |
| R12 | `flex: 1` / `flex: 2` / `flex: 3` in a 600px row | |

---

## Problem Statements (With Input Data)

1. **Three-column split.** Make these three boxes take up the full width of the container in a strict
   **1 : 3 : 2** ratio, using the shortest CSS possible:
   ```html
   <div class="row">
     <div class="a">A</div>
     <div class="b">B</div>
     <div class="c">C</div>
   </div>
   ```
   Then answer: in a **900px** container, what pixel width does each box get?

2. **Fixed sidebar, fluid content.** Build a page shell where `.sidebar` is **always exactly 250px**
   (never grows, never shrinks) and `.content` takes every remaining pixel. Write the CSS for both.

3. **Equal columns vs content columns.** Given two items — one containing the word `Hi` and one
   containing a 12-word sentence — write the CSS that makes them:
   ```
   a) exactly equal in width, ignoring their content
   b) sized so the long sentence gets the bigger share
   ```
   Both answers are one declaration each, and they differ by a single value.

4. **Predict the four behaviours.** For each block below, state (i) can the item grow? (ii) can it
   shrink? (iii) what is the allowed width range, and (iv) what role does the `100px` play?
   ```css
   a) flex: 0 0 100px;
   b) flex: 1 0 100px;
   c) flex: 0 1 100px;
   d) flex: 1 1 100px;
   ```
   Then: **which one is Flexbox's default behaviour when you write nothing at all?**

5. **The clamping order.** An item has `flex-basis: 100px; flex-grow: 1; max-width: 300px;` inside a
   1000px container with two other identical items. Walk through the browser's 5 steps and give the
   final width of each item. Where does the leftover space end up?

6. **Debug it — the item won't shrink.** A card containing a long URL sits in a `flex: 1` column inside
   a narrow container. The text spills out of the box and a `text-overflow: ellipsis` rule is doing
   nothing. Name the invisible property causing it, and write the one-line fix.

7. **Debug it — the columns aren't equal.** A developer writes `flex-grow: 1` on all three children and
   is confused that the widest-content column is still wider than the others. Explain why, and give the
   one-word change that fixes it.

8. **Responsive card grid.** Write the CSS for a card gallery where each card is **at least 250px** wide,
   grows to share any leftover space, and wraps onto new lines when there isn't room. Three declarations
   on the container, one on the cards.

9. **Do the maths.** A `600px` flex container has `gap: 20px` and three items, each `flex: 1 1 100px`.
   How much free space is actually distributed, and what is each item's final width?

10. **Shrink weighting.** Two items — `flex: 0 1 200px` and `flex: 0 1 400px` (both `min-width: 0`) —
    sit in a `300px` container. Their final widths are **100px** and **200px**, not 50px and 250px.
    Explain the formula that produces this.

## Questions and Answers

11. **Recite the priority ladder** from weakest to strongest: content width, `width`, `flex-basis`,
    `min-width`/`max-width`. Which one is applied *last* by the browser, and why does that matter?

12. **If an item has both `width` and `flex-basis`, which is used?** Does your answer change in a
    `flex-direction: column` container?

13. **Why is `max-width` described as "a limit, not a target"?** Give an example where `max-width: 200px`
    results in a 50px-wide element.

14. **What are the default values** of `flex-grow`, `flex-shrink` and `flex-basis`? Say the default in
    one plain-English sentence.

15. **Expand these shorthands:** `flex: 1`, `flex: 2`, `flex: auto`, `flex: none`, `flex: initial`.
    Which one is a trick you're likely to get wrong?

16. **Why do `flex-grow: 1` and `flex: 1` behave differently** even though both set grow to 1?

17. **`flex-basis: auto` vs `flex-basis: 0`** — describe the difference using a container holding one
    single word and one long sentence.

18. **Are `flex-grow: 3` and `flex-grow: 300` different?** Explain what the number really represents.

19. **Why is `flex-shrink` weighted by `flex-basis` while `flex-grow` isn't?** Give the intuition in one
    sentence.

20. **What is `min-width: auto` on a flex item**, and why is it the single most common flexbox bug?

## Self Assignments (No Answers)

21. Build a 3-column layout and cycle every child through `flex: 1`, `flex: 2`, `flex: 3`, `flex: none`
    and `flex: 0 0 200px` — screenshot each and write one line describing what changed.

22. Recreate the **gs-1 → gs-4** table from the notes as a live HTML page: four rows, each with the same
    `flex-basis: 100px` but different grow/shrink pairs. Resize the browser window slowly and confirm
    each row behaves exactly as the table predicts.

23. Build the **Flexbox Pricing Table project** (`course_content/FLEXBOX/9.4+Flexbox+Pricing+Table+Project`)
    from `goal-large.png` / `goal-small.png` without opening `solution.html`.

24. Take one existing project (Web Design Agency or the portfolio) and convert any leftover
    `width: X%` layout rules to `flex` shorthand. Note which ones got *simpler*.

25. Deliberately break it: put a 40-character unbreakable word inside a narrow `flex: 1` box, watch it
    overflow, then fix it with `min-width: 0`. Do the same with an oversized image.

26. Open DevTools on any site you like, find a flex container (the `flex` badge in the Elements panel),
    and read off the computed `flex-grow` / `flex-shrink` / `flex-basis` of three of its children.

## Self-check

- [ ] I can recite the priority ladder: content width < `width` < `flex-basis` < `min`/`max-width`.
- [ ] I know clamping (`min`/`max-width`) happens **last**, after grow/shrink resolve.
- [ ] I can answer all 12 rapid-fire rows in under 3 minutes without looking.
- [ ] I know `flex: 0 1 auto` is the default — **shrink yes, grow no**.
- [ ] I can expand `flex: 1`, `flex: 2`, `flex: auto`, `flex: none`, `flex: initial` correctly.
- [ ] I know `flex: 2` = `2 1 0%`, **not** `2 2 0`.
- [ ] I can explain why `flex-grow: 1` ≠ `flex: 1`.
- [ ] I can explain `flex-basis: auto` vs `0` with the "one word vs one sentence" example.
- [ ] I know grow/shrink are **ratios**, and can compute 1:2:3 in a 600px container.
- [ ] I know `min-width: auto` is the hidden shrink floor, and `min-width: 0` is the fix.
- [ ] I built the Pricing Table project unaided.
