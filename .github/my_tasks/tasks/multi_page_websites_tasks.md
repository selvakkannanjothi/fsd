# Practice Tasks: Multi-Page Websites — Paths, Boilerplate, Portfolio & Hosting

Based on: `course_content/Multi Page websites/` transcripts and `EX 4.0` → `EX 4.3`
Notes: `.github/my_tasks/concepts/concept_multi_page_websites.md`

## Problem Statements (With Input Data)

1. **Write the relative paths.** You are writing code inside `Folder0/index.html`. Given this structure,
   write the correct relative `src` for each image:
   ```
   4.0 File Paths/
     dog.png
     Folder0/
       index.html   <-- you are here
       rabbit.png
       Folder3/
         cat.png
     Folder1/
       fish.png
       Folder2/
         bird.png
   ```
   Give the path for: rabbit, cat, dog, fish, bird. (Use `./` and `../` correctly.)

2. **Spot the broken path.** For each snippet below (written inside `index.html`, which sits next to a
   `public/` folder and an `assets/images/cat.png`), say whether it works and fix it if not:
   ```html
   a) <img href="./assets/images/cat.png" alt="cat" />
   b) <a src="./public/about.html">About</a>
   c) <img src="../assets/images/cat.png" alt="cat" />
   d) <a href="./public/contact.html">Contact Me</a>
   ```

3. **Image-as-a-link.** Write an anchor tag on the home page that shows `assets/images/me.png` and, when
   clicked, navigates to the About page stored at `public/about.html`. Include `alt` text.

4. **Type the boilerplate from memory.** Without looking at the notes, write a complete HTML5 boilerplate
   with the title "Selva's Portfolio", the `lang`, `charset`, and `viewport` set correctly, and one `<h1>`
   inside the body. Then list which line you could safely delete and why.

5. **Portfolio link + preview.** Write the HTML for one portfolio entry: an `<h3>` containing an anchor to
   `public/movie-ranking.html` with the text "Movie Ranking Project", followed by a preview `<img>` of
   `assets/images/movie-ranking.png` sized to 200px tall with `alt` text.

## Questions and Answers

6. **Define in your own words** (1-2 sentences each):
   - Absolute vs. relative file path
   - What `./` means
   - What `../` means
   - Root (of a file system)

7. **Why does web development prefer relative paths** over absolute paths? Give the two reasons from the
   lesson.

8. **`href` vs `src`** — which attribute goes on `<a>`, which goes on `<img>`, and what does each one do?

9. **What is the `public/` folder convention**, and which single file is the exception that stays *outside*
   it?

10. **Head vs. body** — in one sentence each, what kind of thing goes in `<head>` vs `<body>`? Give two
    examples of tags that live in `<head>`.

11. **Why must the home page be named exactly `index.html`** for GitHub Pages, and name two filenames that
    would NOT work.

12. **What is web hosting**, in your own words, and what is the difference between "local development" and a
    site being "hosted"?

13. **The upload gotcha** — when uploading to GitHub, why must you drag the *contents* of your project
    folder rather than the folder itself?

## Self Assignments (No Answers)

14. **Complete `EX 4.0 File Paths`.** Get all five animal images (rabbit, cat, dog, fish, bird) showing in
    the preview using only relative paths. Verify against `goal.png`.

15. **Complete `EX 4.1 Webpages`.** Add (a) a text link to the Contact Me page and (b) an image that links
    to the About page, both from `index.html`. Check both links navigate correctly.

16. **Build your real portfolio (`EX 4.3`).** Work through all 7 to-do's with *your own* Movie Ranking and
    Birthday Invite code, your own titles, and your own screenshots. Don't settle for the fallback images
    if you can take your own.

17. **Autosuggest drill.** In VS Code, deliberately type a wrong special character (`..` where you meant
    `.`) in an `src` path and watch how the autosuggest dropdown changes — train yourself to notice the
    wrong suggestions as an early warning.

18. **Find-the-parent drill.** In any project, collapse folders one at a time until a target file
    disappears, to confirm which folder is its parent. Practice until it's automatic.

19. **Host it live.** Deploy your portfolio to GitHub Pages (public repo → upload contents → Settings →
    Pages → `main` branch). Visit the live URL on your phone to confirm it works away from your computer.

20. **Add a page.** Add a new `about.html` (or `projects.html`) to your portfolio's `public/` folder and
    link to it from the home page — then re-upload and confirm the new page is live.

## Self-check

- [ ] I can write relative paths using `./` and `../` from any starting file without guessing.
- [ ] I know the difference between `href` (on `<a>`) and `src` (on `<img>`) and never mix them up.
- [ ] I can type a full HTML5 boilerplate from memory and explain every line.
- [ ] I know the `public/` folder convention and why `index.html` must keep that exact name.
- [ ] I completed EX 4.0, EX 4.1, and EX 4.3 and checked each against its `goal.png`.
- [ ] I hosted my portfolio on GitHub Pages and shared the live link.
