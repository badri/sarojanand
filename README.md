# Saroj Anand — author site

Pen name for the fiction: thrillers and science fiction, Indian settings, global
genre conventions. Non-fiction stays under Lakshmi Narasimhan.

**Domain:** sarojanandbooks.com (the old sarojanand.com expired; sarojanand.page
is also held but unused). The newsletter link printed in the back of *Divya*
points at the bare domain, so the front page must carry a working signup form
before the book goes on sale.

## The books

| Book | Status | Type |
|---|---|---|
| Partners in Crime | Published 2026-05-21, Kindle + wide via Draft2Digital | Psychological thriller, Andaman Islands |
| Divya | Finished, uploading now (KDP first, then Kobo and D2D) | Sci-fi techno-thriller, Chennai |

India print editions of both are still pending.

## Site

Static pages, no build step, no framework. Open any file in a browser to check
a change.

Everything that gets published lives in `public/`. Nothing outside it is
deployed, which is the point: `content/`, `memory/` and the planning notes stay
in the repo but off the public web.

| File | What it is |
|---|---|
| `public/index.html` | Home: Divya hero, intro blurb, both books, latest journal post, newsletter signup |
| `public/books.html` | Full entry per book, with the buy links |
| `public/blog.html` | Journal index |
| `public/posts/*.html` | One file per post |
| `public/about.html` | Bio and contact |
| `public/images/` | Cover art and author photo |

## Deploying

Cloudflare Pages, connected to this GitHub repo. The build settings are:

| Field | Value |
|---|---|
| Production branch | `main` |
| Framework preset | None |
| Build command | *(empty)* |
| Build output directory | `public` |
| Root directory | `/` |

No environment variables. Pushing to `main` deploys.

Keep new publishable files inside `public/`. Anything added at the repo root is
private by construction.

The pages load nothing from a CDN. Everything is served from `public/`:
one compiled stylesheet, self-hosted fonts, and the icons inlined as an SVG
sprite. A visitor fetches about 510 KB, most of it the two photographs, and the
site keeps working if any third party is down or blocked.

### The stylesheet

`public/assets/site.css` is generated, not hand-edited. Its source is
`src/app.css` — Tailwind v4 plus daisyUI 5, with the dark theme declared once in
a `@plugin "daisyui/theme"` block.

```
npm install        # once
npm run build:css  # after changing classes in any page, or the theme
npm run watch:css  # or leave this running while editing
```

**Rebuild and commit `site.css` whenever you add a class that no page used
before.** Tailwind only includes the classes it finds in `public/**/*.html`, so
a brand-new utility will do nothing until you rebuild. Existing classes are
already in the file, so ordinary copy-editing needs no rebuild.

### Icons

Each page carries the same SVG sprite just inside `<body>`, holding every icon
the site uses, so any icon works on any page. Each icon is a
`<svg><use href="#i-name"/></svg>`. To add a new one, copy its paths from
`node_modules/lucide-static/icons/` into the sprite as another `<symbol>` — in
all five pages. There is no icon JavaScript.

### Newsletter (Kit)

The signup form is in the newsletter section of `public/index.html`, the only
form on the site. It posts to Kit form `9942225`
(`https://app.kit.com/forms/9942225/subscriptions`, field `email_address`).
A short script at the bottom of that page submits it in the background and
shows the "Check your inbox" confirmation in place. It handles Kit's three
answers the way Kit's own script does: success, a list of errors shown under
the field, or "quarantined", which sends the reader to Kit's verification page.
If the script can't run, the form still posts normally and Kit shows its own page.

No Kit JavaScript or CSS is loaded. If you switch to a different Kit form, change
the form number in the `action` attribute; nothing else needs to change.

### Store links

| Book | Amazon | Everything else |
|---|---|---|
| Partners in Crime | `amazon.com/…/dp/B0H2HYD75F` | `books2read.com/u/bPq6yl` |

The home page "Buy now" button uses the Books2Read link, because it sends each
reader to their own regional store, Amazon included.

### One gotcha

The shell (head, navbar, footer, sprite) is copy-pasted into each page, because
there is no templating. Change the nav and you change it in five places.

### Adding a post

Copy `public/posts/the-temple-that-shouldnt-exist.html`, replace the title, date,
reading time and body, then add an `<li>` to the list in `public/blog.html` — there is
a comment marking the spot. Update the featured post on `public/index.html` if you want
the new one on the front page.

### Still to do

- Add Divya's store links to `public/books.html` once it is on sale, the same
  way as Partners in Crime: an Amazon button and a Books2Read button.
- When the store opens, look for the `STORE LATER` comments. They mark the rows
  where a price and a buy button drop in without moving anything else.

### Design variations

Three home page directions were built before this one was picked. They are in
git history at commit `0b7b0b2` under `design/`: the dark one that became the
site, a warm-paper editorial one, and a Swiss grid one.

## Other directories

`content/`, `memory/` and `saroj-next-steps.md` are from an earlier plan to run a
Saroj Anand Substack. That plan is dormant; the priority is the books and this
site. Issue tracking is in `bd`.
