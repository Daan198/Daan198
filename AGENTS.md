# AGENTS.md

## Cursor Cloud specific instructions

This repository is a near-empty skeleton. It contains:

- `.github/workflows/blank.yml` — a template GitHub Actions CI workflow that runs `echo Hello, world!`
- No application code, no dependencies, no build system, no services

### Development

- **No dependencies to install.** There is no `package.json`, `requirements.txt`, `pyproject.toml`, or any other dependency file.
- **No build step.** There is nothing to compile or bundle.
- **No services to start.** There are no backend/frontend servers or databases.
- **No tests to run.** There is no test framework or test files.
- **No linter configured.** There are no lint rules or config files.

### CI

The only CI workflow (`.github/workflows/blank.yml`) runs on push/PR to `main` and executes `echo Hello, world!`. It requires no special setup.

### Branches

- `main` — default branch, contains only the CI workflow template
- `Daan198-patch-1` (remote) — unmerged branch with a `login` file and `python-package.yml` workflow
