# Practice Tasks: What is the Internet?

Based on: `course_content/Introduction/what_is_internet.txt` · Notes: `.github/my_tasks/concepts/concept_what_is_internet.md`

## Warm-up (no coding required)

1. **Trace a request.** Pick a website you use daily. Write down, in your own words, the full journey from typing the URL to the page appearing on screen — mention the browser, ISP, DNS server, and IP address.
2. **Look up an IP address.** Go to [nslookup.io](https://nslookup.io), look up 3 different websites (e.g. `google.com`, `github.com`, a site of your choice). Record their IP addresses.
3. **Visit an IP directly.** Take one of the IP addresses you found and paste it straight into your browser's address bar. What happens? Does it always load the same site? (Hint: think about why it might *not* for some sites — this hints at a concept called virtual hosting, which you don't need to explain yet, just observe.)
4. **Explore the physical Internet.** Visit [submarinecablemap.com](https://submarinecablemap.com) and find a cable that connects to your country/region. Note its name and which other countries it connects to.

## Check your understanding

5. **Define in your own words** (1-2 sentences each, no copy-pasting from the notes):
   - Client
   - Server
   - ISP
   - DNS
   - IP address
6. **Explain the difference** between a Client and a Server using an analogy that is *not* the "library" one used in the lesson.
7. **Short answer:** Why do we need DNS at all? What would browsing the web be like without it?

## Applied / stretch

8. **Diagram it.** Without looking at the notes, draw (on paper or in a tool like Excalidraw) the full request flow from browser → ISP → DNS → server → back to browser. Compare it against the diagram in `my_notes/Introduction/what_is_internet_notes.md` afterward.
9. **Command line DNS lookup.** If you have access to a terminal, try running `nslookup google.com` (or `dig google.com` on Mac/Linux). Compare the result to what nslookup.io showed you.
10. **Teach it back.** Explain "what is the Internet" out loud (or in writing) to someone with no technical background, in under 2 minutes, without using the word "cloud."

## Self-check

- [ ] I can explain client vs. server without notes.
- [ ] I understand what role DNS plays and why it's needed.
- [ ] I know what an IP address is and looked one up myself.
- [ ] I can describe the full request flow from memory.
