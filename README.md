<<<<<<< HEAD
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

## Content Authoring Notes

- Add new playlist/section landing pages as `content/<section>/_index.md`.
- Use the `youtube-responsive` shortcode for embeds to keep markup consistent:
  - `{{< youtube-responsive id="VIDEO_ID" >}}`
  - `{{< youtube-responsive id="VIDEO_ID" query="si=..." >}}`
- Keep all downloadable files in `static/` and link them with root-relative paths (for example `/play-with-arduino/pdf/file.pdf`).
=======
# robot_amateur_site
All the code used to create website for my youtube channel.
>>>>>>> 9c495b007152b4d3e0206ecdade267c226ca8f83
