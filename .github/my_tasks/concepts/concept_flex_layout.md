# Flex Layout — Ordering, Wrapping & Alignment

Source transcript: `course_content/FLEXBOX/flexlayout_transcript.txt`
Practice: [flex-layout demo playground](https://appbrewery.github.io/flex-layout/), [Flexbox Froggy](https://appbrewery.github.io/flexboxfroggy/) (Intermediate difficulty)
Cheat sheet: [CSS-Tricks — A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

## The problem this solves

Once a container is `display: flex`, items sit in source order on one line, sized to content. That's
rarely the final layout you want — you need to reorder items, decide what happens once they run out of
horizontal room, and distribute leftover space (or center things) along both axes. This lesson covers the
six properties that give you that control: `order`, `flex-wrap`, `justify-content`, `align-items`,
`align-self`, `align-content`.

---

## 0. Parent vs. child — get this right first

| Property | Goes on |
|---|---|
| `order` | **child** (flex item) |
| `flex-wrap` | **parent** (container) |
| `justify-content` | **parent** (container) |
| `align-items` | **parent** (container) |
| `align-content` | **parent** (container) — only matters once items wrap |
| `align-self` | **child** (flex item) — the one per-item override |

---

## 1. `order` — rearranging children without touching the HTML (child property)

- Every flex item defaults to `order: 0`. Items that share the same order fall back to their position
  in the HTML (source order).
- Flexbox sorts items lowest → highest. Set `order: 1` on one item and it jumps after everything still
  at `0`; a bigger number (`20`) sends it further right/down still.
- **Purely visual** — the underlying HTML/DOM order is untouched, which matters for accessibility:
  screen readers and tab order still follow the HTML, not the visual `order`.

```css
.rainbow > .green {
  order: 1; /* moves just this item to the end; everything else stays at the default order: 0 */
}
```

---

## 2. `flex-wrap` — what happens when items run out of room (parent property)

| Value | Behavior |
|---|---|
| `nowrap` (default — no hyphen) | Items shrink to fit one line; once they can't shrink further, they overflow off the page |
| `wrap` | Items that no longer fit drop onto a new line: top-left → bottom-right |
| `wrap-reverse` | Same wrapping, but new lines stack the opposite way: bottom-right → top-left |

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

Connects back to the **main/cross axis** idea from the Flex Direction lesson (`concept_flexbox.md`):
wrapping turns a single line into multiple lines, which is exactly what `align-content` (§6) then spaces.

---

## 3. `justify-content` — spacing along the MAIN axis (parent property)

Row container → main axis is horizontal. Column container → main axis is vertical. Only visible once
the items don't already fill all the available space.

| Value | Effect |
|---|---|
| `flex-start` (default) | Items packed at the start |
| `flex-end` | Items packed at the end |
| `center` | Items packed together, centered as a group |
| `space-between` | First/last items touch the edges; remaining space split evenly *between* items |
| `space-around` | Equal space on *both sides* of every item (edge gaps look half the between-item gap) |
| `space-evenly` | Every gap — edges included — is exactly equal |

```
flex-start:     [A][B][C]____________
flex-end:       ____________[A][B][C]
center:         _____[A][B][C]_____
space-between:  [A]______[B]______[C]
space-around:   __[A]____[B]____[C]__
space-evenly:   ___[A]___[B]___[C]___
```

---

## 4. `align-items` — position along the CROSS axis (parent property)

The cross axis is perpendicular to the main axis (vertical in a row container). It only has visible
room to work with once the container has extra height beyond what the items need — e.g. `height: 70vh`
(`vh` = viewport height; `100vh` is the full visible window height).

| Value | Effect |
|---|---|
| `flex-start` | Items align to the top (row container) |
| `flex-end` | Items align to the bottom |
| `center` | Items centered on the cross axis |
| `baseline` | Items aligned by their **text baseline**, ignoring box size |
| `stretch` (default) | Items stretch to fill the container's cross-axis size, if no fixed height is set on them |

**`baseline` vs `flex-start`**: `flex-start` lines up the *box top* of every item; `baseline` lines up
the *text baseline* instead. They only look identical when every item has the same font-size/padding
(so box-top happens to coincide with baseline too).

---

## 5. `align-self` — override for ONE item (child property)

Same value list as `align-items`, but set on a single flex item instead of the container — lets that
one item opt out of the group behavior.

```css
.container {
  display: flex;
  align-items: center;
}
.container > .special {
  align-self: flex-start; /* only this item ignores the container's align-items: center */
}
```

---

## 6. `align-content` — spacing BETWEEN wrapped lines (parent property)

- Only has any visible effect when `flex-wrap: wrap` (or `wrap-reverse`) is set **and** there are
  actually 2+ lines. On a single line, or with `nowrap`, it does nothing at all.
- Easy to confuse with `align-items`: `align-items` positions items *within* a line on the cross axis;
  `align-content` positions the *lines themselves* relative to each other once there's more than one.

```css
.container {
  display: flex;
  flex-wrap: wrap;
  align-content: center; /* only kicks in once items wrap onto 2+ lines */
}
```

---

## Key takeaways

- Six properties split into two camps: container (`flex-wrap`, `justify-content`, `align-items`,
  `align-content`) vs. item (`order`, `align-self`).
- Main axis → `justify-content`'s job. Cross axis → `align-items`'s job. Same main/cross split
  introduced in the Flex Direction lesson, just two more properties hooking into it.
- `align-content` needs `flex-wrap: wrap` **and** multiple lines to do anything — think of it as the
  "wrap" counterpart to `align-items`.
- Don't memorize every value — bookmark the [CSS-Tricks Flexbox cheat
  sheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) (it separates parent vs. child
  properties clearly) and look values up as needed.
- Practiced hands-on with [Flexbox Froggy](https://appbrewery.github.io/flexboxfroggy/) (Intermediate
  difficulty, no directions) and the [flex-layout demo playground](https://appbrewery.github.io/flex-layout/).
- Next lesson continues with **Flexbox sizing** (`flex-grow` / `flex-shrink` / `flex-basis`).
