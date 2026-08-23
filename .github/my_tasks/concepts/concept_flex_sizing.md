# Flex Sizing — `flex-grow` / `flex-shrink` / `flex-basis`

> ⚠️ **SELF-FLAGGED WEAK AREA — this is the "read me every revision" file.**
> Source: lesson `9. Flexbox → 57. Flex Sizing` · formula slide: `course_content/FLEXBOX/flexbox_sizing_formula.png`
> Printable hard copy: `flexbox_master_notes.pdf` (repo root)

---

## 🚀 The 60-second recall (if you read nothing else)

```text
1. WHO WINS?      min/max-width  >  flex-basis  >  width  >  content width
2. THREE LEVERS   flex: <grow> <shrink> <basis>      → "can I get bigger / can I get smaller / where do I start"
3. THE DEFAULT    flex: 0 1 auto   → shrink YES, grow NO
4. THE WORKHORSE  flex: 1          → = 1 1 0%  → equal columns, ratios respected
5. LIMITS ARE NOT TARGETS. max-width = ceiling. min-width = floor. Neither asks for a size.
6. GROW & SHRINK are RATIOS, not pixels. 1 : 2 : 3 → 100px : 200px : 300px.
```

---

## 1. The priority ladder — who overrides who

The course's own formula slide:

```text
Content width  <  width  <  flex-basis  <  min-width / max-width
   (weakest)                                      (strongest)
```

Read it top-down as **"1 beats 2 beats 3 beats 4"**:

| # | Property | Role | Beats |
|---|---|---|---|
| 1 | `min-width` / `max-width` | **The law.** Hard floor / hard ceiling. Applied LAST. | everything |
| 2 | `flex-basis` | **The request.** The size the item asks for on the main axis. | `width`, content |
| 3 | `width` | The normal CSS size — *ignored on the main axis* once `flex-basis` is set. | content |
| 4 | Content width | The fallback: as wide as the text/image inside needs. | — |

**Selva-speak:** *the item asks (`flex-basis`), the law answers (`min`/`max`), `width` only speaks when
`flex-basis` stays silent, and content is the last man standing.*

---

## 2. `flex-basis` vs `width` — basis wins

```css
.item {
  width: 300px;       /* ❌ ignored on the main axis */
  flex-basis: 100px;  /* ✅ this is the size used */
}
```

- If `flex-basis` exists → **`width` is completely ignored** (on the main axis only).
- If the basis can't be honoured (no room), the item falls back down the ladder to its
  **minimum content width** and stops there.
- 🔑 **"Main axis only"** is the catch: in `flex-direction: row`, `flex-basis` = width, and `height`
  still works normally. In `flex-direction: column`, `flex-basis` = **height**, and `width` works
  normally again. `flex-basis` never fights the cross axis.

| Container | `flex-basis` controls | Untouched |
|---|---|---|
| `flex-direction: row` (default) | **width** | `height` |
| `flex-direction: column` | **height** | `width` |

---

## 3. `flex-basis` vs `min-width` / `max-width` — 4 scenarios, 1 rule

The browser sizes the item **first** (basis → grow/shrink), **then** clamps it. Clamping is the last step.

```text
final size = clamp( min-width , size from basis/grow/shrink , max-width )
```

| # | Setup | Basis respects the limit? | **Final width** |
|---|---|---|---|
| S1 | `flex-basis: 200px` + `max-width: 100px` | ❌ breaks the ceiling | **100px** (limit wins) |
| S2 | `flex-basis: 50px` + `max-width: 200px` | ✅ under the ceiling | **50px** (basis wins) |
| S3 | `flex-basis: 200px` + `min-width: 300px` | ❌ breaks the floor | **300px** (limit wins) |
| S4 | `flex-basis: 400px` + `min-width: 300px` | ✅ above the floor | **400px** (basis wins) |

**The one rule:** if the requested size already sits inside the allowed range, `flex-basis` is the
answer. If it falls outside, **the limit it broke becomes the answer.**

Shortcut: **vs `max-width` the smaller wins · vs `min-width` the larger wins.**

### Say it in your own words

