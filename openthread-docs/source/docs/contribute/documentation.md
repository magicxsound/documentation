---
title: Documentation
description: "Contributing to the OpenThread documentation"
---
This documentation site is written in [Markdown](https://daringfireball.net/projects/markdown/) and built with [mkdocs-material](https://squidfunk.github.io/mkdocs-material/). The site is hosted on [Cloudflare Pages](https://pages.cloudflare.com/).

## Contributing

There are two ways of contributing:

- Using the **Edit this page on GitHub** link at the bottom of every page.
- Building the documentation locally.

### Locally

1. Install the dependencies:

    ```bash
    scripts/setup
    ```

2. Start a preview of the website:

    ```bash
    scripts/develop
    ```

    - This hosts the documentation on `http://localhost:8000`.
    - The server reloads automatically to reflect your changes.

3. Before pushing, confirm the site still builds:

    ```bash
    scripts/build
    ```

    The build runs in strict mode, so a broken link, a missing anchor, or a page
    that is not listed in `nav` fails the build rather than producing a warning.

## Folder structure

All pages live under `source/`, and all images under `source/assets/images/`.

## Creating new pages

1. Create a new `.md` file under `source/docs/` in a subdirectory that fits the purpose of the file.
2. Add a reference to that file in `mkdocs.yml`.

At the top of every page, add a header:

```yaml
---
title: A title for the page, this will also be used in the sidebar.
description: "A summary of the contents of this page"
---
```

## Moving or renaming pages

Old URLs must keep working. When you move or rename a page, add a matching entry
to `source/_redirects`.

## About screenshots

- **Size**: before screenshotting, set the window to 1440x900 pixels.
- **Format**: PNG.
- **Dark and light theme**: create two screenshots, one per theme.
- **Location**: `source/assets/images/screenshots/`.
- **File naming convention**:
    - `name_of_the_screenshot/light.png`
    - `name_of_the_screenshot/dark.png`
    - Use underscores `_` to separate words.
    - Use lowercase characters.

## Creating links

### Linking to another page

For a page located at `source/docs/guides/build.md`, use a docs-relative link
that keeps the `.md` extension:

```md
[Building OpenThread](/docs/guides/build.md)
```

To link to an external page, use the full URL.

### Referencing images

For an image located at `source/assets/images/topology.png`:

```md
![image](/assets/images/topology.png)
```
