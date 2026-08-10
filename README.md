# Daan198

GitHub profile and configuration repository. The default branch currently ships
a starter GitHub Actions workflow only—there is no application source, package
manifest, or deploy pipeline yet.

## CI workflow

File: [`.github/workflows/blank.yml`](.github/workflows/blank.yml)  
Workflow name: `CI`

### Triggers

| Event | Scope |
| --- | --- |
| `push` | `main` |
| `pull_request` | targeting `main` |
| `workflow_dispatch` | manual run from the Actions tab |

### Job: `build`

Runs on `ubuntu-latest` and executes:

1. `actions/checkout@v3` — checks out the repository into `$GITHUB_WORKSPACE`
2. **Run a one-line script** — `echo Hello, world!`
3. **Run a multi-line script** — prints placeholder guidance to add build, test,
   and deploy commands

A green run means the runner started and executed those shell steps. It does
**not** prove application correctness, dependency health, or deploy readiness.

## Extending CI

When real project checks exist, replace the placeholder `run:` steps. Keep
commands non-interactive and repeatable on both PRs and pushes to `main`:

```yaml
steps:
  - uses: actions/checkout@v3
  - name: Install dependencies
    run: <dependency install command>
  - name: Run tests
    run: <test command>
```

## Developer notes

- Automatic CI only watches `main`. Feature-branch pushes alone do not start
  the workflow until a PR targets `main` (or you use `workflow_dispatch`).
- No repository secrets are referenced by the current workflow.
- Adding real install/test steps also requires the matching tooling and
  lockfiles in the tree.
- Agent-oriented setup constraints live in [`AGENTS.md`](AGENTS.md).

## Local verification (docs-only)

There is no local build or test suite. For documentation changes:

```bash
git diff --check
git status --short
```
