# LidkeLab Website - Jekyll-based Academic Website

## Build & Run Commands
- Install prerequisites: `sudo apt install ruby-dev ruby-bundler nodejs`
- Install dependencies: `bundle install` (delete Gemfile.lock if errors occur)
- Clean up directory: `bundle clean`
- Local development: `bundle exec jekyll liveserve` (runs at localhost:4000)
- Using dev config: `bundle exec jekyll liveserve --config _config.yml,_config.dev.yml`

## Website Structure
- Content in collections: `_publications`, `_teaching`, `_portfolio`, `_talks`
- Page content in `_pages` directory using Markdown
- Course materials in `_pages/Courses`
- Static assets in `images`, `files` directories

## Content Guidelines
- Use YAML front matter in all content files
- Follow existing markdown formatting patterns
- Publications format: year-month-day-paper-title-number-N.md
- News/blog posts in `_posts` directory
- Generate content with notebooks in `markdown_generator` when possible

## Naming Conventions
- Use descriptive, kebab-case filenames
- Follow date-based naming for time-sensitive content
- Reference images with `/images/` path prefix
- Keep filenames concise but descriptive