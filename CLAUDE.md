# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SlightlyTofu (有点豆腐) — a Jekyll-powered website for a Chinese-language vegan podcast. The site is bilingual (Chinese primary, English secondary) and hosted on GitHub Pages.

## Build & Development Commands

```bash
# Install Ruby dependencies
bundle install

# Build the site (output to _site/)
bundle exec jekyll build

# Local development server (http://localhost:4000)
bundle exec jekyll serve

# Preview built site on port 8020
cd _site && python3 -m http.server 8020

# Compile LESS to CSS and minify JS (requires npm install first)
npx grunt          # runs uglify + less + usebanner
npx grunt watch    # watches for file changes
```

## Architecture

**Theme**: Huxblog (by qiubaiying, based on huxpro). Bootstrap 3 + jQuery with custom LESS styles.

**Layouts** (`_layouts/`): `default.html` → `page.html` / `post.html` / `keynote.html`. Posts use `post` layout; standalone pages (about, tags, search) use `page` layout.

**Key config** (`_config.yml`):
- Pagination: jekyll-paginate, 10 per page
- Plugins: jekyll-paginate, jekyll-sitemap
- Markdown: kramdown (GFM), rouge highlighter
- PWA enabled via `sw.js` and `pwa/manifest.json`

**i18n**: Bilingual labels are configured in `_config.yml` (sidebar descriptions) and hardcoded in `_includes/nav.html`. The site uses a dual-label approach (e.g., "首页 Home") rather than a locale-switching framework.

**Search**: Client-side via Simple-Jekyll-Search. `search.json` generates a JSON index from all posts; `search.html` provides the UI.

**Styles**: LESS source in `less/` compiles to `css/hux-blog.min.css` via Grunt. System font stack with Chinese font fallbacks (PingFang SC, Microsoft YaHei, etc.).

## Content

Posts live in `_posts/` as Markdown files. Front matter includes: `layout`, `title`, `subtitle`, `date`, `author`, `header-img`, `catalog`, `tags`. Most posts are podcast episode show notes.

## CI

Travis CI (`.travis.yml`) runs `jekyll build` to verify the site compiles.
