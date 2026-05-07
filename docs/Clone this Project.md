# Clone this Project

This page shows how to take this repository and turn it into your own markdown site built with Zensical.

## Before You Start

- Install Git if you do not already have it: <https://git-scm.com/downloads>
- Install Python 3.13 or newer: <https://www.python.org/downloads/>
- Install uv: <https://docs.astral.sh/uv/getting-started/installation/>
- Install GitHub CLI if you want to create the GitHub repository from the terminal (optional): <https://cli.github.com/>

If terminal commands are new to you:

## 1. Clone the Template

Open the terminal in the folder where you want the project to live or use `cd` to move there first:

```bash
cd path/to/where/you-want-the-project
```

Change "my-site" to the name of your site.

```bash
git clone https://github.com/Dronicode/markdown-site-template.git my-site
cd my-site
```

What those commands do:

- `git clone … my-site` downloads the template into a new folder named `my-site`
- `cd my-site` moves into that folder

## 2. Install Dependencies

```bash
uv sync
```

- `uv sync` installs the project dependencies from this repository uv to keep it self contained and avoid needing a global install.

## 3. Run the Site Locally

```bash
uv run zensical serve
```

- `uv run …` runs tools in the project that were installed using uv.
- `zensical …` uses Zensical to turn markdown files into webpages and compile it as a website.

Click the link shown in the command output to open the local address to preview the site.

## 4. Publish Under Your Own Repository to Deploy it Online

If you want to push this to your own GitHub repository, remove the template remote and add your own:

Replace `github-username/site-name` below with your own GitHub username or organization and your real repository name.

```bash
git remote remove origin
gh repo create github-username/site-name --public --source=. --remote=origin
git push -u origin main --tags
```

If you do not use GitHub CLI, create the repository in the browser and then run:

```bash
git remote add origin https://github.com/github-username/site-name.git
git push -u origin main --tags
```

## 5. Make the Site Yours

Start by deciding whether you want to keep these template docs for reference.

- Delete the existing files under `docs/` if you want a clean starting point
- Or move the template docs somewhere else in the repository if you want to keep them for later reference

Then update these files:

- `zensical.toml`: set your site name, description, author, and site URL
- `docs/index.md`: replace the homepage content whenever you are ready, but keep the filename as `index.md` and keep the release status markers in place
- `docs/Changelog.md`: keep this file, because the release workflows update it automatically
- `docs/Markdown.md`: keep or expand the writing guide if it is useful for your project
- `README.md`: update the repository description for your own site

Add more .md documents to the docs directory to add pages to your site.

## 6. Commit Your Changes

Any changes you make need to be committed to the repo on GitHub. Commits need short simple messages to identify them.

This template expects commit messages in this shape:

`type(scope): short summary`

Examples:

- `feat(content): add installation guide`
- `fix(content): correct homepage link`
- `chore(ci): update action version`

Use these types:

- `feat`: you added something new, this will bump the second number in the version.
- `fix`: you corrected something broken or wrong, this will bump the third number in the version.
- `chore`: maintenance work that should not create a content release or bump the version number.

Use these scopes:

- `content`: if you made any changes to pages under `docs/`; creates a content release and updates the site changelog
- `site`: changes to theme, navigation, config, or build behavior (but not the content of the site itself); creates an infra release
- `ci`: changes to GitHub Actions or release automation; creates an infra release

If you only changed pages in `docs/` to update what is shown in the website, `content` is usually the right scope.

If you change multiple types of files, commit them separately with their own commit messages.
