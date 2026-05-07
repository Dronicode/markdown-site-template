# Add Changelog and Version Automation

If you are starting from zero, begin with [Create a Site From Scratch](Create%20a%20Site%20From%20Scratch.md). You can follow that page and then continue here to recreate the full automation setup.

Use this checklist when you already have a markdown site and want to add the changelog and semantic-release workflow setup from this template.

## 1. Repository Basics

- Set `main` as the default branch
- Create a `develop` branch

## 2. GitHub App Setup

Create one GitHub App to act as the automation identity.

Path: GitHub -> Settings -> Developer settings -> GitHub Apps -> New GitHub App

Suggested name: `Site Name Assistant`

Webhook:

- Active: disabled
  (Or enabled if you want webhooks and know what you're doing. Can be enabled later.)

Permissions -> Repository permissions:

- Contents: Read and write
- Pull requests: Read and write

Where can this GitHub App be installed?:

- Only on this account

After creating the app:

- Create a private key
- Install App -> Install on your account -> Only select repositories
- Save the App ID and private key for later

## 3. Repository Settings

General:

- Enable release immutability: enabled
- Wikis, Issues, Sponsorships, Preserve this repository, Discussions, Projects: disabled
- Pull requests: enabled
- Pull request permissions: collaborators only
- Allow merge commits: enabled
- Allow squash merging: disabled
- Allow rebase merging: disabled
- Allow auto-merge: enabled
- Allow comments on individual commits: false

Rules -> Rulesets:

- New ruleset -> New branch ruleset
- Name: main protection + workflow automation
- Enforcement status: Active
- Bypass list -> Add bypass: add `Site Name Assistant`
- Target branches -> Add target: Include default branch
- Restrict deletions: enabled
- Require a pull request before merging: enabled
- Required approvals: 0
- Allowed merge methods: Merge
- Require status checks to pass: enabled
- Required checks -> Add checks:
  - `Lint Commits`
  - `Validate Paths`
  - `Validate Build`
  - Source: GitHub Actions
    > Note: These checks won't appear until after the first time they are run, so leave checks in setup and add it after doing a commit
- Block force pushes: enabled

Actions -> General:

- Actions permissions: Allow all actions and reusable workflows
- Workflow permissions: Read and write permissions
- Allow GitHub Actions to create and approve pull requests: enabled

Pages:

- Source: GitHub Actions
- Custom domain: optional

Secrets and variables -> Actions:

- New repository secret -> Name: `APP_ID` Secret: (The app ID from the bot)
- New repository secret -> Name: `APP_PRIVATE_KEY` Secret: (When you made the private key for the bot it downloaded a private-key.pem file. Open that and paste the whole thing here.)

## 4. Baseline Version Tags

If you didn't already create starting tags, do so now. Create both starting tags on `main` so semantic-release has a baseline:

- `v0.0.1`
- `infra-v0.0.1`

You can create draft releases in GitHub to create the tags, then delete the release objects afterward if you only want the tags.

## 5. Files To Copy Into The Existing Project

```text
.github/
  workflows/
    auto-pr.yml
    commit-lint.yml
    path-scope-validate.yml
    validate-site.yml
    semantic-release.yml
    deploy-site.yml
.releaserc.content.cjs
.releaserc.infra.cjs
.releaserc.utils.cjs
.commitlintrc.js
versions.json
CHANGELOG_INFRA.md
docs/
  Changelog.md
scripts/
  update_versions_json.py
  update_index_md_release_status.py
  update_pyproject_version.py
  normalize_changelog_headers.py
pyproject.toml
```

## 6. Scope Rules

- `content`: documentation content changes under `docs/`
- `site`: site configuration, theme, navigation, or build behavior
- `ci`: workflow, release, and repository automation changes

`path-scope-validate.yml` assumes that `content`-scoped commits touch files under `docs/`, and that pull requests touching `docs/` include at least one `content`-scoped commit.

## 7. Version Tracks

Content track:

- Config file: `.releaserc.content.cjs`
- Triggers on `feat(content): …` and `fix(content): …`
- Publishes GitHub Releases and updates `Changelog.md`, `index.md`, and `../versions.json`

Infra track:

- Config file: `.releaserc.infra.cjs`
- Triggers on `feat(ci): …`, `fix(ci): …`, `feat(site): …`, and `fix(site): …`
- Publishes `infra-vX.Y.Z` tags and updates `CHANGELOG_INFRA.md` in the repository root, `versions.json`, and `pyproject.toml` version

## 8. Final Verification

- Push a test commit to `develop`
- Confirm the auto PR to `main` appears
- Confirm commit lint, path validation, and site validation run on the PR
- Merge to `main` and confirm semantic-release updates the expected changelog files
- Confirm GitHub Pages deploys after a content release
