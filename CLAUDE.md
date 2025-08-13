# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
Academic Pages Jekyll website - A GitHub Pages template for personal/professional academic portfolios based on the Minimal Mistakes Jekyll theme.

## Build & Run Commands

### Prerequisites Installation
```bash
# Linux/WSL
sudo apt install ruby-dev ruby-bundler nodejs
# For build issues, also install:
sudo apt install build-essential gcc make

# macOS
brew install ruby node
gem install bundler
```

### Development Commands
- **Install dependencies**: `bundle install` (delete Gemfile.lock if errors occur)
- **Local development**: `bundle exec jekyll liveserve` (runs at localhost:4000)
- **Alternative local serve**: `jekyll serve -l -H localhost`
- **With dev config**: `bundle exec jekyll liveserve --config _config.yml,_config.dev.yml`
- **Clean directory**: `bundle clean`
- **Docker alternative**: `docker compose up` (runs at localhost:4000)

### JavaScript Build Commands
- **Build JS**: `npm run build:js` or `npm run uglify`
- **Watch JS changes**: `npm run watch:js`

### Dependency Management
If permission errors occur with `bundle install`:
```bash
bundle config set --local path 'vendor/bundle'
bundle install
# Add 'vendor' to .gitignore
```

## Architecture & Structure

### Collections (Content Types)
- `_publications/`: Academic publications (format: `YYYY-MM-DD-paper-title-number-N.md`)
- `_teaching/`: Teaching experiences
- `_portfolio/`: Portfolio items
- `_talks/`: Talks and presentations
- `_posts/`: Blog posts (format: `YYYY-MM-DD-title.md`)

### Key Directories
- `_pages/`: Static pages (about, cv, teaching, etc.)
  - `_pages/Courses/`: Course-specific content and materials
- `_includes/`: Reusable HTML components
- `_layouts/`: Page templates
- `_sass/`: SCSS stylesheets
- `assets/`: CSS, JS, and fonts
- `images/`: Image assets (reference with `/images/` prefix)
- `files/`: Downloadable files (PDFs, etc.)
- `markdown_generator/`: Python/Jupyter tools for generating content from data files
- `talkmap/`: Interactive map generation for talks

### Configuration
- `_config.yml`: Main site configuration (requires restart after changes)
- `_data/navigation.yml`: Site navigation structure
- `_data/ui-text.yml`: UI text strings

## Content Creation Patterns

### Front Matter Requirements
All content files require YAML front matter:
```yaml
---
title: "Title Here"
collection: publications/teaching/portfolio/talks
permalink: /path/to/page/
date: YYYY-MM-DD
---
```

### Publications Generation
Use `markdown_generator/` tools:
- `publications.py`: Generate from TSV
- `PubsFromBib.ipynb`: Generate from bibliography
- `talks.py`: Generate talk pages from TSV

### Course Pages
Located in `_pages/Courses/`:
- Main course page: `CourseName.md`
- Supporting materials in subdirectories

## Key Development Notes
- Jekyll doesn't auto-reload `_config.yml` changes - restart server
- Use existing content as templates for consistency
- Follow kebab-case naming for files
- Date-based naming for time-sensitive content
- Generate structured content with markdown_generator tools when possible