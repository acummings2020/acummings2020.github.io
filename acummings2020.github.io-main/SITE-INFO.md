# SITE-INFO — your personal cheat sheet

This is **not** a page on the site. It's a note-to-self covering everything
you'll ever want to change. Every "how do I..." lives here.

The file is excluded from the built site via `_config.yml` (see the
`exclude:` list), so nothing here leaks to the public.

---

## 1. Who you are (name, tagline, links)

Edit **`_config.yml`**. Everything visible on the site — your name, tagline,
description, email, GitHub handle — reads from this one file. Change a value,
push, done. Fields to know:

| Field                  | Where it shows                        |
| ---------------------- | ------------------------------------- |
| `title`                | Browser tab, header, RSS feed         |
| `tagline`              | (Available via `{{ site.tagline }}`)  |
| `description`          | Google snippet, link previews         |
| `author.name` / `email`| Footer, RSS feed, mailto link         |
| `social.*`             | Footer links — blank ones are hidden  |

---

## 2. Attaching your CV

1. Save your CV as PDF, name it exactly **`cv.pdf`** (lowercase).
2. Drop it in the **`/assets/`** folder.
3. Commit + push.

The download button on `/cv/` points to `/assets/cv.pdf` already — no code
change needed. If you rename the file, update the link inside `cv.md`.

You can also edit the text of the CV page itself (`cv.md`) — I've laid out
sections for Summary, Experience, Education, Skills, Contact. Nothing there
is required; delete what doesn't apply.

---

## 3. Writing a blog post

Create a new file inside **`_posts/`** named:

    YYYY-MM-DD-short-title-in-dashes.md

⚠️ **Dashes only** — no underscores, no spaces, no capitals. Jekyll silently
ignores posts that don't follow this pattern. (That's why the old
`2023_03_29_REVAMP.md` never appeared.)

Every post starts with front-matter:

```markdown
---
layout: post
title: "A friendly title readers will actually click"
date: 2026-07-01
---

Write your post in Markdown here. Headings with `##`, links with `[text](url)`,
code with backticks, images with `![alt](/assets/images/foo.png)`.
```

Save, commit, push. It appears on `/blog/` automatically.

### Tips for the mixed audience (practitioners + friends + newcomers)
- Open every post with a **one-sentence summary a non-technical friend
  could read.**
- Use `> blockquotes` for "if you already know this, skip ahead" notes.
- Put a "Why this matters" section near the top. Save the math for the end.

---

## 4. Changing colors, fonts, spacing

Open **`css/main.css`** and scroll to the top block (`:root { ... }`). That's
the control panel — every color and font on the site comes from a variable
there. Change **one value** and it propagates everywhere.

Common tweaks:

| I want to...                        | Change...                     |
| ----------------------------------- | ----------------------------- |
| Different accent color for links    | `--color-accent` (and its `-hover` twin) |
| Slightly larger text overall        | `--font-size-base: 18px;`     |
| Wider reading column                | `--content-max-width: 46em;`  |
| Serif font for headings             | `--font-heading: Georgia, ...`|
| Kill dark mode entirely             | Delete the `@media (prefers-color-scheme: dark)` block |

Accent color ideas that work for a data-sciencey vibe:

- Teal `#0f766e` (current)
- Indigo `#4338ca`
- Slate blue `#2b6cb0`
- Burgundy `#9f1239`
- Forest `#166534`

---

## 5. Changing the layout / adding pages

- Add a new **top-level page** by creating a `.md` file at the repo root
  with `layout: default` and a `permalink:` in front-matter (see `about.md`).
- Add a new **nav link** by editing the `<ul>` inside
  `_layouts/default.html` (the section marked "Site header").
- Change **what wraps every page** by editing `_layouts/default.html`.
- Change **how posts look** by editing `_layouts/post.html`.

Every layout file has line-by-line comments — read them before changing.

---

## 6. Previewing locally (optional)

You don't have to — GitHub Pages will rebuild automatically on push. But if
you want to see changes before pushing:

```bash
# One-time setup (needs Ruby installed):
gem install bundler jekyll

# From the repo folder:
jekyll serve
# then open http://localhost:4000
```

---

## 7. Deployment

Push to `main` (or whatever your default branch is). GitHub Pages rebuilds
within a minute or two. If a build fails, GitHub will email you and show
the error under the repo's **Actions** tab.

---

## 8. Files in this repo, at a glance

```
_config.yml            site-wide settings (edit here first)
_layouts/
  default.html         header/nav/footer wrapper
  post.html            wraps every blog post
_posts/                blog posts, one .md file each
about.md               About page  → /about/
cv.md                  CV page     → /cv/
index.html             Home page   → /
blog/
  index.html           Blog index  → /blog/
  atom.xml             RSS feed    → /blog/atom.xml
css/
  main.css             all styling (CSS variables at top)
assets/                CV PDF, images, downloadable files
SITE-INFO.md           this file (excluded from build)
README.md              GitHub repo landing (excluded from build)
```

---

## 9. Common mistakes

- **New post not showing** — filename doesn't match `YYYY-MM-DD-title.md`
  (dashes, no underscores, lowercase), OR the `date:` in front-matter is
  in the future.
- **Link is broken locally but works on GitHub** — use `{{ '/path' |
  relative_url }}` in HTML/layouts instead of hardcoding `/path`.
- **Site looks unstyled** — you probably broke `<head>` in `default.html`,
  which prevents the CSS link from loading. Compare against the version I
  wrote.
