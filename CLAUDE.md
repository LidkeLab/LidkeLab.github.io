# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
LidkeLab GitHub Pages website - Academic portfolio and research showcase for the Keith A. Lidke Laboratory at University of New Mexico. Built on Academic Pages Jekyll template (Minimal Mistakes theme).

## Development Commands

### Building with Claude Code
Due to environment limitations in Claude Code, traditional Ruby/bundler setup may require sudo access. Use these alternative approaches:

#### Option 1: Docker (Recommended if Docker is available)
```bash
# Build and run with Docker Compose
docker compose up --build

# Or if you have Docker permissions:
sudo docker compose up --build

# Site will be available at localhost:4000
```

#### Option 2: Manual Ruby Setup (if Ruby is installed)
```bash
# Set up local gem installation to avoid permission issues
export GEM_HOME=$HOME/.gems
export PATH=$HOME/.gems/bin:$PATH

# Install bundler
gem install bundler

# Configure bundler for local installation
bundle config set --local path 'vendor/bundle'

# Install dependencies
bundle install

# Run Jekyll
bundle exec jekyll liveserve
```

#### Option 3: Request System Setup
If the above methods fail, you may need to request:
```bash
# System-level installation (requires admin)
sudo apt-get install ruby-dev ruby-bundler nodejs
sudo gem install bundler jekyll
```

### Standard Development (after setup)
```bash
# Primary method
bundle exec jekyll liveserve

# Alternative commands
jekyll serve -l -H localhost
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

### Dependency Management
```bash
# Install Ruby dependencies
bundle install

# If permission errors occur:
bundle config set --local path 'vendor/bundle'
bundle install

# Install Node dependencies (for JS build tools)
npm install
```

### JavaScript Build Commands
```bash
npm run build:js  # Build minified JS
npm run uglify    # Alternative build command
npm run watch:js  # Auto-rebuild on JS changes
```

### Docker Development
```bash
docker compose up  # Runs at localhost:4000
```

### CV JSON Generation
```bash
# Update CV JSON from markdown
python scripts/cv_markdown_to_json.py
# Or use the shell script:
./scripts/update_cv_json.sh
```

## Architecture

### Content Collections
Jekyll collections define content types with specific front matter requirements:

- `_publications/`: Academic papers (format: `YYYY-MM-DD-paper-title-number-N.md`)
- `_teaching/`: Courses and teaching experiences
- `_portfolio/`: Research projects and demos
- `_talks/`: Presentations and conferences
- `_posts/`: Blog posts (format: `YYYY-MM-DD-title.md`)

### Page Structure
- `_pages/`: Static pages
  - `about.md`: Homepage content (permalink: /)
  - `publications.md`: Publications listing
  - `research-highlights.md`: Research overview
  - `Courses/`: Course materials (BiophysicsFall2024, FluorNanoFall2024, etc.)
- `_layouts/`: Page templates (default, single, talk, cv-layout)
- `_includes/`: Reusable components (header, footer, analytics, etc.)

### Configuration Hierarchy
1. `_config.yml`: Main configuration (requires server restart on change)
2. `_config.dev.yml`: Development overrides
3. `_config_docker.yml`: Docker-specific settings
4. `_data/navigation.yml`: Site navigation (currently: Overview, Research Highlights, Publications)

### Asset Management
- `images/`: Image assets (reference as `/images/filename`)
- `files/`: Downloadable PDFs and documents
- `assets/css/`: Stylesheets (main.scss compiles SASS)
- `assets/js/`: JavaScript (main.min.js is the compiled bundle)

## Content Patterns

### Required Front Matter
All content files need YAML front matter:
```yaml
---
title: "Title"
collection: publications  # or teaching, portfolio, talks
permalink: /path/
date: YYYY-MM-DD
---
```

### Publications Generation
Use `markdown_generator/` tools to batch-create content:
- `publications.py`: Generate from TSV data
- `PubsFromBib.ipynb`: Generate from bibliography files
- `OrcidToBib.ipynb`: Import from ORCID

### Current Site Structure
The site has been simplified to three main sections:
1. **Overview** (/): Lab introduction and research areas
2. **Research Highlights** (/research-highlights/): Key research focus
3. **Publications** (/publications/): Academic publications list

## Key Implementation Notes

### Jekyll Specifics
- Changes to `_config.yml` require server restart
- Use `bundle exec` prefix to ensure correct gem versions
- Collections must be defined in _config.yml to be processed
- Permalink structure follows `/:collection/:path/` pattern

### Theme Customization
- Based on Minimal Mistakes theme with Academic Pages modifications
- Custom layouts in `_layouts/` override theme defaults
- SASS customizations in `_sass/` directories
- JavaScript plugins configured in package.json

### GitHub Pages Deployment
- Site automatically builds and deploys on push to main branch
- CNAME file configures custom domain if needed
- Only whitelisted Jekyll plugins work on GitHub Pages