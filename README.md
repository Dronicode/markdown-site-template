# Markdown Site Template

Markdown site template built with Zensical, with automated changelog, semantic-release, and GitHub Pages workflows.

Live template site: https://dronicode.github.io/markdown-site-template/

## What This Template Includes

- Markdown site scaffold under `docs/`, built with Zensical
- Conventional Commits with scoped release automation
- Separate content and infra release streams
- Automatic `develop` -> `main` release PR flow
- GitHub Pages deployment from GitHub Actions

## Project Layout

- `docs/`: published documentation content
- `.github/workflows/`: CI, release, and deploy automation
- `scripts/`: helper scripts for changelog and version metadata updates
- `versions.json`: release version metadata for docs and infra streams
- `zensical.toml`: site build configuration

## Local Development

```bash
uv sync
uv run zensical serve
```

To build the static site locally:

```bash
uv run zensical build --clean
```

## Release Model

- `content` scope: releases the content stream with tags like `vX.Y.Z`
- `ci` and `site` scopes: release the infra stream with tags like `infra-vX.Y.Z`
- Content releases update `docs/Changelog.md`, `docs/index.md`, and `versions.json`
- Infra releases update `CHANGELOG_INFRA.md` and `versions.json`
- GitHub Pages deployment runs only after a content release

## Setup Guides

- [Getting Started](docs/Getting%20Started.md)
- [Create a Site From Scratch](docs/Create%20a%20Site%20From%20Scratch.md)
- [Add Changelog Automation](docs/Add%20Changelog%20Automation.md)
- [How to Use Zensical](docs/How%20to%20Use%20Zensical.md)
- [Markdown](docs/Markdown.md)
- [Release Policy](docs/Release%20Policy.md)

## Template Customization Checklist

- Update `zensical.toml` metadata such as `site_name`, `site_description`, and `site_author`
- Review scopes in `.github/workflows/path-scope-validate.yml`
- Review release rules in `.releaserc.content.cjs` and `.releaserc.infra.cjs`
- Review branch policy and bot setup in `.github/workflows/auto-pr.yml`
- Replace starter documentation pages in `docs/` with your own content
