# FSD Quiz Memory

This file is the persistent store for the FSD self-quiz. It is NOT study notes.

## Quiz Rules (always follow)
- Questions are drawn from all covered topics (see `AGENTS.md` progress tracker / `course_content/`).
- Difficulty mix per quiz: **Easy < 30%**, **Medium ~20%**, **Difficult > 50%**.
- Every question has **exactly 4 options**, and all distractors must be **close/plausible** to the correct answer (no obvious throwaways).
- Every question answered **wrong** is logged in the "Wrong Questions Bank" below.
- Wrong questions **must be repeated** in subsequent quizzes until answered correctly. Once answered correctly, mark it resolved (move to "Resolved" or strike through) so it stops repeating.

## Config
- Questions per quiz: **Ask the user at the start of each quiz.**
- Delivery: **One question at a time** (ask, wait for answer, then next).
- Show answers: **After each question** (immediate feedback + explanation on a miss).

---

## Wrong Questions Bank (repeat these next quiz)

### WQ1 · 🔴 Difficult · Topic: CSS Cascade
**Q:** The CSS cascade resolves conflicts by checking criteria in a specific order. Which sequence is correct (first-checked → last-checked)?
- A. Specificity → Position → Importance → Type
- B. Position → Specificity → Type → Importance
- C. Importance → Specificity → Type → Position
- D. Type → Specificity → Position → Importance
**Correct:** B — Position → Specificity → Type → Importance
**Missed on:** Quiz 1 (answered "don't know")

### WQ2 · 🔴 Difficult · Topic: CSS Specificity
**Q:** Given `p { color: green } .note { color: blue } #intro { color: orange }` applied to `<p id="intro" class="note">`, which color wins and why?
- A. green — the element selector is most specific
- B. blue — the class selector wins
- C. orange — the ID selector has the highest specificity
- D. blue — the last rule declared always wins
**Correct:** C — ID has the highest specificity (ID > class > element)
**Missed on:** Quiz 1 (guessed correctly but requested to bank for reinforcement)

### WQ3 · 🔴 Difficult · Topic: CSS Positioning
**Q:** An element has `position: absolute`. What is it positioned relative to?
- A. The browser window (viewport)
- B. Its nearest ancestor that has a `position` other than `static`
- C. Its immediate parent element, always
- D. Its own normal position in the document flow
**Correct:** B — nearest positioned ancestor (else falls back to page/viewport). A = fixed, D = relative.
**Missed on:** Quiz 1 (guessed correctly but requested to bank for reinforcement)

### WQ4 · 🔴 Difficult · Topic: CSS Units (em/rem)
**Q:** `font-size: 2em` on a `<p>` whose parent `<div>` is `20px`. Computed size, and em vs rem?
- A. 32px — em is relative to the root <html> element
- B. 40px — em is relative to the parent element; rem would be relative to the root
- C. 40px — em and rem both scale from the root identically
- D. 2px — em is an absolute unit like px
**Correct:** B — 2em × 20px = 40px; em = parent-relative, rem = root-relative
**Missed on:** Quiz 1 (guessed correctly but requested to bank for reinforcement)

### WQ5 · 🔴 Difficult · Topic: Flexbox Sizing — flex-basis vs max-width ⚠️ SELF-FLAGGED WEAK AREA
**Q:** A flex item has `flex-basis: 200px; max-width: 100px;` (no grow/shrink in play). What is its final width?
- A. 200px — `flex-basis` is a flex property, so it overrides `max-width`
- B. 100px — `max-width` is a hard ceiling applied after `flex-basis` is resolved
- C. 300px — the two values are added together
- D. 150px — the browser averages the requested size and the limit
**Correct:** B — the browser sizes from `flex-basis` first, then clamps; `200px` breaks the ceiling so `flex-basis` is overruled → **100px**
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ6 · 🔴 Difficult · Topic: Flexbox Sizing — flex-basis vs max-width ⚠️ SELF-FLAGGED WEAK AREA
**Q:** A flex item has `flex-basis: 50px; max-width: 200px;` (no grow/shrink in play). What is its final width?
- A. 200px — `max-width` stretches the item up to its stated limit
- B. 125px — the item settles halfway between the basis and the limit
- C. 50px — `flex-basis` is within the ceiling, so `max-width` never kicks in
- D. 0px — the two rules conflict and cancel each other out
**Correct:** C — `max-width` is only a limit, never a target; the basis respects it, so `flex-basis` wins → **50px**
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ7 · 🔴 Difficult · Topic: Flexbox Sizing — flex-basis vs min-width ⚠️ SELF-FLAGGED WEAK AREA
**Q:** A flex item has `flex-basis: 200px; min-width: 300px;` (no grow/shrink in play). What is its final width?
- A. 200px — `flex-basis` is the explicit request, so it wins
- B. 300px — `min-width` is a hard floor applied after `flex-basis` is resolved
- C. 250px — the item settles between the request and the floor
- D. 500px — the floor is added on top of the basis
**Correct:** B — the basis **breaks** the floor, so it is overruled and clamped **up** → **300px**
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ8 · 🔴 Difficult · Topic: Flexbox Sizing — flex-basis vs min-width ⚠️ SELF-FLAGGED WEAK AREA
**Q:** A flex item has `flex-basis: 400px; min-width: 300px;` (no grow/shrink in play). What is its final width?
- A. 300px — `min-width` always overrides `flex-basis`
- B. 350px — the browser averages the two values
- C. 400px — the basis is already above the floor, so `min-width` never kicks in
- D. 700px — the two values stack
**Correct:** C — a floor is a limit, not a target; the basis respects it, so `flex-basis` wins → **400px**. (Swap the floor for `max-width: 300px` and the answer flips to **300px**.)
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ9 · 🔴 Difficult · Topic: Flexbox Sizing — the `flex` shorthand ⚠️ SELF-FLAGGED WEAK AREA
**Q:** What does `flex: 2` expand to in longhand?
- A. `flex-grow: 2; flex-shrink: 2; flex-basis: 0;`
- B. `flex-grow: 2; flex-shrink: 1; flex-basis: 0%;`
- C. `flex-grow: 2; flex-shrink: 1; flex-basis: auto;`
- D. `flex-grow: 0; flex-shrink: 2; flex-basis: 2px;`
**Correct:** B — a single number sets **`flex-grow` only**; `flex-shrink` stays at its default `1` and `flex-basis` becomes `0%`
**Missed on:** Self-flagged (originally noted as `2 2 0`)

