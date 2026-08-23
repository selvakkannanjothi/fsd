# Practice Tasks: EX 9.4 — Flexbox Pricing Table Project

Based on: `course_content/FLEXBOX/EX 9.4+Flexbox+Pricing+Table+Project/`
Notes: `.github/my_tasks/concepts/concept_pricing_table_project.md` · Hard copy: `flexbox_master_notes.pdf` (p8)

> ✅ **Built and corrected on 2026-08-23.** Final build matches the goal images at both widths.
> The two bugs that survived to the last round are Q1 and Q2 below — re-test yourself on those.

---

## Problem Statements (With Input Data)

1. **The 100vh trap.** A container is `display: flex; flex-direction: column; justify-content: center;
   height: 100vh;` and holds three cards that together need **895px**, in an **804px** window.
   ```
   a) What is the first card's top edge, relative to the top of the page?
   b) Can the user scroll to see it? Explain why or why not.
   c) Give TWO one-line fixes.
   ```

2. **The list that won't centre.** Inside a card with `text-align: center`, the feature list renders
   ~20px right of the title. The CSS says:
   ```css
   li { list-style-type: none; margin-bottom: 20px; padding: 0; }
   ```
   Name the property still in effect, say **which element** it's on, and write the fix.

3. **Fluid but capped.** Write the two declarations that make three cards share a row equally, stay fluid
   as the window resizes, but never exceed 400px each. Then say which flex-sizing step makes the second
   declaration win.

4. **Lean the media query.** Rewrite this so it only overrides what changes:
   ```css
   @media (max-width: 1250px) {
     .pricing-container {
       display: flex; flex-direction: column;
       justify-content: center; align-items: center;
       height: 100vh; gap: 2rem;
     }
   }
   ```

5. **Centre anything.** Write the three declarations that centre a single box in the exact middle of the
   screen, both axes. Which one do people forget, and what breaks without it?

6. **Unit audit.** For each, say whether it's valid and whether it's sensible:
   ```
   a) height: 100vh          d) max-width: 30vw
   b) max-width: 50vh        e) gap: 2rem
   c) max-width: 400px       f) padding: 2vh
   ```

7. **Pick the breakpoint.** The project uses `max-width: 1250px`. Three 400px cards + two 2rem gaps need
   how much room? Given that, is 1250px early, late, or about right — and what would you use instead?

8. **Debug by measurement.** You suspect a default browser style is breaking your layout but don't know
   which element owns it. Describe the exact DevTools steps to prove it in under 30 seconds.

## Questions and Answers

9. **Why is `min-height: 100vh` usually safer than `height: 100vh`?** When would you deliberately choose
   `height: 100vh` anyway?

10. **Why does centred overflow lose content that normal overflow doesn't?** Sketch where the overflow goes
    with `justify-content: flex-start` vs `center`.

11. **Which element carries a list's bullets, and which carries its indent?** Why does setting
    `list-style: none` on the `li` appear to work while `padding: 0` on the `li` does not?

12. **What does `flex: 1` expand to,** and why does adding `max-width: 400px` not conflict with it?

13. **`gap: 2rem` vs `gap: 32px`** — identical today. Name two situations where they diverge.

14. **`vh` vs `vw` vs `%`** — when is `%` the better choice than either viewport unit?

15. **The HTML already had `.plan-features` and `.plan-button` classes.** Give two concrete reasons to use
    them rather than bare `li` / `button` selectors.

16. **The whole responsive behaviour is one property.** Which one — and why is that the payoff of the
    entire Flexbox section?

## Self Assignments (No Answers)

17. Rebuild the pricing table **from the blank starter**, from memory, without opening `solution.html` or
    your finished `index.html`. Time it. Target: under 15 minutes.

18. Deliberately re-break it: put `height: 100vh` back in the media query, shrink the window until the top
    card is clipped, then confirm in DevTools that the container's height is smaller than its `scrollHeight`.
    Fix it again. **Feel the bug** so you recognise it in future projects.

19. Add a **4th** "Enterprise" card. Note what changes on its own (the flex ratio re-balances) and what you
    have to touch by hand (the breakpoint, probably).

20. Make the middle "Standard" card visually featured — say **1.5×** the width of the others — using only a
    flex property. Then make it keep that emphasis when stacked.

21. Convert the layout to `flex-wrap: wrap` with `flex: 1 1 300px` and **delete the media query entirely**.
    Compare the two approaches: which gives finer control, which is less code?

22. Swap `max-width: 400px` for `max-width: 30vw` and resize slowly. Describe in one sentence what feels
    different and why 400px was the better call for a card.

## Self-check

- [ ] I can explain why `height: 100vh` + `justify-content: center` hides content **above** the page.
- [ ] I know the list indent is the `<ul>`'s `padding-left: 40px`, not the `<li>`'s.
- [ ] I can write the `flex: 1` + `max-width` card pattern from memory.
- [ ] I can write the 3-line "centre anything" recipe from memory.
- [ ] I only override what changes inside a media query.
- [ ] I match units to axes — `vh` for height, `px`/`%`/`vw` for width.
- [ ] I use the classes the HTML already provides instead of bare element selectors.
- [ ] I rebuilt the project from the blank starter in under 15 minutes.
