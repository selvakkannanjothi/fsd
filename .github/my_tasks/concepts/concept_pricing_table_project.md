# EX 9.4 — Flexbox Pricing Table Project (section capstone)

Source: `course_content/FLEXBOX/EX 9.4+Flexbox+Pricing+Table+Project/`
(`transcript.txt` · `index.html` = my build · `solution.html` = course version · `goal-large.png` / `goal-small.png`)
My iteration log: `pricing_table_review_notes.txt` (submissions #1 and #2 + the CSS-units Q&A)

---

## The brief

Three pricing cards. **The only hard requirement is the Flexbox part:**

1. Cards sit in a flex row and **adapt their width** to the space available.
2. Below a breakpoint they **stack vertically** — done with a **media query + `flex-direction: column`**.

Everything else (colours, radius, fonts) is personal preference. The starter file gave you all the HTML,
the `Sono` Google font, and an **empty** `@media (max-width: 1250px) { }` block as the hint.

---

## The whole project is 4 ideas stacked

```css
/* 1 — the "cheat code" for perfect centring, both axes at once */
.pricing-container {
  display: flex;
  justify-content: center;   /* main axis  — horizontal */
  align-items: center;       /* cross axis — vertical   */
  height: 100vh;             /* ← align-items needs height to work against */
  gap: 2rem;
}

/* 2 — fluid but capped: THE professional card pattern */
.pricing-plan {
  flex: 1;             /* = 1 1 0%  → three equal, fluid cards      */
  max-width: 400px;    /* ceiling   → they stop before going silly  */
}

/* 3 — kill the list's bullets AND its indent (both live on the <ul>) */
.plan-features { list-style: none; padding: 0; margin: 0; }

/* 4 — the responsive switch: one line does the real work */
@media (max-width: 1250px) {
  .pricing-container {
    flex-direction: column;
    height: 100%;      /* ← and this line stops it breaking. See §Trap 1 */
  }
}
```

> 🔑 **`flex: 1` + `max-width`** is the pattern to memorise. `flex: 1` says *"share the row equally and stay
> fluid"*; `max-width` says *"…but never get wider than this."* Fluid **and** capped. Straight out of the
> flex-sizing lesson: the basis/grow result gets **clamped** by `max-width` at the end.

> 🔑 **The centring cheat code.** `justify-content: center` + `align-items: center` + a `height` on the
> container centres anything vertically *and* horizontally. Before Flexbox this was genuinely hard.

---

## ⚠️ Trap 1 — `height: 100vh` must become `height: 100%` when you stack

**This is the bug that was still in my build, and it's the one the instructor demos on purpose.**

Keeping `height: 100vh` inside the media query looks harmless. It isn't:

| | container height | content needs | first card's top edge |
|---|---|---|---|
| `height: 100vh` ❌ | **804px** (locked to the window) | **895px** | **−82px** — *above the top of the page* |
| `height: 100%` ✅ | **967px** (grows with content) | 967px | **+8px** — nothing cut |

*(Measured in Chrome at a 760×900 window.)*

### Why it breaks — and why it's worse than a normal overflow

`justify-content: center` centres the items in the container. When the content is **taller** than the
container, "centred" means the overflow splits **both ways** — half spills below, half spills **above**.
Scrolling can reach the bottom half. **It can never reach the top half.** The "Basic" heading is not just
off-screen, it's *unreachable*.

> The instructor's words: *"when you scroll to the top and the bottom, it actually cuts off a bunch of stuff."*

**The rule:** `100vh` means *"exactly one screen tall, no more"*. That's right for a **row** that fits on one
screen. It's wrong the moment content **stacks**. Use `height: 100%` (or `min-height: 100vh`, which is the
even safer idiom — one screen *minimum*, free to grow).

```css
min-height: 100vh;   /* 👍 grows past one screen when it needs to */
height: 100vh;       /* 👎 hard cap — overflows, and centring hides the top */
```

---

## ⚠️ Trap 2 — `padding: 0` on the `<li>` does nothing

I put `padding: 0` on the `li` to remove the list indent. It had **zero effect** — the feature list stayed
pushed ~20px to the right of the title and price.

**Both** the bullet *and* the indent belong to the **`<ul>`**, not the `<li>`:

- `list-style` → set on the `<ul>` (it does inherit, so on the `li` it happens to work too)
- **`padding-left: 40px`** → the browser default, **on the `<ul>` only**

```css
li            { padding: 0; }   /* ❌ measured: ul padding-left still 40px */
.plan-features{ padding: 0; }   /* ✅ measured: 0px — list finally centres */
```

Because the card has `text-align: center`, a `<ul>` that's 40px narrower on its left centres its text
**20px too far right**. A subtle misalignment with an obvious cause once you know where to look.

> 🔎 **How to catch this yourself:** DevTools → select the `<ul>` → **Computed** tab → look at
> `padding-left`. Don't guess which element owns a default.

---

## Trap 3 — selector hygiene

