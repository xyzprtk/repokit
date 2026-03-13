# Changelog

## 1.0.0

- Finalized packaging metadata for a stable `repox` release.
- Added polished README documentation covering install, commands, config, templates, and release flow.
- Added GitHub Actions workflows for CI on pushes and pull requests.
- Added a tagged release workflow that builds the package and publishes it to PyPI.

## 0.4.0

- Added template manifests with metadata and post-install instructions.
- Added `repo templates` for listing available templates.
- Added `django`, `cli`, and `ml` starter templates.
- Added variable substitution for `{{repo_name}}` and `{{author}}` in template paths and file contents.

## 0.3.0

- Added persistent configuration in `~/.repox.toml`.
- Added `repo config`, `repo config --show`, and `repo config --reset`.
- Added support for custom template directories and configurable default remote names.

## 0.2.0

- Added colored output, step formatting, summary confirmation, and smarter defaults.
- Added `--yes` and `--open` flags.
- Improved error handling for `git` and `gh` failures.

## 0.1.0

- Initial Phase 1 implementation.
