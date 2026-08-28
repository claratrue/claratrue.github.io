# clarathomas.site

An academic site built with [Quarto](https://quarto.org). Minimal,
near-monochrome, five pages.

## Files you'll actually touch

| File | What it is |
|---|---|
| `index.qmd` | **Home** — name, affiliations, short intro. |
| `research.qmd` | **Research** — projects, publications, presentations, funding. |
| `about.qmd` | **About** — background, community work, tools. |
| `cv.qmd` | **CV** — full CV, styled to match. |
| `fieldnotes/index.qmd` | **Fieldnotes** — the blog listing page. |
| `fieldnotes/posts/` | One folder per post. |
| `theme.scss` | Colors, fonts, spacing. Palette is at the top. |
| `_quarto.yml` | Site config — nav links, title, description, favicon. |
| `references.bib` | Optional BibTeX, if you switch publications to auto-citations. |
| `cv.pdf` | The printable CV, generated from `cv.qmd` — see below. |

Everything in `_site/` is generated — never edit it, never commit it.

## First-time setup

1. Install Quarto: <https://quarto.org/docs/get-started/>
   (It's a normal installer. No R or Python needed unless you want code chunks.)

2. Open Terminal and `cd` into **this folder** — the one containing this README
   and `_quarto.yml`. Every Quarto command below runs from here.

   ```bash
   cd ~/Downloads/site      # or wherever you put it
   ```

   Shortcut: type `cd ` (with a space), then drag the folder from Finder into
   the Terminal window — it fills in the path for you.

   To confirm you're in the right place, `ls` should show `_quarto.yml`,
   `index.qmd`, `cv.qmd`, and `theme.scss`. If it doesn't, you're one level too
   high or too low.

3. Start the live preview:

   ```bash
   quarto preview
   ```

   A browser opens at `localhost:4000` and live-reloads as you save. This is the
   way to work — leave it running while you edit. `Ctrl-C` stops it.

4. When you're done: `quarto render` writes the finished site to `_site/`.

## Filling in the placeholders

Everything needing your input is marked `PLACEHOLDER` or in `[BRACKETS]`.
Search the file for those two strings and you'll find all of them.

- **Affiliations** — the stacked lines under your name, in `.affil`. Add or
  remove `<div>` lines freely. `<div class="sep"></div>` inserts a small gap.
- **Projects** — each is an `### [Title](url)` plus a `.note` line. Add or delete
  list items; the hairline dividers handle themselves.
- **Publications** — hand-written for now, which is the least friction at your
  publication count. See below to switch to BibTeX.
- **CV** — lives in `cv.qmd`, already filled in from your Word CV. Each entry is
  a `.cv-item` with three lines: `.org` (bold), `.role` (italic), `.when` (date).
  Copy an existing block to add a new one.

## Keeping cv.pdf current

`cv.pdf` is the printable version, and it's generated from `cv.qmd` — so you
update the CV in one place, not two. After editing:

1. `quarto render`
2. Open `_site/cv.html` in your browser
3. Cmd-P → **Save as PDF**, margins Default, **uncheck** headers/footers
4. Save over `cv.pdf` in this folder

The print stylesheet handles the rest — the back-link and footer are hidden,
type sizes drop, and entries won't split across pages. A fresh `cv.pdf` is
already included.

## Switching publications to BibTeX

When the hand-written list gets tedious:

1. Export your library to `references.bib`.
2. Download a style (e.g. Ecology) from <https://www.zotero.org/styles> into this
   folder and uncomment the `csl:` line in `_quarto.yml`.
3. Replace the publications section with `::: {#refs}` and add
   `nocite: |\n  @*` to the frontmatter to list everything.

## Writing a Fieldnotes post

One folder per post, each containing an `index.qmd`:

```
fieldnotes/posts/2026-09-04-my-post-title/index.qmd
```

The folder name is only for your own organisation — the date shown on the site
comes from the frontmatter. Start each post with:

```yaml
---
title: "Your title here"
description: "One sentence — this is what shows on the listing page."
date: 2026-09-04
---
```

Then write in markdown below it. Posts appear on the Fieldnotes page
automatically, newest first — there's no index to update.

An example post is already in there (`2026-08-11-dawn-chorus/`). Delete it once
you've written a real one.

**Figures from code.** Because this is Quarto, a post can run R or Python and
embed the result:

````
```{r}
#| label: fig-detections
#| fig-cap: "Detections per hour at one site."
#| echo: false

library(ggplot2)
# your code here
```
````

Set `echo: true` to show the code alongside the figure. Note this requires R (or
Python) installed locally — plain markdown posts don't.

## Changing the navigation

The five tabs are defined in `_quarto.yml` under `navbar: right:`. Each is two
lines:

```yaml
      - href: research.qmd
        text: Research
```

Reorder, rename, or delete entries there. To add a page, create `newpage.qmd`
alongside the others and add an entry pointing at it.

## Publishing

**GitHub Pages** — free, and the usual choice for an academic site.

```bash
quarto publish gh-pages
```

That's the whole deployment. It builds, pushes to a `gh-pages` branch, and gives
you a `username.github.io/repo` URL. Re-run it any time you want to update.

**Netlify** — if you'd rather drag-and-drop or auto-deploy from git:

```bash
quarto publish netlify
```

**Custom domain** — buy the domain anywhere (Namecheap, Cloudflare, ~$12/yr),
then point it at your host. On GitHub Pages that's a `CNAME` record plus the
domain entered in the repo's Pages settings. HTTPS is automatic and free.

## Notes

- Fonts are Newsreader (serif body) and Inter (small caps labels), loaded from
  Google Fonts in `_extra/fonts.html`. Swap them there.
- The page has a print stylesheet — Cmd-P gives a clean one-sheet profile.
- The favicon is a small SVG waveform in `images/`.
