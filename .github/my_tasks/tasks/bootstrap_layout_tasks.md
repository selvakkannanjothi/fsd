# Practice Tasks: Bootstrap — The 12-Column Layout System

Based on: `course_content/11.0 Bootstrap/11.0_bootstrap_layout.txt`
Exercise site: <https://appbrewery.github.io/bootstrap-layout/>
Notes: `.github/my_tasks/concepts/concept_bootstrap_layout.md`

Breakpoint ladder to keep beside you while answering:
*(none)* `<576` · `sm ≥576` · `md ≥768` · `lg ≥992` · `xl ≥1200` · `xxl ≥1400`

---

## Problem Statements (With Input Data)

1. **Read the skeleton.** What is wrong with this markup, and what will it actually render as?
   ```html
   <div class="container">
     <div class="col-6">Left</div>
     <div class="col-6">Right</div>
   </div>
   ```

2. **Bare `col` division.** A `.row` holds five divs, each `class="col"`. What percentage of the row
   does each take? Now a sixth is added. What does each take? What CSS declaration on `.col` is
   producing this, and which flex-sizing scenario from `concept_flex_sizing.md` is it?

3. **Adds up to more than 12.** Predict the rendered layout, and say *why* the columns do not simply
   squash to fit.
   ```html
   <div class="row">
     <div class="col-8">A</div>
     <div class="col-6">B</div>
   </div>
   ```

4. **Container variants.** For each class below, state the rendered width at a viewport of **500px**,
   **800px**, and **1300px**. (Container caps: 540 / 720 / 960 / 1140 / 1320.)
   a) `container`  b) `container-md`  c) `container-xl`  d) `container-fluid`

5. **Which container?** Pick the right class and justify it in one line each:
   a) A hero image banner that must touch both edges of the screen at every size.
   b) A blog article body that should always have comfortable margins left and right.
   c) A dashboard that should be edge-to-edge on phones and tablets, but gain margins on laptops up.

6. **Direction check.** A div has `class="col-md-4"` and nothing else. State its width (in twelfths)
   at each of: 400px, 700px, 900px, 1300px, 1600px. Explain the value at 400px and the value at 1600px
   in terms of the `min-width` rule.

7. **Stacked breakpoints.** Give the width in twelfths at 400 / 700 / 900 / 1100 / 1300 / 1500px:
   ```html
   <div class="col-sm-12 col-md-8 col-lg-4">…</div>
   ```

8. **Mix sized and unsized.** What width does the third div get, and which CSS declaration makes that
   happen?
   ```html
   <div class="row">
     <div class="col-3">A</div>
     <div class="col-2">B</div>
     <div class="col">C</div>
   </div>
   ```

9. **⚠️ The leak trap (the big one — see §9 of the notes).** Target behaviour: Column 1 is **10/12 on
   extra small**, **12/12 on small and medium**, **6/12 on large and up**.
   ```html
   <div class="col-10 col-lg-6">Column 1</div>
   ```
   a) What does this actually render at 700px?
   b) Why — which rule is still in force at that width, and why does `col-lg-6` not help?
   c) Fix it with one added class.
   d) Column 2 in the same exercise is written `col-10 col-sm-6 col-lg-3` and has no such bug.
      Why does it escape?

10. **Redundant or required?** For each, say whether `col-sm-12` can be deleted without changing
    anything, and why:
    a) `<div class="col-sm-12 col-xl-6">`
    b) `<div class="col-10 col-sm-12 col-lg-6">`
    c) `<div class="col-sm-12 col-md-6">`

11. **Specificity or source order?** `.col-sm-12` and `.col-lg-4` are on the same div. At 1100px the
    div is 4/12 wide. Is that because `.col-lg-4` is more specific? Calculate both specificities and
    give the real reason. Which cascade rule from `concept_css.md` is doing the work?

12. **Measure-to-class.** You measure a demo box and its row with DevTools and get: box `293px`,
    row `1172px`. Which `col-N` class is it? Show the arithmetic.

13. **Reverse-engineer from a table.** You measured a demo div across the bands and got the twelfths
    below. Write the complete `class="…"` attribute, using the fewest classes possible.
    | Band | xs | sm | md | lg | xl | xxl |
    | --- | --- | --- | --- | --- | --- | --- |
    | width | 12 | 12 | 6 | 4 | 4 | 3 |

