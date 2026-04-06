# Robot Amateur Site

Hugo source for the Robot Amateur website (projects, videos, diagrams, and code resources).

## Project Structure

- `content/` - all site content (sections and pages)
- `layouts/shortcodes/` - reusable content snippets used by markdown files
- `static/` - static assets served as-is (images, PDFs, icons)
- `themes/PaperMod/` - PaperMod theme submodule (do not edit theme internals here)
- `hugo.toml` - site configuration

## Local Development

```bash
hugo server -D
```

## Production Build

```bash
hugo
```

Generated files go to `public/` and are ignored by git.

## Deploy (CI → `gh-pages`, recommended)

This repo includes [`.github/workflows/hugo-pages.yml`](.github/workflows/hugo-pages.yml). On every push to **`main`** or **`master`**, GitHub Actions runs **Hugo Extended**, builds into `public/`, and pushes the result to the **`gh-pages`** branch (using [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages)).

**Repository layout**

- **`main`** (or `master`): Hugo **source** only — what you edit and push day to day.
- **`gh-pages`**: **built site** only — updated by the workflow; do not edit by hand.

**One-time GitHub settings** ([`robotamateur123.github.io`](https://github.com/robotamateur123/robotamateur123.github.io))

1. **Settings → Pages → Build and deployment:** source **Deploy from a branch**, branch **`gh-pages`**, folder **`/`** (root).
2. **Settings → Actions → General → Workflow permissions:** **Read and write** (so the workflow can push to `gh-pages`).

**Publish changes**

```bash
git push origin main
```

Then check **Actions** for a green **“Build Hugo and deploy to gh-pages”** run. The live site is [https://robotamateur123.github.io/](https://robotamateur123.github.io/).

**If the remote only had `gh-pages` before:** create `main` from this full project (including `.github/`, submodule `themes/PaperMod`), push `main`, and leave `gh-pages` for CI to overwrite.

## Content Authoring Notes

- Add new playlist/section landing pages as `content/<section>/_index.md`.
- Use the `youtube-responsive` shortcode for embeds to keep markup consistent:
  - `{{< youtube-responsive id="VIDEO_ID" >}}`
  - `{{< youtube-responsive id="VIDEO_ID" query="si=..." >}}`
- Keep all downloadable files in `static/` and link them with root-relative paths (for example `/play-with-arduino/pdf/file.pdf`).
- For the **Beginner Robotics Projects** section (content path `DIY-robotic-arm`), put PDFs/ZIPs under `static/diy-robotic-arm/downloads/` and link as `/diy-robotic-arm/downloads/yourfile.pdf`.

## Portfolio (home & `/projects/`)

The home page and `/projects/` use the `portfolio` layout. Project cards are built from all regular pages under the sections listed in `hugo.toml` → `params.portfolioSections`. On those pages, **Playlist** links (**All** / each section) navigate to the right list: **All** stays on home or `/projects/`, and each playlist opens that section’s page (for example `/play-with-arduino/`), which Hugo renders with only that folder’s projects—no JavaScript required.

For each project page, optional front matter:

- `date` — sort order (newest first).
- `description` — short blurb on the card (falls back to summary).
- `params.youtube` — video ID; card uses the YouTube thumbnail and a play overlay.
- `cover.image` — path under `static/` (root-relative, e.g. `/play-with-arduino/images/photo.jpg`); shown on the card and on the post page via PaperMod.
