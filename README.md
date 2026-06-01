# Engineering Documentation

This repository currently contains a starter GitHub Actions workflow. The
workflow establishes the CI entry point for future engineering changes, but it
does not yet build, test, or deploy application code.

## CI workflow

The CI workflow is defined in `.github/workflows/blank.yml` and is named `CI`.

### When it runs

The workflow runs in three cases:

- A push targets the `main` branch.
- A pull request targets the `main` branch.
- A maintainer starts it manually through GitHub workflow dispatch
  (`workflow_dispatch`).

### What it does today

The workflow has one job:

- `build` runs on the `ubuntu-latest` GitHub-hosted runner.
- It checks out the repository with `actions/checkout@v3`.
- It runs two placeholder shell steps:
  - `Run a one-line script` prints `Hello, world!`.
  - `Run a multi-line script` prints guidance to add build, test, and deploy
    commands.

Because these commands are placeholders, a passing workflow run only verifies
that the GitHub Actions runner can start and execute shell commands. It does not
validate application correctness.

## Updating the workflow

Replace the placeholder shell commands with the real project checks once source
code is added. A typical sequence is:

```yaml
steps:
  - uses: actions/checkout@v3
  - name: Install dependencies
    run: <dependency install command>
  - name: Run tests
    run: <test command>
```

Keep the workflow focused on repeatable, non-interactive commands so it can run
reliably on both pull requests and pushes to `main`.

## Common pitfalls

- The workflow only triggers automatically for changes involving `main`.
- Manual runs can be started from the GitHub Actions tab or other GitHub
  workflow dispatch mechanisms available to maintainers.
- Adding project-specific build or test commands requires the corresponding
  tooling and lockfiles to exist in the repository.
- Secrets are not configured or referenced by the current workflow.