- **`max-width` = the item's potential to EXTEND** — how big it's *allowed* to get.
- **`min-width` = the item's potential to SHRINK** — how small it's *allowed* to get.
- **Neither is a goal.** They only draw the boundaries. `flex-basis` is the only property actually
  *asking* for a size. `max-width: 200px` will never stretch a 50px item up to 200px.

> ⚠️ **Easy to mistype:** swap S4's `min-width` for `max-width: 300px` and the answer flips to **300px**
> (that's just S1 again). **Always name the limit out loud — "ceiling or floor?" — before answering.**

### Two follow-on traps

1. **`max-width` also caps `flex-grow`.** `flex-grow: 1; max-width: 300px` grows into free space then
   stops dead at 300px — the leftover then goes to the other items.
2. **`min-width` beats `max-width`.** `min-width: 300px; max-width: 100px` → **300px**. The floor is
   checked last, so it wins.

---

## 4. The three levers — what each one actually means

| Property | Question it answers | Default | Unit |
|---|---|---|---|
| `flex-grow` | *"If there's spare space, do I take a share of it?"* | `0` (**no**) | ratio (unitless) |
| `flex-shrink` | *"If we're overflowing, do I give up some of my size?"* | `1` (**yes**) | ratio (unitless) |
| `flex-basis` | *"What size do I start from before any of that happens?"* | `auto` (= use `width`, else content) | length / % / `auto` / `0` |

All three are **child (flex item) properties** — never on the container.

> 🧠 grow/shrink are **ratios**, not pixels. `flex-grow: 5` doesn't mean "5px" or "500%", it means
> *"give me 5 shares of the leftover, while a `1` item gets 1 share."*

---

## 5. The 4 grow/shrink scenarios (`gs-1` … `gs-4`)

All four use `flex-basis: 100px`. Only grow/shrink change — and the whole *behaviour* changes with them.

```text
gs-1   flex: 0 0 100px      [====100px====]              RIGID — a brick
gs-2   flex: 1 0 100px      [====100px====]--------->    100px is the FLOOR
gs-3   flex: 0 1 100px  <---[====100px====]              100px is the CEILING   ← DEFAULT behaviour
gs-4   flex: 1 1 100px  <---[====100px====]--------->    100px is just the START LINE
```

| # | grow | shrink | Can grow? | Can shrink? | Allowed range | `100px` acts as |
|---|---|---|---|---|---|---|
| **gs-1** | 0 | 0 | ❌ | ❌ | exactly `100px` | a **fixed** width — zero flexibility |
| **gs-2** | 1 | 0 | ✅ freely | ❌ | `100px → available space` | a **minimum** |
| **gs-3** | 0 | 1 | ❌ | ✅ to min-content | `min-content → 100px` | a **maximum** |
| **gs-4** | 1 | 1 | ✅ | ✅ | `min-content → available space` | a **starting point** |

### 🔑 gs-3 is Flexbox's factory default

`flex: 0 1 auto` is what every flex item does when you write nothing at all:

> **You are allowed to shrink. You are NOT allowed to grow.**

That's why a row of items squeezes when the window narrows but never spreads out to fill the row —
until you hand out a `flex-grow`.

### gs-4 and "DUMMY PIECE BAAVA" — the honest version

With `flex: 1 1 100px` the item shrinks *and* grows, so the `100px` never survives as a final width.
Calling it a dummy piece is the right instinct — **but with one correction that matters later:**

> `flex-basis` is a dummy as a **final width**. It is still very much alive as the **starting line**.

Free space is measured *after* every basis is laid down, and then shared out. So `flex: 1 1 0` and
`flex: 1 1 auto` give **completely different results** — see §6. If the basis were truly ignored,
they'd be identical. (Verified in Chrome: two items, one short + one long, in a 600px row →
`flex: 1 1 auto` gives **182px / 418px**, `flex: 1 1 0` gives **300px / 300px**.)

---

## 6. `flex-basis: auto` vs `0` — the one switch you'll use most

Same grow, same shrink. Only the starting line moves — and that changes everything.

```css
/* CONTENT-PRIORITY: big content keeps more room */
.item { flex: 1 1 auto; }   /* start at content size, then share the LEFTOVER equally */

/* EQUAL COLUMNS: content is irrelevant */
.item { flex: 1 1 0; }      /* start at zero, so ALL space is shared equally */
```

