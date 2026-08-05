# Practice Tasks: HTML Elements — Structure, Lists, Links & Images

Based on: `course_content/HTML/html_part1.txt` → `html_part7.txt` and `EX 2.1`–`EX 3.4`
Notes: `.github/my_tasks/concepts/concept_html_elements.md`

## Problem Statements (With Input Data)

1. **Fix the missing wrapper.** Given this snippet (the actual bug from `EX 2.3 Void Elements/mistake.md`):
   ```html
   William Blake<br />
   17 South Molton Street<br />
   London<br />
   ```
   Rewrite it correctly, including whatever tag is missing, and explain in one sentence *why* `<br />`
   alone isn't enough here.

2. **Heading levels from a real structure.** Given this outline, write the HTML using the correct heading
   levels (no skipped levels, only one top-level heading):
   ```
   Cinnamon Roll Recipe
     Ingredients
       Dough ingredients (list)
       Filling ingredients (list)
     Instructions (list)
   ```

3. **Convert this list to nested HTML.** Write the `ul`/`ol` markup for:
   ```
   - A
   - B
     1. B1
     2. B2 (unordered under here: B2a, B2b)
   - C
   ```
   Pay attention to where B's `</li>` closing tag actually goes.

4. **Build a mini favorites list.** Using `EX 3.2` as reference, write an `<ol>` with 3 `<li>` items, each
   containing an `<a href="...">` to a real website, and make the list start counting from `10` instead
   of `1`.

5. **Add an accessible image.** Write an `<img>` tag pointing at `https://picsum.photos/300/200` with an
   `alt` description appropriate for a placeholder photo used in a draft layout.

## Questions and Answers

6. **Define in your own words** (1-2 sentences each):
   - Tag vs. element
   - Void element
   - Attribute
   - Global attribute (give an example other than `draggable`)
7. **Why is `<p>` important for accessibility**, specifically for screen reader users — what exactly does
   the screen reader do differently at a `<p>` boundary vs. plain unwrapped text?
8. **What's the difference** between the `/` in a closing tag (`</p>`) and the `/` in a void element
   (`<hr />`) — where does each one sit in the tag?
9. **Why does `<img>` have no closing tag**, in your own words, referencing what the "content" of an
   image conceptually is?
10. **Explain the nesting rule** for lists in your own words: when you put a `<ul>` inside an `<li>`, why
    does the outer `<li>`'s closing tag move to after the nested list instead of right after the text?
11. **Two conventions, not hard rules**: name the two heading conventions from the lesson (one `h1`, don't
    skip levels) and explain why breaking them won't crash your page but is still bad practice.

## Self Assignments (No Answers)

12. **Recreate a real page's list structure.** Pick any "Top 10" or "Best of" article online, right-click
    → Inspect, and identify whether it uses `<ul>` or `<ol>` and why that choice makes sense (or doesn't).
13. **Screen reader check.** Turn on a screen reader (VoiceOver on Mac, Narrator on Windows) or a browser
    extension like Silktide, and listen to how it reads out a page with images. Note whether any images
    are missing `alt` text and what that sounds like.
14. **Build your own top-5 page.** Extend `EX 3.2 Anchor Elements` with your actual top 5 favorite
    websites, each with a real working link.
15. **Diffchecker debugging drill.** Intentionally break your `EX 2.3` solution (e.g. delete a closing
    `</p>`), observe how the preview breaks, then use diffchecker.com against the real solution to find it
    — practice reading the diff instead of eyeballing the code.
16. **Extend the Birthday Invite project.** Add a nested `<ul>` (e.g. a sub-list of "drinks to bring"
    under one of the existing `<li>` items) to `EX 3.4 Birthday Invite Project/index.html`, applying the
    nesting rule from Q10.

## Self-check

- [ ] I can explain the difference between a tag and an element without looking at notes.
- [ ] I know when to use `<br />` vs. a new `<p>`, and why the distinction matters for accessibility.
- [ ] I can write a correctly nested list (list-inside-a-list-item) from scratch.
- [ ] I know where attributes go, and the difference between an element-specific attribute and a global one.
- [ ] I always add `alt` text to meaningful images without being reminded.
- [ ] I completed EX 2.1 through EX 3.4 and checked my code against each solution file.
