# Flex Sizing — `flex-grow` / `flex-shrink` / `flex-basis`

> ⚠️ **SELF-FLAGGED WEAK AREA — this is the "read me every revision" file.**
> Source transcript: `course_content/FLEXBOX/flexsizing_transcript.txt` · formula slide: `course_content/FLEXBOX/flexbox_sizing_formula.png`
> Exercise: [Flexbox Sizing Exercise](https://appbrewery.github.io/flexbox-sizing-exercise/) (solution in the tasks file)
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

### How the lesson phrases it — walk the list top-down

> *"The first thing it looks at is whether there is a min-width and max-width set on the item. If this is
> not set, it looks at the next thing: is there a flex-basis set? If there's no flex-basis either, it looks
> at the width — or the height on a column-based flexbox. The final one, if none of those are set, is the
> actual content width."*

So: **walk down the list until you hit something that's actually set — that's your size.** (The real CSS
engine also *clamps* with `min`/`max-width` at the very end, which is precisely why they sit at the top
of the list: whether you meet them first or last, they always win.)

---

## 1b. "Content width" is not one number — it's a RANGE

This is the piece that makes everything else click. Every element has **two** natural content sizes:

| | What it is | The lesson's words |
|---|---|---|
| **max-content** (the "ideal" width) | the width where **all the text fits on ONE line** | *"all of the content lined up, occupying the ideal estate"* |
| **min-content** (the floor) | the width of the **single longest WORD**, at the current font-size | *"the minimum width looks at the longest word"* |

With **no sizing properties at all**, a flex item **starts at max-content and shrinks toward min-content.**

- 🔑 **Shrinking is NOT uniform.** Each item has its **own** floor, because each has its own longest word.
  In the lesson's demo, the box containing the word **"programming"** stays visibly the widest — flexbox
  refuses to break a word across lines.
- 🔑 **Past the floor, it stops shrinking and overflows.** Keep narrowing the window and the content is
  *"pushed off the page and will not be visible on screen anymore."* It does **not** keep shrinking.
- This min-content floor is exactly what `min-width: auto` resolves to — see gotcha #1 in §10.

```text
        min-content                                   max-content
        (longest word)                                (all on one line)
             |◄───────── the item lives in here ─────────►|
      overflows                                      won't grow past this
      off-screen                                     unless you let it grow
```

---

## 2. `flex-basis` vs `width` — basis wins

```css
.item {
  width: 300px;       /* ❌ ignored on the main axis */
  flex-basis: 100px;  /* ✅ this is the size used */
}
```

- If `flex-basis` exists → **`width` is completely ignored** (on the main axis only).
- The lesson is blunt about it: *"there's actually not even any point in setting it, because it's going to
  be looking at the more important property."* Setting both is just noise — delete the `width`.
- If the basis can't be honoured (no room), the item falls back down the ladder to its
  **minimum content width** and stops there.

### `width` and `flex-basis` behave *identically* under pressure

Whichever one wins the lookup, it is only a **preferred** size — it gets abandoned the moment there
isn't room. Worked example from the lesson:

```text
4 items × width: 100px  +  gap: 10px × 3   →  the container needs ~430px

container ≥ 430px  →  every item is exactly 100px  ✅ preference respected
container < 430px  →  the 100px is ABANDONED; each item shrinks toward its OWN min-content
```

> *"As soon as there's not enough space in the container to accommodate all of the items that have the set
> width, it's going to ignore this and dynamically shrink each of the items until it reaches that minimum
> width for each item."* — and the same sentence is true word-for-word if you swap `width` for `flex-basis`.

**The only difference between `width` and `flex-basis` is who wins the lookup, not how they behave.**
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

### 🔍 The 3 questions — steal the instructor's debugging method

When the lesson sets the exercise, it tells you exactly what to look for:

> *"Resize the window and see how the green box behaves. **Does it grow? Does it shrink? What's the size
> that it wants to be?**"*

Those three questions **are** the three properties, in order:

| Grab the window edge and ask… | …and you've found |
|---|---|
| **Does it grow** when I widen the window? | `flex-grow` |
| **Does it shrink** when I narrow it? | `flex-shrink` |
| **What size does it want to be** when there's plenty of room? | `flex-basis` |

Run this on any layout you're copying or debugging **before writing a single line of CSS.**

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

Straight from the lesson: *"the flex-basis is pretty much completely ignored because flex-grow and
flex-shrink are both on. It's going to grow to the max-width and shrink to the minimum width — and if
those two aren't set, it infers them from the content."* So the item's range becomes:

```text
min-width  (or min-content)  ◄────────────────►  max-width  (or the available space)
```

With `flex: 1 1 100px` the item shrinks *and* grows, so the `100px` never survives as a final width.
Calling it a dummy piece is the right instinct — **but note the lesson's hedge, "pretty much", and the
one correction that matters later:**

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

**🎧 Your note was NOT a mis-hearing — the lesson says it too.** Transcript, on the `flex: 2` box:

> *"…essentially what we're doing here is we're setting the grow to 1 and the shrink to 1. And in this
> case, it's a grow of 2 and **a shrink of 2**."*

That last bit is a slip in the video. `flex: 1` → grow 1 / shrink 1 is correct (coincidence: the default
shrink already *is* 1), which is probably what carried it over to `flex: 2`. Trust the browser:
**a single number never touches `flex-shrink`.**

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
| 15 | An item with **no** sizing properties at all | starts at **max-content** (all on one line), shrinks to **min-content** (longest word) |
| 16 | Narrowed past min-content | stops shrinking → **overflows off-screen** |
| 17 | Why do 4 items shrink at *different* rates? | each has its **own** longest word = its own floor |
| 18 | 4 items × `width: 100px`, `gap: 10px`, container 400px | `100px` abandoned (needs ~430px) → each shrinks to its own min-content |
