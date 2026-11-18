# FindIt – Campus Retrieval System

A privacy-preserving lost-and-found website for campus. This repository holds the **UI/UX prototype**: a 60-page desktop website built with **pure HTML and CSS** (no JavaScript, no build step).

> Project report: *Campus Retrieval System (FindIt)* – B.Tech CSE, Career Point University, Kota (July – Dec 2026)
> Author: Sujal Singh Hada (K28280)

**Live demo:** `https://<your-username>.github.io/<repo-name>/` (see [Deploy](#deploy-with-github-pages))

---

## The idea

Campus lost-and-found usually happens in public group chats, where people post phone numbers and anyone can claim an item. FindIt fixes this with three rules:

1. **One searchable place** for every lost and found report, filtered by campus zone and category.
2. **Verify before contact.** The finder sets a secret question. The owner gets three attempts to answer it.
3. **Masked handover.** Finder identity and phone numbers stay hidden. Chat happens in-app and ends at a campus security point.

## Pages and user flow

| Module | Pages | What it shows |
|---|---|---|
| Landing | `index.html` | Hero, stats, recent items, how it works, verification preview |
| MOD-01 Discover | `feed.html`, `search.html` | Filter sidebar (zone, category), Lost/Found switch, card grid, search results |
| MOD-02 Rapid Post | `post-1.html` → `post-1b.html` → `post-2.html` → `post-3.html` → `post-4.html` | 3-step report wizard with live preview and AI-suggestion state |
| MOD-03 Item Inspector | `item-1.html` … `item-8.html` | Item hero, campus map, masked finder, claim panel, similar items |
| MOD-04 Verification Gatekeeper | `claim-N.html`, `claim-N-wrong.html`, `claim-N-locked.html`, `claim-N-ok.html` | Question, wrong answer, locked, verified states (N = 1–8) |
| MOD-05 Secure Chat | `chat-1.html` … `chat-8.html`, `chats.html`, `returned.html` | Masked messenger, safe exchange points, item returned |
| Help | `about.html`, `design-system.html` | Step explainer with FAQ, colour, type and component reference |

Suggested walkthrough: **Home → Discover → open an item → Claim → Verify → Open secure chat → Mark as returned.**

## How it works without JavaScript

| Feature | Technique |
|---|---|
| Lost/Found, zone and category filters | Hidden radio inputs plus the CSS `:has()` selector hide non-matching cards |
| Active filter highlight | `:has(#id:checked)` rules on the sidebar labels |
| Search | A plain `GET` form that opens `search.html` |
| Wizard and claim states | Each state is its own linked page |
| FAQ accordion | Native `<details>` / `<summary>` |
| Animation | CSS `@keyframes` and transitions |
| Icons | Inline SVG sprite reused with `<use>` |

## Design

- Material Design 3 dark theme with CSS custom properties.
- Key colours: surface `#141218`, primary `#d0bcff`, lost `#ff8a80`, found `#34d399`.
- Desktop-first (1240 px content width); reflows for tablets and 390 px phones.
- Status is shown by text as well as colour. Key colour pairs measured at 4.5:1 or better (WCAG AA).
- The full token and component list is on `design-system.html`.

## Run locally

No install is needed. Download or clone the repo and open `index.html` in a modern browser.

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
# open index.html in your browser
```

To serve it instead: `python3 -m http.server 8000` and visit `http://localhost:8000`.

## Deploy with GitHub Pages

1. Put the files at the **root** of the repository (so `index.html` sits at the top level).
2. Open **Settings → Pages**.
3. Under *Build and deployment*, choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. After a minute or two the live link appears at the top of the Pages screen.

All internal links are relative, so the site works under the `/<repo-name>/` path. A Vercel import (framework preset "Other") also works.

## Browser support

The filters use the CSS `:has()` selector, supported by current Chrome, Edge, Safari and Firefox. In older browsers the feed shows all items unfiltered.

## Limitations of this prototype

- Data is static: eight seeded items are written into the pages, and posting a new item does not add it to the feed.
- The gatekeeper does not judge the typed answer. **Verify answer** always opens the verified page, and a labelled "Prototype shortcut" link shows the wrong-answer and locked states.
- The AI suggestion is a designed state, not a live model call.
- There is no sign-in; claims and chats are not tied to accounts.
- The campus map in the Discover sidebar is a fixed example.

## Planned production architecture (design only, not built)

React Native or Flutter client, Node.js service, Supabase (PostgreSQL with Row-Level Security) and the Gemini API for image tagging and answer validation. The proposed schema and policies are in the project report.

## Repository layout

```
index.html            landing page
feed.html  search.html
post-1.html … post-4.html   (plus post-1b.html)
item-1.html … item-8.html
claim-N*.html         verification states
chat-1.html … chat-8.html  chats.html  returned.html
about.html  design-system.html
web.css               all design tokens and components
```

## Credits

- Design language: Google Material Design 3.
- Built as a B.Tech CSE project at Career Point University, Kota.
