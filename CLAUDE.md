# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The HACS documentation site published at https://hacs.xyz. It is content-only — there is no application code here; the HACS integration itself lives at https://github.com/hacs/integration. Built with MkDocs + Material for MkDocs, hosted on Cloudflare Pages.

## Commands

```bash
scripts/setup      # apt-get install libcairo2 (needed by the social/imaging plugins) + pip install -r requirements.txt
scripts/develop    # mkdocs serve — live-reloading preview on http://localhost:8000
scripts/build      # mkdocs build — output goes to build/
pre-commit run --all-files   # codespell, the only linter
```

There are no tests. CI (`.github/workflows/actions.yml`) runs pre-commit, then `scripts/setup` + `scripts/build`. A devcontainer (`.devcontainer.json`, Python 3.13) runs `scripts/setup` on create.

`mkdocs.yml` sets `strict: true`, so build warnings are errors: a broken relative link, a missing anchor, or a page not listed in `nav` (and not matched by `not_in_nav`) fails the build. Run `scripts/build` before pushing content changes.

## Build pipeline specifics

Beyond stock mkdocs-material, four custom pieces run at build time:

- **`source/macros.py`** (mkdocs-macros, `on_undefined: strict`) exposes `{{ hacsui("key") }}` and `{{ coreui("key") }}`. These resolve UI strings from the *live* English translation files of the HACS frontend and the Home Assistant frontend, downloaded on first build and cached in `.cache/translations/`. A key that does not exist raises and fails the build; the first build of a session needs network access. Prefer these macros over hardcoding UI labels so the docs track the actual UI.
- **`source/hooks/shortcodes.py`** implements `<!-- hacs:my <redirect> title="..." -->`, expanding to a `my.home-assistant.io/redirect/<redirect>/` link. `title` is commonly built from `coreui(...)` calls.
- **`source/hooks/html_tag_modifier.py`** post-processes HTML: external links get `target=_blank`, images get `loading=lazy`. Do not add these attributes by hand.
- **`source/overrides/`** holds the Material theme overrides (header/content/footer partials, 404, the `home.html` template used by `source/index.md`).

`source/_redirects` is the Cloudflare Pages redirect file — old URLs are preserved there, so move or rename a page only together with a redirect entry.

## Content conventions

- Pages live under `source/docs/<section>/`, and every new page must also be added to `nav:` in `mkdocs.yml`.
- Every page starts with front matter: `title:` (also the sidebar label) and `description:`.
- Internal links are docs-relative and include the `.md` extension: `[Features](/docs/contribute/features.md)`. Images: `![image](/assets/images/features.png)`.
- Screenshots go in `source/assets/images/screenshots/<name_of_the_screenshot>/{light,dark}.png` — PNG, captured at 1440x900, both themes, lowercase with underscores. `scripts/compress_images.py` re-saves PNGs under `source/assets/images` at quality 50.
- Upstream contributions target the `next` branch, not `main` (`remote_branch` in `mkdocs.yml`).

The contributor-facing version of these rules is `source/docs/contribute/documentation.md`; keep the two in sync when either changes.
