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
- **Content:** `content/` — Markdown files organized by section (currently `projects/`)
- **Theme:** `themes/PaperMod/` — git submodule, no local overrides yet
- **Overrides:** To customize theme templates, copy from `themes/PaperMod/layouts/` into `layouts/`; same for `assets/` and `static/`
- **Archetypes:** `archetypes/default.md` — template for `hugo new` commands
- **CI/CD:** `.github/workflows/hugo.yml` — builds and deploys on push to `main`
- **Domain:** `CNAME` file maps to briancarroll.cool

## Content Conventions

Front matter uses TOML (`+++`) format. New content starts as `draft = true` — remove or set to `false` to publish. The site uses home-info mode for the landing page (configured in `hugo.toml` under `[params.homeInfoParams]`).
