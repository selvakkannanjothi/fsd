# What is the Internet?

## The core idea

The Internet is **not** a mysterious cloud — it's essentially a giant network of wires connecting computers all over the world, so they can send data to each other.

- Two computers (e.g. one in London, one in Seattle) are connected by wire and can transfer data between them.
- Scale that up to *all* computers in the world, and that's the Internet.
- Between continents, this is literally true: massive **undersea fiber-optic cables** connect land masses (see submarinecablemap.com). Each cable has hundreds of fibers, using lasers to send up to 400 gigabytes/second.

## Key roles: Client vs Server

| Term | What it is |
|---|---|
| **Server** | A computer that's online 24/7, whose job is to store and "serve" data/files (e.g. a website) whenever someone requests them. |
| **Client** | Any computer a user uses to access the Internet (e.g. your laptop, phone). |

Think of a server as a library that's always open — you ask for a specific book (webpage) and it hands it over.

## The problem: finding things in a huge "library"

With millions of servers/websites out there, how does your browser know exactly where to find `google.com`? This is solved with **DNS**.

## How loading a website actually works (step by step)

1. You type `google.com` into your browser.
2. Your browser sends that request to your **ISP** (Internet Service Provider) — the company you pay for internet access (e.g. AT&T, Comcast, BT, TalkTalk).
3. Your ISP forwards the request to a **DNS server** (Domain Name System server) — essentially a phone book for the Internet.
4. The DNS server looks up `google.com` and finds its **IP address** — a unique numeric "postal code" that every device on the Internet has.
5. The DNS server sends that IP address back to your browser (via the ISP).
6. Your browser now makes a **direct request** to that IP address.
7. The server living at that IP address (Google's servers) sends back all the files/data needed to render the Google homepage.

```
You type google.com
      │
      ▼
   Browser ──► ISP ──► DNS Server (looks up IP address)
      ▲                      │
      │                      ▼
      └────── IP address returned
      │
      ▼
 Browser requests page directly from that IP
      │
      ▼
 Google's servers respond with the page data
```

## Key terms glossary

- **ISP (Internet Service Provider)**: the company that connects you to the Internet.
- **DNS (Domain Name System)**: translates human-readable domain names (`google.com`) into machine-readable IP addresses.
- **IP address**: a unique identifier/address for every device connected to the Internet.
- **Server**: a computer that stores and serves data/files on request.
- **Client**: the device used to request/access that data.

## Try it yourself

- Look up a site's IP address: [nslookup.io](https://nslookup.io) → type in a domain like `google.com`.
- You can paste the resulting IP address directly into your browser's address bar and it should load the same site.
- Explore undersea cables connecting the world: [submarinecablemap.com](https://submarinecablemap.com)

## Why this matters going forward

Understanding client/server + DNS + IP addresses is the foundation for the next step: understanding **how websites themselves work**, before building our own.