14. **Boundary precision.** Bootstrap's small breakpoint is `min-width: 576px`. At a viewport of
    exactly **576px**, is `col-sm-6` active or not? What about at exactly **575px**? What does that
    tell you about whether the boundary is inclusive?

15. **Translate away Bootstrap.** Write the plain CSS (media queries and all) that reproduces this,
    with no Bootstrap:
    ```html
    <div class="row">
      <div class="col-12 col-md-6">A</div>
      <div class="col-12 col-md-6">B</div>
    </div>
    ```
    Then say in one sentence what Bootstrap bought you here.

---

## Questions and Answers

**Q1. Why 12 columns and not 10 or 16?**
12 divides evenly by 1, 2, 3, 4, 6 and 12 — so halves, thirds, quarters and sixths are all whole
numbers. 10 cannot give you thirds; 16 cannot give thirds either. 12 is the smallest number that
covers the layout splits designers actually use.

**Q2. What are the three required pieces of a Bootstrap layout, in order?**
`container` (overall width + side margins) → `row` (one horizontal band, and the thing the 12 columns
are counted within) → `col` (the items). Your content goes inside the `col`, never directly in the
`row`.

**Q3. What does bare `col` (no number) do?**
Splits the row equally between however many there are. Three `col`s → thirds; six → sixths. It is
`flex: 1 0 0%` — grow 1, shrink 0, **basis 0** — which is the "share everything equally" case from
the flex-sizing lesson.

**Q4. `container` vs `container-fluid`?**
`container` is capped (540 / 720 / 960 / 1140 / 1320px) so there is always a margin down each side.
`container-fluid` is always 100% wide, edge to edge. These are the two you will reach for most.

**Q5. What does `container-lg` actually mean?**
"Be 100% wide **until** 992px, then behave like a normal container (960 → 1140 → 1320)." The name is
the width at which it **stops** being full-width. Mechanically, `.container-lg` simply doesn't appear
in Bootstrap's `max-width` rules until the `min-width: 992px` media query.

**Q6. Is `container-sm` different from `container`?**
No — identical. `.container-sm` joins the max-width list at the very first breakpoint (576px), which
is exactly where `.container` starts being capped too. The transcript says this explicitly.

**Q7. Does `col-sm-6` mean "6 columns on small screens only"?**
No, and this is the single most common misreading. It means **"6 columns from 576px upward"** —
mobile, tablet, laptop, desktop and TV, unless a larger breakpoint overrides it. Every Bootstrap
breakpoint is a `min-width` media query. **Breakpoints go up, never down.**

**Q8. Why does extra small have no letters in the class name?**
It is the bottom of the ladder, so there is no `min-width` to name. `col-4` *is* the extra-small
class — and, because it has no upper bound, it applies at every width above too.

**Q9. What happens if my `col-*` numbers add up to more than 12?**
The overflow wraps onto a new line. It does not squash, because `.row > *` sets `flex-shrink: 0`.
That is also the tell for a bug: if a row unexpectedly became two rows, add your numbers up.

**Q10. Why is a class-less `<div>` inside a `.row` already full width?**
Because `.row > * { width: 100%; max-width: 100% }` — Bootstrap sets it directly. It is not a special
grid rule; it is one CSS declaration on the universal child selector.

**Q11. In `col-sm-12 col-md-8 col-lg-4`, why does `col-lg-4` win at 1200px?**
Source order, not specificity. Both are a single class = `(0,1,0)` — a perfect tie. Bootstrap writes
its media queries smallest-first, so `.col-lg-4` is physically later in the stylesheet and wins the
tie. This is cascade rule 1 from `concept_css.md`: *position — lower wins*.

**Q12. What is "mobile-first" in one sentence?**
Describe the smallest screen first, then add classes that override it upward — which works precisely
because Bootstrap's file is ordered smallest-first, so bigger breakpoints always come later.

**Q13. ⚠️ Why does `<div class="col-10 col-lg-6">` render as 10/12 at 700px instead of 12/12?**
`col-10` has no infix, so it applies from 0px **upward with no ceiling**. At 700px (the `sm` band),
`col-lg-6` has not kicked in yet — so nothing has overridden `col-10`, and it is still in force.
Measured on the exercise page: 10/12. Fix: add `col-sm-12`. **There is no "unset" in Bootstrap's
grid, only "override."**

