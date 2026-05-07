# How to Use Zensical

Zensical is the build tool for this markdown site.

If you need help writing content, go to [Markdown](Markdown.md).

## Install Dependencies

```bash
uv sync
```

Run this first after cloning the repository or after dependency changes.

## Start the Local Preview Server

```bash
uv run zensical serve
```

Use this while writing content so you can refresh the browser and check the site locally.

## Build the Static Site

```bash
uv run zensical build --clean
```

This writes a fresh production build to the `site/` directory.

## When to Use Which Command

- Use [`uv run zensical new`](https://zensical.org/docs/usage/new/) only when bootstrapping a brand new site
- Use [`uv run zensical serve`](https://zensical.org/docs/usage/preview/) while developing
- Use [`uv run zensical build --clean`](https://zensical.org/docs/usage/build/) when you want to validate the production output
