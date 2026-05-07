# Create a Site From Scratch

Use this when you want to build a brand new markdown site and then carry this template's changelog and release automation into that repo. The site content is plain Markdown. Zensical is the build tool.

## Before You Start

- Install Git if you do not already have it: <https://git-scm.com/downloads>
- Install Python 3.13 or newer: <https://www.python.org/downloads/>
- Install uv: <https://docs.astral.sh/uv/getting-started/installation/>
- Install GitHub CLI if you want to create the GitHub repository from the terminal (optional): <https://cli.github.com/>

If terminal commands are new to you:

- `cd folder-name` moves into a folder
- `uv add` installs a package into the project, using uv to keep it self contained in the project
- `uv run …` runs a tool from the project, using uv to avoid needing a global install

## Simple Beginner Steps

### 1. Initialize a Python Project with Uv

If you are not already in the right place, either open the terminal in the folder where you want the project to live or use `cd` to move there first:

```bash
cd path/to/where/you-want-the-project
```

Then create the project with uv:

```bash
uv init my-project && cd my-project
```

### 2. Add Zensical and Generate the Starter Files:

```bash
uv add --dev zensical
uv run zensical new
```

### 3. Commit the Starting Point:

```bash
git add .
git commit -m "init project"
```

Seed the baseline release tags on that same commit:

```bash
git tag -a v0.0.1 -m "seed content version tag"
git tag -a infra-v0.0.1 -m "seed infra version tag"
```

**Note:** If you want verified tags and have a GPG/ SSH key registered to your GitHub account, use `-s` instead of `-a` and have a GPG key registered to your GitHub account.

### 4. Create the GitHub Repository

It can be done on the GitHub ui, or from the terminal with the following command.

Replace `github-username/project-name` below with your own GitHub username and repository name.

If you created the repository on GitHub, connect the local one to it:

```bash
git remote add origin https://github.com/github-username/site-name.git
```

If you want to create the repository with a simple command (auto connects local one):

```bash
gh repo create github-username/project-name --public --source=. --remote=origin
```

### 5. Enable GitHub Pages to Build with GitHub Actions

It can be done on the GitHub ui, or from the terminal with the following command.

To set Pages in the ui, go to Pages in project settings and set the source to 'GitHub Actions'.

To set it with an easy command:

```bash
gh api -X POST repos/github-username/project-name/pages -f build_type=workflow
```

### 6. Push to GitHub

```bash
git push -u origin main --tags
```

Open the site:

`https://github-username.github.io/project-name/`