### WQ10 · 🔴 Difficult · Topic: Flexbox Sizing — longhand vs shorthand ⚠️ SELF-FLAGGED WEAK AREA
**Q:** Container A's children have `flex-grow: 1`. Container B's children have `flex: 1`. Both hold one short word and one long sentence. Why aren't the results identical?
- A. They are identical — `flex: 1` is just shorthand for `flex-grow: 1`
- B. `flex: 1` also sets `flex-basis: 0%`, so widths become equal; `flex-grow: 1` leaves the basis at `auto`, so the longer content stays wider
- C. `flex-grow: 1` also sets `flex-shrink: 0`, which blocks shrinking
- D. `flex: 1` only works when `flex-wrap: wrap` is set
**Correct:** B — the shorthand resets any omitted `flex-basis` to `0`, the longhand doesn't (verified in Chrome: 300/300 vs 182/418)
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ11 · 🔴 Difficult · Topic: Flexbox Sizing — default behaviour ⚠️ SELF-FLAGGED WEAK AREA
**Q:** You write `display: flex` on a container and nothing else. What are the children's effective flex values, and what does that mean?
- A. `flex: 1 1 auto` — they grow and shrink freely
- B. `flex: 0 1 auto` — they may **shrink** but will **not grow** to fill the row
- C. `flex: 1 0 auto` — they grow but never shrink
- D. `flex: 0 0 auto` — they are completely rigid
**Correct:** B — `flex: initial` = `0 1 auto`. Shrink yes, grow no. That's why a flex row squeezes on a narrow window but never spreads out on a wide one.
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ12 · 🔴 Difficult · Topic: Flexbox Sizing — grow/shrink scenarios ⚠️ SELF-FLAGGED WEAK AREA
**Q:** An item is `flex: 1 0 100px`. The window is dragged very narrow, then very wide. What is its width range?
- A. Always exactly 100px — the basis is fixed
- B. `min-content → 100px` — it can shrink but not grow
- C. `100px → whatever space is available` — 100px acts as a **floor**
- D. `0 → 100px` — it collapses when there's no room
**Correct:** C — `flex-shrink: 0` blocks shrinking so 100px is the minimum; `flex-grow: 1` lets it expand freely. (Flip the two numbers, `flex: 0 1 100px`, and 100px becomes the **ceiling** instead — that's the default behaviour.)
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ13 · 🔴 Difficult · Topic: Flexbox Sizing — the priority ladder ⚠️ SELF-FLAGGED WEAK AREA
**Q:** Order these from **weakest to strongest** when a flex item's main-axis size is decided: `flex-basis`, `min-width`/`max-width`, content width, `width`.
- A. `width` → content width → `flex-basis` → `min`/`max-width`
- B. content width → `width` → `flex-basis` → `min`/`max-width`
- C. content width → `flex-basis` → `width` → `min`/`max-width`
- D. `min`/`max-width` → `flex-basis` → `width` → content width
**Correct:** B — content width < `width` < `flex-basis` < `min`/`max-width`. The clamp is applied **last**, which is exactly why it always wins.
**Missed on:** Self-flagged as a weak area (not yet quizzed)

### WQ14 · 🔴 Difficult · Topic: Flexbox Sizing — the hidden shrink floor ⚠️ SELF-FLAGGED WEAK AREA
**Q:** A `flex: 1` box containing one very long unbreakable word refuses to shrink below ~190px, and `text-overflow: ellipsis` does nothing. Why, and what's the fix?
- A. `flex-shrink` defaults to `0`, so it can't shrink — set `flex-shrink: 1`
- B. Flex items have an implicit `min-width: auto` (= min-content size) that shrinking can't cross — set `min-width: 0` (or `overflow: hidden`)
- C. `flex-basis: 0` is missing — add it
- D. The container needs `flex-wrap: wrap`
**Correct:** B — the automatic minimum size. `min-width: 0` unlocks it (verified: 190px → 100px). This is the single most common flexbox bug in real code.
**Missed on:** Self-flagged as a weak area (not yet quizzed)

---

## Resolved (previously wrong, now answered correctly)
_(empty)_

---

## Quiz History

### Quiz 1
- Length: 10 questions (2 easy / 2 medium / 6 difficult)
- Score: 9/10 correct (1 genuine miss: WQ1 cascade order)
- Banked: WQ1 (missed), WQ2/WQ3/WQ4 (guessed correctly, banked on user request)
- Correct & confident: Q1 DNS, Q2 void element, Q3 external CSS link, Q4 box model order, Q9 combinators, Q10 inline-block
