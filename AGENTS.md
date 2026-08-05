# Agent Memory - Learning Context

## Who I am
- Name: Selva (Jothis)
- Background: Automation tester with Selenium Java, API Testing, Cypress, JavaScript
- Goal: Learn full stack web development from scratch — frontend, backend, databases, and deployment
- Editor: (not specified yet)

---

## My Learning Workflow
Every new lesson follows this exact pattern - always follow it proactively:

1. **Digest** → Read the lesson transcript in `course_content/<Topic>/`, and discuss/explain the material with a problem-first approach, connecting it to concepts already covered
2. **Concepts** → Save full revision notes to `.github/my_tasks/concepts/concept_<lesson>.md`
3. **Tasks** → Create practice tasks (Problem Statements + Q&A + Self Assignments) to `.github/my_tasks/tasks/<lesson>_tasks.md`
4. **Quick Notes** → Append one-liner summary to `.github/my_notes.txt` under `Topic: <TopicName>`

`course_content/` is source material (raw lesson transcripts) and is never edited by the agent.

---

## File Structure
```
.github/
    my_notes.txt                              # Quick revision - one-liners per lesson
    my_tasks/
        concepts/
            concept_what_is_internet.md       # Full revision notes: what is the Internet
        tasks/
            what_is_internet_tasks.md         # Practice tasks: what is the Internet
course_content/
    Introduction/
        what_is_internet.txt                  # Raw lesson transcript (source, not edited)
AGENTS.md                                     # This file - agent memory
CLAUDE.md                                     # Pointer to AGENTS.md, kept in sync
```

---

## Topics Completed

### Phase 1: Web Fundamentals
- [x] What is the Internet — client/server, ISP, DNS, IP addresses
- [x] How websites actually work — HTML/CSS/JS roles, browser render order, Chrome DevTools
- [ ] HTTP methods, status codes, headers
- [ ] Domain names, hosting, and web servers

### Phase 2: Frontend
- [ ] HTML — structure, semantic tags, forms
- [ ] CSS — selectors, box model, flexbox, grid, responsive design
- [ ] JavaScript fundamentals — variables, functions, DOM manipulation, events
- [ ] Frontend frameworks (e.g. React) basics

### Phase 3: Backend
- [ ] Node.js fundamentals
- [ ] Building APIs (e.g. Express) — routing, middleware, REST principles
- [ ] Authentication and authorization basics

### Phase 4: Databases
- [ ] Relational databases (SQL) — schema design, queries, joins
- [ ] Non-relational databases (NoSQL, e.g. MongoDB)
- [ ] ORMs and connecting a backend to a database

### Phase 5: Full Stack Integration & Deployment
- [ ] Connecting frontend to backend (fetch/AJAX, full CRUD app)
- [ ] Version control workflows (Git/GitHub) for full projects
- [ ] Testing a full stack app
- [ ] Deploying frontend + backend + database to the cloud

---

## Teaching Style Preferences
- Always start with **problem statement first** (why do we need this)
- Use **real-world web/automation context** where it helps (e.g. relate backend APIs to the API testing already known from Cypress/Selenium work)
- Keep examples practical and beginner-friendly — favor clear explanations over terse answers
- Prefer well-commented, beginner-friendly code over clever/compact code
- Connect new topics back to ones already covered in `course_content/`
- After explaining a lesson, proactively offer to create the concept file + task file + update quick notes
- Format tasks file with 3 sections: Problem Statements (With Input Data), Questions and Answers, Self Assignments (No Answers)
- Format concept file with numbered/headed sections matching `concept_what_is_internet.md` style

---

## Key Concepts Already Explained (with extra detail)
- **Client vs Server**: Server = always-on computer that stores/serves data on request; Client = the device (browser) making the request.
- **ISP (Internet Service Provider)**: the company (AT&T, Comcast, BT, TalkTalk, etc.) that connects you to the Internet and relays your requests.
- **DNS (Domain Name System)**: a "phone book" that translates human-readable domain names (`google.com`) into IP addresses.
- **IP address**: a unique numeric identifier ("postal code") for every device connected to the Internet.
- **Request flow**: Browser → ISP → DNS server (resolves IP) → Browser requests directly from that IP → server responds with page data.
- **Physical Internet**: undersea fiber-optic cables physically connect continents, carrying data via lasers at very high speeds (see submarinecablemap.com).
- **HTML/CSS/JS roles**: HTML = content (bricks), CSS = styling (paint), JavaScript = functionality (electricity/appliances) — house analogy.
- **Browser render order**: HTML loads first (raw content) → CSS applied (styled) → JavaScript runs (interactive).
- **Chrome DevTools**: Right-click → Inspect opens live HTML/CSS view; edits are local-only and reset on refresh since the browser re-fetches the real files from the server.
