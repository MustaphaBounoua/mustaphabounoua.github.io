# Copilot Instructions: Al-Folio Academic Website

This is a **Jekyll-based academic website** built on the al-folio theme. It generates static HTML for GitHub Pages.

## Architecture Overview

**Content Model**: Data-driven static site
- **Pages**: `_pages/` (about, CV, publications) → layouts in `_layouts/`
- **Posts**: `_posts/` (blog posts with frontmatter) → uses date-based permalinks
- **News**: `_news/` (timeline items) → included in `_includes/news.html`
- **Projects**: `_projects/` (portfolio items) → rendered in `_includes/projects.html`
- **Publications**: `_bibliography/papers.bib` (BibTeX) → parsed by `jekyll-scholar` plugin

**Data Sources**: YAML files in `_data/` control dynamic rendering
- `cv.yml` - CV sections (time_table, map types) → rendered by `_includes/cv/`
- `repositories.yml` - GitHub repo links → fetched via GitHub API in includes
- `coauthors.yml` - Author metadata aliases
- `venues.yml` - Conference/venue information

**Layouts Chain**: `default.html` → specific layout (e.g., `post.html`, `about.html`) → includes for components

## Key Build Details

**Build Command**: `bundle exec jekyll build --lsi` (includes Latent Semantic Indexing)
- Docker: Build environment in `Dockerfile`; use `bin/docker_run.sh` for local dev
- Output: `_site/` (ignored in git)
- Plugins: 21 gems configured; 3 custom Ruby plugins in `_plugins/`

**Custom Plugins** (critical for functionality):
- `external-posts.rb` - Fetches RSS feeds from `external_sources` config
- `details.rb` - Adds `{% details %}` tag for collapsible HTML5 `<details>`
- `hideCustomBibtex.rb` - Customizes bibliography rendering

## Content Conventions

**Posts**: Front matter includes `layout: post`, `date`, `categories`, `description`
- Comments: Include `giscus_comments: true` for discussion threads
- Related posts: `related_posts: true` for "See Also" section
- Math: Wrapped in `$` (inline) or `$$` (blocks); MathJax auto-loaded

**CV Structure in YAML** (in `_data/cv.yml`):
```yaml
- title: Education
  type: time_table  # or 'map' for key-value pairs
  contents:
    - title: PhD
      institution: University
      year: 2022-2025
      description:
        - Point 1
        - Point 2
```

**Projects**: File naming `N_project.md` sorts by N; edit frontmatter `title`, `img`, `description`, `category`

**News Items**: YAML in `_news/` with optional `inline` or `related_posts` flags

## Styling & Customization

**SASS Architecture**: `_sass/` contains:
- `_base.scss` - Custom blockquotes (block-tip, block-warning, block-danger)
- `_themes.scss` - Light/dark mode variables
- `_variables.scss` - Breakpoints, fonts, colors
- Imports Bootstrap (configured in Jekyll config)

**Config-Driven Themes**:
- `highlight_theme_light/dark` - Syntax coloring (from jekyll-pygments-themes)
- `repo_theme_light/dark` - GitHub stats card themes
- Max width: `800px` (set in config)

## Important Workflows

**Adding Content**:
1. Posts: Create `_posts/YYYY-MM-DD-slug.md` with Jekyll front matter
2. Publications: Add entries to `_bibliography/papers.bib`; jekyll-scholar auto-renders `publications.html`
3. Projects: Create `_projects/N_project.md` (N determines sort order)
4. News: Create `_news/announcement_N.md` with date and optional description

**Editing Metadata**:
- Personal info: Top of `_config.yml` (name, email, title)
- CV content: Modify `_data/cv.yml` (structures with type: time_table or map)
- Social links: `_config.yml` has 40+ username fields (github_username, twitter_username, etc.)
- Featured repos: Edit `_data/repositories.yml` (GitHub users/repos list)

**Deployment**:
- Automatic: GitHub Actions `.github/workflows/deploy.yml` builds on push to `master`
- Docker image available: `amirpourmand/al-folio` on Docker Hub

## Plugin Dependencies & Gotchas

- **jekyll-scholar**: Requires gems `citeproc-ruby`, `bibtex-ruby`; publications render from `.bib` files
- **jekyll-imagemagick**: Resizes images; needs ImageMagick in environment
- **jekyll-diagrams**: Adds `{% mermaid %}`, `{% plantuml %}` tags
- **jekyll-toc**: Auto-generates table of contents if `page.toc: { sidebar: right/left }` in YAML
- **External posts**: Only process if `site.config['external_sources']` is set; uses HTTParty + Feedjira

## File Reference

Critical files to understand patterns:
- [_config.yml](_config.yml#L1) - All configuration (theme, plugins, social, build settings)
- [_layouts/default.html](_layouts/default.html) - Master template structure
- [_layouts/about.html](_layouts/about.html) - Home page (includes news, CV, papers)
- [_includes/cv/time_table.html](_includes/cv/time_table.html) - CV rendering
- [_data/cv.yml](_data/cv.yml) - Structured CV content
- [_plugins/external-posts.rb](_plugins/external-posts.rb) - RSS feed integration
- [Gemfile](Gemfile) - Ruby dependencies

---

**Tip**: When adding features, check if jekyll-scholar or other plugins already provide it before creating custom code. The theme is well-documented; refer to [al-folio README](https://github.com/alshedivat/al-folio) for upstream changes.
