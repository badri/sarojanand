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

| File | What it is |
|---|---|
| `index.html` | Home: Divya hero, intro blurb, both books, latest journal post, newsletter signup |
| `books.html` | Full entry per book, with the buy links |
| `blog.html` | Journal index |
| `posts/*.html` | One file per post |
| `about.html` | Bio and contact |
| `images/` | Cover art and author photo |

Styling is Tailwind v4 (`@tailwindcss/browser@4`) plus daisyUI 5, both from a
CDN, with one custom dark theme declared in a `<style type="text/tailwindcss">`
block at the top of every page. Icons are Lucide from a CDN.

**Two gotchas if you edit the pages:**

- The theme block must stay `@theme static`, not `@theme`. Plain `@theme` only
  emits the variables a Tailwind utility on that page happens to use, so a page
  whose only red thing is a daisyUI class like `btn-primary` silently falls back
  to daisyUI's default indigo.
- The shell (head, navbar, footer) is copy-pasted into each page, because there
  is no build step. Change the nav and you change it in five places.

### Adding a post

Copy `posts/the-temple-that-shouldnt-exist.html`, replace the title, date,
reading time and body, then add an `<li>` to the list in `blog.html` — there is
a comment marking the spot. Update the featured post on `index.html` if you want
the new one on the front page.

### Still to do

- Paste the MailerLite embed into `index.html`, inside the
  `<div class="ml-form-embed">` container in the newsletter section, deleting the
  mock form that is in there now. That is the only form on the site; every other
  page links to it, so there is one embed to maintain.
- Fill in the store links on `books.html`. They are `href="#"` today.
- Get cover art for *Partners in Crime*. Its slot on `books.html` is a
  typographic panel standing in for the missing cover.
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
