# IDEC-Wiki

A documentation / static website built with Zola and the `juice` theme (customized). This repository contains the content, templates and theme used to generate a static site.

## Contents

- `config.toml` — site configuration and theme settings
- `content/` — markdown pages and section index files
- `templates/` — site templates (overrides and global templates)
- `themes/juice/` — bundled theme sources
- `static/` & `public/` — static assets and build output

## Quick start (development)

Prerequisites

- Zola installed
- A POSIX shell (examples below use `bash`)

Run development server (live reload):

```bash
zola serve
```

Build for production:

```bash
zola build
```

Generated site will be available in `public/` after build.

## How this project is structured

- Templates and macros
  - `templates/_macros.html` contains `render_header()` used by `templates/index.html`.
  - Customize header/logo/navigation by editing `_macros.html` or the `templates/` files.
- Images and static assets
  - Put site images under `static/images/` and reference them with `get_url(path="images/your.png")` in templates.
- Theme
  - The `themes/juice` directory holds the original theme. Local template overrides live in the top-level `templates/` folder.

## Styling notes

- Tailwind is included via CDN in `templates/index.html` (script: `https://cdn.tailwindcss.com`). For production, consider compiling Tailwind locally to reduce runtime overhead and control the generated utility set.
- Header and sidebar have been adjusted to use Tailwind utility classes. If you change header height, update the `.hero` padding (or implement JS to compute it dynamically) to avoid content overlap.

## Common edits

- Change the logo or name: edit `config.toml` keys referenced by `_macros.html` (`config.extra.juice_logo_path` & `config.extra.juice_logo_name`).
- Add/modify nav menu: edit `config.extra.juice_extra_menu` in `config.toml` or the template logic in `_macros.html`.
- Fix image URL issues: avoid spaces in filenames (use `-` or `_`) so browsers don't percent-encode paths.

## Deploy

- Build (`zola build`) and deploy the content of the `public/` folder to your static host (Netlify, Vercel, GitHub Pages, etc.).

## Extras & suggestions

- Replace Tailwind CDN with a local build for production to reduce third-party requests and remove unused utilities.
- Implement responsive/accessible navigation (mobile menu) inside `templates/_macros.html` and add minimal JS for toggle.
- Rename any image files with spaces to use dashes to avoid encoding confusion.

## License

The repository inherits the theme license where applicable. Check `themes/juice/LICENSE` for the theme license.

If you want, I can:

- Add a small `Makefile` or `package.json` scripts to standardize dev/build tasks.
- Implement a mobile hamburger menu and dynamic header-height JS.
