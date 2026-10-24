# Wilson Lab website

Source for [klwilson.org](https://klwilson.org), built with [Quarto](https://quarto.org) and published to GitHub Pages automatically whenever changes are pushed to `main`.

## Quick edits (no install needed)

You can make most changes directly on GitHub: open a file, click the pencil icon, edit, and commit. The site rebuilds in about two minutes (watch progress under the **Actions** tab).

| To change... | Edit this file |
|---|---|
| Lab members | `people/people.yml` |
| Alumni | `people/alumni.yml` |
| Publications | `papers/papers.yml` |
| A project | `research/projects/<project>.qmd` |
| Homepage text or featured project | `index.qmd` |
| Openings for students | `prospective-students/index.qmd` (the "Current openings" box) |
| Links and course materials | `resources/index.qmd` |
| Navigation menu and footer | `_quarto.yml` |
| CV | Replace `files/wilson-cv.pdf` (keep the same filename) |
| Colours and fonts | `assets/theme.scss` |

### Add a lab member
Add an entry to `people/people.yml`:

```yaml
- name: Jane Doe
  group: grad            # pi | postdoc | grad | undergrad
  role: PhD student
  focus: Rockfish life histories on the Central Coast
  photo: images/jane-doe.jpg   # optional; square, about 400px. Put the file in people/images/
  links:
    - label: Website
      url: https://example.com
```

When someone graduates, move them to `people/alumni.yml`.

### Add a paper
Add an entry to `papers/papers.yml`. Wrap lab members in `**double asterisks**` to bold them.

```yaml
- year: 2026
  title: "Title of the paper"
  authors: "**Doe J**, Smith A, **Wilson KL**"
  journal: "Canadian Journal of Fisheries and Aquatic Sciences 83: 1–15"
  doi: "10.1139/cjfas-2026-0000"
  code: https://github.com/klwilson23/repo-name   # optional
  open_access: true                                 # optional
  topics: [salmon, people]   # salmon, groundfish, freshwater, people, theory
```

### Add a news post
1. Copy a folder in `news/posts/`, e.g. `2026-09-15-new-website`.
2. Rename it `YYYY-MM-DD-short-title`.
3. Edit the `index.qmd` inside: change `title`, `description`, `date`, and the text.
4. Optional: add a photo to the folder and set `image: photo.jpg` for a thumbnail.

The three newest posts appear on the homepage automatically.

### Add a project
Copy a file in `research/projects/`, rename it, and edit the front matter (`title`, `description`, `system`, `partners`, `order`) plus the header block and text. It appears on the Research page and homepage automatically.

## Where files go

| File | Folder | How to link it |
|---|---|---|
| CV | `files/wilson-cv.pdf` | Already linked in the menu, on your People profile, and from the old `/curriculum-vitae/` address |
| Paper PDFs | `files/papers/` | `pdf: ../files/papers/name.pdf` in `papers/papers.yml` |
| Headshots | `people/images/` | `photo: images/name.jpg` in `people/people.yml` |
| Project figures | `research/projects/images/` | `![Caption.](images/name.jpeg)` in the project page |
| News photos | the post's own folder | `![Caption.](photo.jpg)` in the post, plus `image: photo.jpg` for a thumbnail |
| Hero backdrop and homepage photo strip | `assets/images/` | See the "Photos on the homepage" section below |

Keep individual files well under 50 MB. Resize photos to about 400 px (headshots) or 1,600 px wide (figures and news photos). If you add a new top-level folder for files, list it under `resources:` in `_quarto.yml` so it gets published.

## Photos on the homepage

**Hero backdrop.** Put a landscape photo in `assets/images/` (about 2000 px wide, under ~500 KB) and point line 23 of `index.qmd` at it:

```html
<header class="hero has-photo" style="background-image:url('assets/images/field-hero.jpg'); --hero-pos:60% 50%">
```

`--hero-pos` shifts which part of the photo stays visible behind the headline, like `background-position`: the first number is horizontal (0% left, 100% right), the second vertical. A dark overlay keeps the headline readable and lets the river network draw over the photo. To go back to a plain dark hero, remove `has-photo` and the `style` attribute.

**Photo strip.** The "From the field" section on the homepage holds four photos (about 1200 px wide each). Edit the `<figure>` blocks in `index.qmd` to change the files, alt text, and captions. Add `class="tall"` to a figure for a portrait crop. Delete the whole section if you don't want it.

Always write real alt text describing the photo, and get permission before posting photos of people or of work on partners' territories.

## Working locally (recommended for bigger changes)

1. Install [Quarto](https://quarto.org/docs/get-started/) (RStudio already includes it).
2. Clone this repository and open the folder in RStudio or VS Code.
3. Run `quarto preview` in the terminal. The site opens in your browser and refreshes as you edit.
4. Commit and push to `main` to publish.

## One-time GitHub setup

1. Settings → Pages → **Source: GitHub Actions**.
2. Settings → Pages → **Custom domain: klwilson.org**, then save.
3. Point the domain's DNS at GitHub Pages (four A records to 185.199.108.153, .109.153, .110.153, .111.153, and a `www` CNAME to `klwilson23.github.io`).
4. Once the DNS check passes, tick **Enforce HTTPS**.

Old WordPress addresses `/current-projects/` and `/publications/` redirect to the new Research and Papers pages.
