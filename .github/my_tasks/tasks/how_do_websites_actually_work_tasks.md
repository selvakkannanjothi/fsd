# Practice Tasks: How Do Websites Actually Work?

Based on: `course_content/Introduction/how_do_websites_actually_work.txt` · Notes: `.github/my_tasks/concepts/concept_how_do_websites_actually_work.md`

## Problem Statements (With Input Data)

1. **Classify the file.** For each item below, say whether it belongs in an HTML, CSS, or JavaScript file:
   - A paragraph of text
   - A button turning red when clicked
   - A submit button's rounded corners
   - Sending a form's data when "Submit" is clicked
   - An `<img>` tag showing a logo
2. **Predict the render order.** Given a page with HTML, CSS, and JS files, describe what the page would look like if the browser only loaded the HTML file and nothing else (no CSS, no JS). What would be missing?
3. **DevTools edit.** Open `google.com`, right-click the search button, click Inspect, and change its visible label text to your name. Refresh the page. Write down what happened and why.

## Questions and Answers

4. **Define in your own words** (1-2 sentences each, no copy-pasting from the notes):
   - HTML
   - CSS
   - JavaScript
   - Chrome DevTools
5. **Explain the house analogy** in your own words — map HTML, CSS, and JS to three parts of a house that are *not* the ones used in the lesson (bricks/paint/electricity).
6. **Short answer:** Why does editing an element in Chrome DevTools not "hack" the real website for other visitors? What exactly did you change?
7. **Short answer:** What's the difference between an element's visible text and its `aria-label`? Why might a website need both?

## Self Assignments (No Answers)

8. **Inspect three sites.** Pick 3 different websites you use often. On each, inspect one element and identify: (a) the HTML tag, (b) one CSS property affecting it, (c) whether it has any obvious JS-driven behavior (e.g. reacts to a click).
9. **Break a headline.** On a news site's homepage, use DevTools to edit a headline into something absurd. Take a screenshot before refreshing (for your own amusement/reference).
10. **Teach it back.** Explain "how websites work" out loud (or in writing) to someone non-technical, in under 2 minutes, using a house analogy that isn't the one from the lesson.
11. **Connect the lessons.** Write 2-3 sentences linking this lesson to the previous one (What is the Internet) — i.e. describe the full journey from typing a URL to seeing a fully styled, interactive page.

## Self-check

- [ ] I can explain what HTML, CSS, and JS each do without notes.
- [ ] I can predict what a page looks like at each stage (HTML only → +CSS → +JS).
- [ ] I've used Chrome DevTools to inspect and edit a live element myself.
- [ ] I understand why DevTools edits don't persist after a refresh.