| | `flex-basis: auto` | `flex-basis: 0` |
|---|---|---|
| Starting size | each item's own content/`width` | `0` for everyone |
| A 10-word sentence | gets **maximum** room | gets the **same** room as everyone |
| A single word | gets **minimum** room | gets the **same** room as everyone |
| Use it for | navbars, tag lists, "size me to my content" | **equal-width columns**, card grids, pricing tables |

**Mnemonic:** `auto` = *"share the leftovers"* · `0` = *"share everything."*

---

## 7. The `flex` shorthand

```css
flex: <flex-grow> <flex-shrink> <flex-basis>;
```

```css
/* longhand */                    /* shorthand */
flex-grow: 1;                     flex: 1 1 0;
flex-shrink: 1;        ═══►       /* or simply */
flex-basis: 0;                    flex: 1;
```

### The presets worth memorising

| Shorthand | Expands to | Meaning |
|---|---|---|
| `flex: 1` | `1 1 0%` | **equal columns.** The workhorse. |
| `flex: 2` | `2 1 0%` | takes **2 shares** of the space |
| `flex: auto` | `1 1 auto` | grows & shrinks, but content-weighted |
| `flex: none` | `0 0 auto` | rigid, sized to content — will not budge |
| `flex: initial` | `0 1 auto` | the default: shrink yes, grow no |
| `flex: 0 0 250px` | — | a hard 250px sidebar |

### ⚠️ Correction to make now — `flex: 2` does **NOT** mean `2 2 0`

> One number sets **`flex-grow` only**. `flex-shrink` stays at **`1`**, and `flex-basis` becomes **`0%`**.
>
> `flex: 2` → `flex-grow: 2; flex-shrink: 1; flex-basis: 0%;`
>
> (Confirmed with `getComputedStyle` in Chrome.) It doesn't change the 1:2:3 ratio result at all —
> with a basis of `0` there's nothing to shrink anyway — but say it correctly in an interview.

### ⚠️ The shorthand quietly resets the basis

```css
.a { flex-grow: 1; }   /* basis stays AUTO → content-weighted widths */
.b { flex: 1; }        /* basis becomes 0%  → EQUAL widths */
```

Same intent, different result. **Any omitted `flex-basis` in the shorthand defaults to `0`, not `auto`.**
This single line explains most "why aren't my columns equal?" bugs.

---

## 8. Ratios in action — `flex: 1` / `flex: 2` / `flex: 3`

Three items in one row:

```css
.one   { flex: 1; }
.two   { flex: 2; }
.three { flex: 3; }
```

Total shares = `1 + 2 + 3 = 6`. In a **600px** container (basis 0, so all 600px is up for grabs):

```text
|<-- 100px -->|<-------- 200px -------->|<-------------- 300px -------------->|
|    flex:1   |         flex: 2         |               flex: 3               |
     1 share          2 shares                       3 shares
```

- **Ratios are respected**: `1x : 2x : 3x`.
- Resize the window and they **grow and shrink together, still 1:2:3**. The `3` item moves 3px for
  every 1px the `1` item moves.
- Adding a 4th `flex: 1` item makes it 7 shares → `600/7` per share. The ratio adapts automatically.

---

## 9. How the browser actually computes it (the 5-step algorithm)

Worth reading once, then you'll never be surprised again:

1. **Lay down the basis.** Every item takes its `flex-basis` (or `width`, or content size).
2. **Measure free space.** `free = container size − Σ(basis) − Σ(gaps) − margins`.
3. **Positive free space?** → share it out by **`flex-grow` ratio**.
   **Negative (overflow)?** → claw it back by **`flex-shrink` × basis** (see below).
4. **Clamp** each item to its `min-width` / `max-width`.
5. **Position** whatever space is still left with `justify-content`.

> `gap` is eaten in step 2 — it's subtracted *before* anything is shared. A 600px row with
> `gap: 20px` and 3 items only has **560px** to distribute.

### The asymmetry nobody tells you: shrink is weighted by basis

- **Grow** is a plain ratio: grow factor only.
- **Shrink** is weighted: `shrink factor × flex-basis`. A bigger item loses proportionally more.

