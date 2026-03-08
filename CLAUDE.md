# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal website for briancarroll.cool — a Hugo static site using the PaperMod theme (git submodule). Deployed to GitHub Pages via GitHub Actions on push to `main`.

## Build & Development Commands

```bash
# Local dev server with drafts
hugo server -D

# Production build (matches CI)
hugo --minify

# Create new content
hugo new projects/my-project.md
```

Hugo version: 0.147.6 (extended). No npm/node dependencies.

## Architecture

- **Config:** `hugo.toml` — all site settings, menu, social icons, PaperMod params
- **Content:** `content/` — Markdown files organized by section: `projects/`, `presentations/`, `transcripts/`, `paris/`, `jcc-articles/`, plus standalone `book.md` and `music.md`
- **Theme:** `themes/PaperMod/` — git submodule
- **Shortcodes:** `layouts/shortcodes/button.html` — styled external link button
- **Overrides:** To customize theme templates, copy from `themes/PaperMod/layouts/` into `layouts/`; same for `assets/` and `static/`
- **Images:** `static/images/presentations/` (thumbnails), `static/images/paris/` (78 travel photos)
- **Archetypes:** `archetypes/default.md` — template for `hugo new` commands
- **CI/CD:** `.github/workflows/hugo.yml` — builds and deploys on push to `main`
- **Domain:** `CNAME` file maps to briancarroll.cool

## Content Conventions

Front matter uses TOML (`+++`) format. New content starts as `draft = true` — remove or set to `false` to publish. The site uses profile mode for the landing page (configured in `hugo.toml` under `[params.profileMode]`). Presentations use `weight` for ordering and `cover.image` for list thumbnails. Paris blog uses `weight` for day ordering. YouTube embeds use Hugo's built-in `{{< youtube ID >}}` shortcode.