**Q14. So is `col-sm-12` redundant or not?**
It depends entirely on what else is on the div. Redundant when nothing smaller is set (the default is
already full width). **Required** the moment a no-infix `col-N` is present, because that value would
otherwise leak upward through `sm` and `md`.

**Q15. How do I find which breakpoint a layout jump happened at?**
The instructor's tip: DevTools → toggle the device toolbar → set to *Responsive* → drag the handle and
watch the width readout at the top. The width shown when the layout snaps is the breakpoint. The
precise version: measure the box, divide by the row width, multiply by 12 — that turns "looks about
half" into an exact number.

**Q16. Do Bootstrap breakpoints replace media queries entirely?**
For *layout*, mostly yes. But responsive font sizes, background images, off-scale spacing, and any
breakpoint at a width Bootstrap doesn't ship still need your own media query. The skill is used less,
not retired.

**Q17. Is Bootstrap's grid the same as CSS Grid?**
No. Despite the name, `.row` is `display: flex; flex-wrap: wrap` — it is **Flexbox** with the CSS
pre-written. Only `.row > *` sets widths; there are no grid tracks, lines or areas involved.

**Q18. What were the answers to the three exercises?**
- **Ex 1:** `col-xl-6` on both divs. (`col-sm-12` optional — genuinely redundant here.)
- **Ex 2:** `col-10 col-sm-12 col-lg-6` / `col-10 col-sm-6 col-lg-3` / `col-10 col-sm-6 col-lg-3`.
- **Ex 3:** `col-md-6 col-lg-4 col-xl-2 col-xxl-1` / `col-md-6 col-lg-8 col-xl-10 col-xxl-11`.
All three verified against the demo rows at six viewport widths — 18/18 exact matches.

---

## Self Assignments (No Answers)

1. **Redo the site cold.** Go back to <https://appbrewery.github.io/bootstrap-layout/>, refresh so the
   textareas reset, and solve all three from scratch **without** looking at §8 of the notes. Use the
   DevTools responsive ruler, not the answers. Time yourself.

2. **Prove the trap to yourself.** In Exercise 2, delete `col-sm-12` from Column 1, hit *Apply
   Changes*, and drag the window down through the `sm` band until you can *see* the 10/12. Then put it
   back. Do not skip the seeing-it part — this is the one thing the video gets wrong.

3. **Build the container ladder page.** One HTML file, six stacked `<div>`s, one per container variant,
   each labelled with its own class name and given a visible background colour. Open it and drag the
   window from 400px to 1500px. Write down, from what you observe, the width at which each one stops
   being full-width. Check against §3 of the notes afterwards.

4. **Rebuild the pricing table with Bootstrap.** Take `EX 9.4 Flexbox Pricing Table` and rebuild the
   layout using `container` / `row` / `col-*` only. Target: three cards side by side on `lg` and up,
   stacked full width below `md`. Delete your `flex-direction: column` media query and get the same
   behaviour from classes alone. Then write two sentences: what got shorter, and what got worse.

5. **Classic app shell.** Build a page with a `container-fluid` nav bar across the top, then a
   `container` holding one row with a 3/12 sidebar and a 9/12 main area. On tablet, make the sidebar
   4/12. On mobile, stack them full width. No custom CSS for the layout — classes only.

6. **Twelfths flash-drill.** Write out `col-1` through `col-12` and next to each the percentage it
   represents, to one decimal place. Then cover the percentages and recite them. Then cover the class
   names and go the other way. Repeat until both directions are instant.

7. **Reverse-engineer a real site.** Open any Bootstrap-built site, inspect a section, and write down
   the full class list on one column div. Predict its width at each of the six bands, then verify by
   resizing. (Search for `col-` in DevTools' Elements search to find one fast.)

8. **Translate both ways.** Take one row from Self Assignment 5 and write the equivalent plain CSS,
   media queries included. Then take the Mondrian project's first row and try to express it in
   Bootstrap columns. Which one fought back, and what does that tell you about when Bootstrap's grid
   is the wrong tool?