Verified: items with `basis 200px` and `basis 400px` (both `shrink: 1`) squeezed into `300px` →
**100px and 200px**, not 50px and 250px. The 400px item gave up twice as much because it had twice
as much to give. *Makes sense — a big item can afford a bigger haircut.*

---

## 10. Real-world gotchas (these will bite you in projects)

### 🐛 #1 — "My item refuses to shrink / my text overflows"

Every flex item silently carries **`min-width: auto`**, which resolves to its **min-content size**
(the longest unbreakable word, or an image's intrinsic width). `flex-shrink` cannot cross that floor.

```css
.item {
  flex: 1;
  min-width: 0;         /* ✅ the fix — lets it shrink below its content */
  /* overflow: hidden;  also unlocks shrinking */
}
```

Verified: a 100px container holding `Antidisestablishmentarianism` stayed **190px** wide until
`min-width: 0` was added — then it obeyed at **100px**. This is the #1 flexbox bug in real code
(long URLs, `<pre>` blocks, `text-overflow: ellipsis` that "doesn't work").

### 🐛 #2 — `box-sizing`

`flex-basis` sizes the **content box** by default, so padding and border are added *on top*.
Set `box-sizing: border-box` (usually globally with `*`) so `flex-basis: 200px` really means 200px total.

### 🐛 #3 — Images

Images have an intrinsic size and don't shrink politely. `min-width: 0` + `max-width: 100%`, or
`flex-shrink: 0` if you want them fixed.

### 🐛 #4 — Percentage basis

`flex-basis: 50%` is a percentage of the **container's main size** — not of the item, not of the viewport.
Handy: `flex: 1 1 50%` + `flex-wrap: wrap` = a 2-column responsive grid.

### 💡 #5 — `margin: auto` eats free space

`margin-left: auto` on one item pushes it (and everything after it) to the far end. The classic
"logo left, links right" navbar trick — no `justify-content` gymnastics needed.

```css
.navbar { display: flex; }
.navbar .login { margin-left: auto; }   /* shoved to the right edge */
```

---

## 11. The patterns you'll actually type

```css
/* Equal-width columns */
.row > *          { flex: 1; }

/* Fixed sidebar + fluid content */
.sidebar          { flex: 0 0 250px; }
.content          { flex: 1; min-width: 0; }

/* Holy grail: 3 columns, middle one twice as wide */
.left, .right     { flex: 1; }
.middle           { flex: 2; }

/* Responsive cards: min 250px, grow to fill, wrap when tight */
.cards            { display: flex; flex-wrap: wrap; gap: 1rem; }
.cards > *        { flex: 1 1 250px; }

/* Perfect centering */
.hero { display: flex; justify-content: center; align-items: center; height: 100vh; }
```

---

## Quick self-check (cover the right column)

| # | Setup | Final size |
|---|---|---|
| 1 | `width: 300px; flex-basis: 100px` (row) | **100px** — basis beats width |
| 2 | `flex-basis: 200px; max-width: 100px` | **100px** — basis breaks the ceiling |
| 3 | `flex-basis: 50px; max-width: 200px` | **50px** — ceiling never used |
| 4 | `flex-basis: 200px; min-width: 300px` | **300px** — basis breaks the floor |
| 5 | `flex-basis: 400px; min-width: 300px` | **400px** — floor never used |
| 6 | `min-width: 300px; max-width: 100px` | **300px** — floor beats ceiling |
| 7 | `flex: 0 0 100px`, window resized | **100px always** — rigid |
| 8 | `flex: 1 0 100px`, tiny window | **100px** — can't shrink below the basis |
| 9 | `flex: 0 1 100px`, huge window | **100px** — can't grow past the basis |
| 10 | `flex: 1` written out in full | **`1 1 0%`** |
| 11 | `flex: 2` written out in full | **`2 1 0%`** (shrink is 1, **not** 2) |
| 12 | `flex: 1` / `flex: 2` / `flex: 3` in 600px | **100 / 200 / 300** |
| 13 | `flex-grow: 1` alone vs `flex: 1` | basis `auto` (content-weighted) vs `0` (equal) |
| 14 | `flex: 1` on a long unbreakable word | won't shrink past min-content → add `min-width: 0` |
