# CLAUDE.md

Website of the Molecular Biology Lab (Institute of Life Sciences, Sion), published at https://kuhn-lab.github.io. The owner is not fluent in Ruby, so explain Ruby/Jekyll steps as you go.

## Stack
- Jekyll 4.4.1 with the Minimal Mistakes theme via `remote_theme: "mmistakes/minimal-mistakes@4.28.1"` (pinned; don't float on master).
- Plugins: jekyll-feed, jekyll-include-cache, jekyll-remote-theme, jekyll-sitemap.
- Nav lives in `_data/navigation.yml` (not `header_pages`). Pages use `layout: single`; the theme has no `page` layout.
- Sass entry point is `assets/css/main.scss` (the path Minimal Mistakes expects), which imports `_sass/custom.scss`.

## Publishing
- `.github/workflows/jekyll.yml` builds with this repo's Gemfile and deploys to Pages on push to `main`.
- Repo Settings -> Pages source was still "Deploy from a branch" at last check, so GitHub's classic build was doing the publishing. Switching the source to "GitHub Actions" is a manual setting.
- `main` has a "changes via pull request" rule; the owner's account can bypass it.

## Run locally
- Ruby 3.3 from apt; Bundler is a user gem. Ensure `~/.local/share/gem/ruby/3.3.0/bin` is on PATH.
- Gems install into `vendor/bundle` (`.bundle/config`, untracked). `libssl-dev` is needed to build the openssl gem.
- `bundle install && bundle exec jekyll serve` -> http://localhost:4000/. Restart after editing `_config.yml`.
- The theme is fetched from GitHub at build time, so builds need network access.
- Sass deprecation warnings from the theme are expected noise.

## Decisions
- No author sidebar: `author_profile: false` in `defaults:` in `_config.yml`.
- `_publications` is a data-only collection (`output: false`, no per-item layout). `publications.markdown` loops over it; the DOI link only shows when `doi` is non-empty.
- Don't wrap `###` headings in `**bold**`; headings are already bold and nesting renders them heavier than intended.

## Standing preferences
- Don't write prose about the lab or its research. Where content is missing, leave a clearly marked `TODO` comment and list it for the owner (e.g. `about.markdown` is a TODO placeholder).
- Don't add self-credit or co-author lines to commit messages.
- Ask before installing anything system-wide (apt etc.); the owner runs `sudo` commands themselves.
