# repox

`repox` is a Python CLI for creating GitHub repositories and bootstrapping the
current directory without leaving the terminal.

It wraps `gh` and `git`, adds interactive prompts with sensible defaults, and
can scaffold a starter project template before the first push.

## Why repox

- Create a GitHub repo from the terminal with one command.
- Avoid the repeated `git init`, `git add`, `git commit`, remote setup, and push flow.
- Reuse starter templates for APIs, CLIs, frontends, and ML projects.
- Keep defaults in `~/.repox.toml` so repeated setup takes less time.

## Requirements

- Python 3.8+
- `git`
- `gh` authenticated with `gh auth login`

## Install

From PyPI:

```bash
pip install repox
```

For local development:

```bash
pip install -e ".[dev]"
```

If your shell does not find the installed `repo` command, add:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

## Quick Start

Create a repo with guided prompts:

```bash
repo
```

Create a private Flask project without confirmation:

```bash
repo my-api --private --template flask --yes
```

Create a public React repo and open it in the browser after push:

```bash
repo my-ui --public --template react --open
```

## How It Works

When you run `repo`, repox:

1. Verifies `git` and `gh` are installed and that `gh` is authenticated.
2. Creates the remote GitHub repository with `gh repo create`.
3. Applies an optional bundled or custom template.
4. Fetches a `.gitignore` suggestion from GitHub's gitignore templates API.
5. Initializes the local git repository, commits, adds the remote, and pushes.

## Commands

### `repo`

Create a repository in the current directory.

Options:

- `--public` create a public repository
- `--private` create a private repository
- `--template <name>` choose a scaffold template
- `-y, --yes` skip the confirmation prompt
- `--open` open the repository in the browser after a successful push
- `--version` print the installed version

### `repo config`

View or update persistent defaults stored in `~/.repox.toml`.

Examples:

```bash
repo config
repo config --show
repo config --reset
```

Config shape:

```toml
[defaults]
visibility = "private"
template = "none"
remote = "origin"

[templates]
custom_dir = "~/my-templates"
```

### `repo templates`

List the available built-in templates plus any templates discovered in the
configured custom template directory.

## Built-In Templates

- `flask`: Minimal Flask API with a health check route
- `fastapi`: Minimal FastAPI service
- `react`: React + Vite starter
- `django`: Minimal Django project scaffold
- `cli`: Click-based Python CLI scaffold
- `ml`: Notebook-first machine learning project scaffold

Templates can declare metadata through `template.toml` and may use:

- `{{repo_name}}`
- `{{author}}`

These variables are rendered into file contents and template paths during copy.

## Custom Templates

Set a custom template directory:

```bash
repo config
```

Point `custom_dir` to a folder that contains one subdirectory per template. Each
template can include a `template.toml` file:

```toml
[meta]
name = "Internal API"
description = "Company starter service"
language = "Python"
post_install = "Run: uv sync"
```

## Development

Run tests:

```bash
python -m unittest discover -s tests -v
```

Build a distribution locally:

```bash
python -m build
```

## Release Process

The repository includes GitHub Actions workflows for:

- running tests on every push and pull request
- building and publishing to PyPI when a tag like `v1.0.0` is pushed

To publish a release:

1. Update code and docs.
2. Push to `main` and confirm CI passes.
3. Create and push a version tag:

```bash
git tag v1.0.0
git push origin v1.0.0
```

4. Ensure the repository has a `PYPI_API_TOKEN` secret configured.

## Demo

The README is prepared for a future GIF or terminal recording section. No demo
asset is bundled in the repository yet.
