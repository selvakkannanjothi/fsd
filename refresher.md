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
