# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic portfolio website for Hancheng Lou, built with Jekyll and hosted on GitHub Pages. Based on the Academic Pages template (fork of Minimal Mistakes theme). URL: https://louhc.github.io

## Common Commands

```bash
# Install dependencies
bundle install                              # Ruby gems
npm install                                 # Node packages

# Local development (site at localhost:4000, live reload)
bundle exec jekyll serve -l -H localhost

# Build JavaScript (minify all JS into main.min.js)
npm run build:js

# Docker alternative
docker compose up                           # site at localhost:4000
```

**Important:** Changes to `_config.yml` require restarting the Jekyll server. Markdown/HTML changes reload automatically.

## Architecture

**Jekyll static site** using collections-based content organization:

- **`_config.yml`** — Central configuration: site metadata, author info, collections, plugins, theme selection
- **`_data/navigation.yml`** — Controls header navigation links
- **`_data/cv.json`** — Structured CV data used by the JSON-based CV page

**Content collections** (each in `_collections/` with Markdown + YAML front matter):
- `_publications/` — Research papers (categorized: books, manuscripts, conferences)
- `_talks/` — Presentations and tutorials
- `_teaching/` — Courses
- `_portfolio/` — Projects

**Layout hierarchy:** `compress.html` → `default.html` → `single.html` | `talk.html` | `cv-layout.html`

**Pages** (`_pages/`): Archive/listing pages for each collection, plus CV, about, talkmap.

**Styling:** SASS in `_sass/`, theme set via `site_theme` in `_config.yml` (options: default, air, sunrise, mint, dirt, contrast).

**Automation:** `markdown_generator/` contains Python scripts and Jupyter notebooks to generate collection Markdown from CSV/TSV files. GitHub Actions workflow (`scrape_talks.yml`) auto-updates talk location data.

## Content Front Matter

Publications:
```yaml
title: "Paper Title"
collection: publications
category: conferences  # or: books, manuscripts
permalink: /publication/YYYY-MM-DD-slug
venue: 'Journal Name'
paperurl: 'https://...'
date: YYYY-MM-DD
```

Talks:
```yaml
title: "Talk Title"
collection: talks
type: "Talk"  # or "Tutorial"
permalink: /talks/YYYY-MM-DD-slug
venue: "Location Name"
date: YYYY-MM-DD
location: "City, State, Country"
```

## Key Details

- Markdown processor: kramdown (GFM input)
- Plugins: jekyll-feed, jekyll-gist, jekyll-paginate, jekyll-sitemap, jekyll-redirect-from, jemoji
- `future: true` in config — posts with future dates are rendered
- Author sidebar configured in `_config.yml` under `author:`, template in `_includes/author-profile.html`
- Static files (PDFs, etc.) go in `files/`, images in `images/`