```css
li     { ... }   /* ❌ hits every list item on the page */
button { ... }   /* ❌ hits every button on the page    */

.plan-features li { ... }   /* ✅ scoped */
.plan-button      { ... }   /* ✅ scoped */
```

The HTML **already gave me the classes** (`.plan-features`, `.plan-button`) — using bare element selectors
throws away work that was done for me. Harmless on a 3-card page; a real bug the moment a second list or
button exists. Ties back to the **specificity/cascade** lesson (`concept_css.md`).

---

## Trap 4 — media query hygiene

Only override what **changes**. Everything else still applies from the base rule.

```css
/* ❌ re-declares 4 properties that were never going to change */
@media (max-width: 1250px) {
  .pricing-container {
    display: flex; flex-direction: column;
    justify-content: center; align-items: center;
    height: 100vh; gap: 2rem;
  }
}

/* ✅ two lines, and it's obvious what the breakpoint actually does */
@media (max-width: 1250px) {
  .pricing-container { flex-direction: column; height: 100%; }
}
```

Repeating rules hides the *intent*. When the lean version is two lines, anyone reading it instantly sees
"at 1250px we go vertical" — and there's only one place to change `gap` later.

---

## CSS units — the questions this project raised

From the review log. The recurring mistake was **mixing axes**.

| Unit | Relative to | Use it for |
|---|---|---|
| `px` | nothing — absolute | borders, tiny precise nudges, things that shouldn't scale |
| `rem` | **root** `<html>` font-size (default **16px**) | layout spacing, `gap`, margins/padding — scales with zoom |
| `em` | **parent** font-size (compounds when nested) | spacing tied to *this* element's text |
| `%` | the parent's matching dimension | fluid widths, `height: 100%` |
| `vw` | 1% of viewport **WIDTH** | width-ish sizing |
| `vh` | 1% of viewport **HEIGHT** | height-ish sizing (`height: 100vh`) |

```text
1rem = 16px  ·  2rem = 32px  ·  0.5rem = 8px
On a 1280px screen: 10vw = 128px · 20vw = 256px · 30vw = 384px
```

### 🔑 Axis discipline

```css
height: 100vh;      /* ✅ height property, height unit  */
max-width: 400px;   /* ✅ width property,  neutral unit */
max-width: 30vw;    /* ✅ width property,  width unit   */
max-width: 50vh;    /* ❌ width property,  HEIGHT unit  */
```

`max-width: 50vh` was my submission #2. On a 900px-tall screen that's a 450px-wide cap — a card's width
driven by an **unrelated dimension**. It isn't a syntax error, so nothing warns you; it just behaves
strangely as the window changes shape.

And `30vw` (≈384px on a 1280px screen) isn't *wrong* either — but `max-width: 400px` is chosen because a
card has a **readable width**, which is a property of the text, not of the window. Fixed and predictable
beats clever here.

### Why `gap: 2rem` rather than `gap: 32px`

Same pixels today (`2 × 16px`). But `rem` is tied to the root font-size, so the spacing stays proportional
if the user zooms or you ever change `html { font-size }`. Spacing that scales with type = a design system;
spacing in `px` = a fixed guess.

---

## My iteration log (worth re-reading — the mistakes are the lesson)

| # | What I wrote | Verdict |
|---|---|---|
| 1 | `flex-basis: 440px` (no grow) | Works, but rigid — cards can't share the row. `flex: 1` is the intent. |
| 2 | `flex: 1` + `max-width: 50vh` | Right idea, **wrong axis** — a width capped by screen *height*. |
| 3 | `flex: 1` + `max-width: 400px` | ✅ Sizing correct. Left: the `100vh` media query + the `<ul>` padding. |
| ✔ | + `height: 100%`, `.plan-features` reset, scoped selectors, `border-radius` | Matches the goal. |

**Pattern in my own mistakes:** the *layout thinking* was right every time. What tripped me up was
**which element owns a property** (`ul` vs `li`) and **which axis a unit belongs to** (`vh` vs width).
Both are "read the property, not the vibe" errors — worth a deliberate pause on future projects.

---

## Key takeaways

- **`flex: 1` + `max-width`** = fluid but capped. The professional card pattern; memorise it.
- **`justify-content: center` + `align-items: center` + a height** = centre anything, both axes.
- **`100vh` is a hard cap.** Fine for a single-screen row; wrong once content stacks — use `height: 100%`
  or `min-height: 100vh`. Centred overflow hides content **above** the page where scrolling can't reach it.
- **Defaults live on a specific element.** The list indent is the `<ul>`'s `padding-left: 40px` — check
  Computed styles instead of guessing.
- **Use the classes the HTML gives you.** Bare `li` / `button` selectors leak.
- **In a media query, override only what changes.**
- **Match the unit to the axis.** `vh` for height, `vw`/`px`/`%` for width.
- One media query line — `flex-direction: column` — is the entire responsive story. That's the payoff for
  the whole Flexbox section.
