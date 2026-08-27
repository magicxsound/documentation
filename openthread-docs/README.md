# OpenThread Documentation

Documentation site for OpenThread, built with [MkDocs](https://www.mkdocs.org/) +
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) and intended
for hosting on Cloudflare Pages.

This scaffolding is adapted from the HACS documentation site.

## Commands

```bash
scripts/setup      # apt-get install libcairo2 (needed by the social/imaging plugins) + pip install -r requirements.txt
scripts/develop    # mkdocs serve — live-reloading preview on http://localhost:8000
scripts/build      # mkdocs build — output goes to build/
pre-commit run --all-files   # codespell, the only linter
```

`mkdocs.yml` sets `strict: true`, so build warnings are errors: a broken relative
link, a missing anchor, or a page not listed in `nav` (and not matched by
`not_in_nav`) fails the build. Run `scripts/build` before pushing.

The `social` plugin fetches the configured Google Font on first build, so the
first build of a session needs network access.

## Layout

- `source/` — the docs root (`docs_dir`). Pages live under `source/docs/<section>/`.
- `source/overrides/` — Material theme overrides: `partials/header.html`,
  `partials/content.html` (the "Help and support" block and the auto-generated
  section index grids), `templates/home.html` (used by `source/index.md`), `404.html`.
- `source/hooks/html_tag_modifier.py` — post-processes HTML so external links get
  `target=_blank` and images get `loading=lazy`. Do not add these by hand.
- `source/assets/stylesheets/extra.css` — the palette (`--ot-color-primary`) and
  the custom components used by the overrides.
- `source/_redirects` — the Cloudflare Pages redirect file. Moving or renaming a
  page requires an entry here.
- `source/includes/abbreviations.md` — auto-appended to every page by
  `pymdownx.snippets`.

## Things to fill in

The site builds and is wired up end to end, but the content is a skeleton:

- Pages under `source/docs/` marked with a `!!! note` are starters — port the real
  content from https://openthread.io / the upstream repository.
- There is no logo or favicon. Add them under `source/assets/images/` and set
  `theme.logo` / `theme.favicon` in `mkdocs.yml`.
- The palette in `extra.css` and `social.cards_layout_options.background_color`
  are placeholder blues. Replace with the real brand colors.
- `extra.docs_repo_url` in `mkdocs.yml` points the "Edit this page" button at the
  repository that holds *this* site. Change it if the site does not live there.
