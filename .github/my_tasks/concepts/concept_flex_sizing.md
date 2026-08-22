# Flex Sizing — `flex-basis` vs `max-width` / `min-width`

> **Status:** in-progress notes. Seeded with a self-identified **weak area** before the full
> Flexbox Sizing lesson (`flex-grow` / `flex-shrink` / `flex-basis`) is digested.

---

## ⚠️ WEAK AREA — READ THIS EVERY REVISION

### The confusion

`flex-basis` and `max-width` both look like "set the width", so it feels like they fight each other
and you can't tell which one wins. They are **not** the same kind of property:

- `flex-basis` = the **requested / starting size** of a flex item along the main axis.
- `max-width` = a **hard ceiling**. It doesn't request anything, it only says *"never go past me."*
- `min-width` = a **hard floor**. *"never go below me."*

The browser sizes the item **first** (from `flex-basis`, then `flex-grow` / `flex-shrink`), and
**then** clamps the result between `min-width` and `max-width`. Clamping is the **last** step.

---

### Scenario 1 — `flex-basis` **>** `max-width`

```css
.item {
  flex-basis: 200px;
  max-width: 100px;
}
```

- The requested `200px` **breaks** the ceiling.
- So `flex-basis` is **overruled** — the clamp kicks in.
- **Final width = 100px** (the `max-width`).

### Scenario 2 — `flex-basis` **<** `max-width`

```css
.item {
  flex-basis: 50px;
  max-width: 200px;
}
```

- The requested `50px` is **within** the ceiling, so `max-width` never has to do anything.
- `flex-basis` is **fully respected**.
- **Final width = 50px** (the `flex-basis`).

> Note: `max-width: 200px` does **not** stretch the item up to 200px. A ceiling is not a target.

---

### Scenario 3 — `flex-basis` **<** `min-width`

```css
.item {
  flex-basis: 200px;
  min-width: 300px;
}
```

- The requested `200px` **breaks** the floor (it's below the minimum allowed).
- So `flex-basis` is **overruled** — the clamp kicks in.
- **Final width = 300px** (the `min-width`).

### Scenario 4 — `flex-basis` **>** `min-width`

```css
.item {
  flex-basis: 400px;
  min-width: 300px;
}
```

- The requested `400px` is **above** the floor, so `min-width` never has to do anything.
- `flex-basis` is **fully respected**.
- **Final width = 400px** (the `flex-basis`).

> Note: `min-width: 300px` does **not** shrink the item down to 300px. A floor is not a target either.

> **⚠️ Easy to mistype:** swap Scenario 4's `min-width` for `max-width` and the answer flips —
> `flex-basis: 400px` + `max-width: 300px` → **300px**, not 400px (that's just Scenario 1 again).
> Always name the limit out loud — *"ceiling or floor?"* — before deciding who wins.

---

### The symmetry — 4 scenarios, 1 rule

| | Basis obeys the limit | Basis breaks the limit |
|---|---|---|
| **`max-width`** (ceiling) | S2: `50` vs `200` → **50** (basis wins) | S1: `200` vs `100` → **100** (limit wins) |
| **`min-width`** (floor) | S4: `400` vs `300` → **400** (basis wins) | S3: `200` vs `300` → **300** (limit wins) |

**One rule for all four:** the browser tries `flex-basis`. If that value already sits inside the
allowed range, `flex-basis` is the answer. If it falls outside, the limit it broke becomes the answer.

---

### Selva — say it in your own words

- **`max-width` = the potential of the item to *extend* — how big it is *allowed* to get.**
- **`min-width` = the potential of the item to *shrink* — how small it is *allowed* to get.**
- **Neither one is a goal.** They only draw the boundaries of the allowed range; `flex-basis` is the
  only one actually *asking* for a size.
- **If `flex-basis` does NOT respect the limit → the limit steps in and becomes the final width.**
  (`flex-basis` > `max-width` → `max-width` wins · `flex-basis` < `min-width` → `min-width` wins)
- **If `flex-basis` DOES respect the limit → the limit stays out of the way and `flex-basis` becomes
  the final width.** (`flex-basis` < `max-width` → basis wins · `flex-basis` > `min-width` → basis wins)

Shorthand to memorise:

```text
final width = clamp(min-width, <size from flex-basis/grow/shrink>, max-width)
```

So: vs. `max-width` the **smaller** value wins; vs. `min-width` the **larger** value wins.

---

### Two follow-on traps to remember

1. **`max-width` also caps `flex-grow`.** An item with `flex-grow: 1; max-width: 300px` will grow into
   free space but stop dead at `300px` — the leftover space then goes to the other items.
2. **`min-width` beats `max-width`.** If you ever write `min-width: 300px; max-width: 100px`, the
   floor wins and the item is `300px`. The floor is checked last.

---

## Quick self-check

| # | `flex-basis` | Limit | Final width | Why |
|---|---|---|---|---|
| S1 | `200px` | `max-width: 100px` | **100px** | Basis breaks the ceiling → clamped down |
| S2 | `50px` | `max-width: 200px` | **50px** | Basis is under the ceiling → ceiling never used |
| S3 | `200px` | `min-width: 300px` | **300px** | Basis breaks the floor → clamped up |
| S4 | `400px` | `min-width: 300px` | **400px** | Basis is above the floor → floor never used |
| — | `150px` | `max-width: 150px` | **150px** | Equal, nothing to clamp |
| — | `0` + `flex-grow: 1` | `max-width: 120px` | **≤120px** | Grows into free space but stops at the ceiling |
| — | `50px` | `max-width: 100px` + `min-width: 80px` | **80px** | Floor is applied last and raises it |
