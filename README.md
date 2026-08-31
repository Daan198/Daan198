# Daan198

GitHub profile and configuration repository (`Daan198/Daan198`). The default
branch currently ships a starter GitHub Actions workflow only—there is no
application source, package manifest, or deploy pipeline yet.

A `README.md` on `main` is also the public GitHub profile README for this
account. Keep the top of this file accurate if the profile page should stay
short; put operational detail in the sections below.

## Layout

| Path | Role |
| --- | --- |
| [`.github/workflows/blank.yml`](.github/workflows/blank.yml) | Only active workflow (`CI`) |
| [`AGENTS.md`](AGENTS.md) | Constraints for coding agents |

## CI workflow

- Workflow name: `CI`
- File: [`.github/workflows/blank.yml`](.github/workflows/blank.yml)

### Triggers

| Event | Scope |
| --- | --- |
| `push` | `main` |
| `pull_request` | targeting `main` |
| `workflow_dispatch` | manual run from the Actions tab (no inputs defined) |

### Job: `build`

Runs on `ubuntu-latest` and executes:

1. `actions/checkout@v3` — checks out the repository into `$GITHUB_WORKSPACE`
2. **Run a one-line script** — `echo Hello, world!`
3. **Run a multi-line script** — prints placeholder guidance to add build, test,
   and deploy commands

A green run means the runner started and executed those shell steps. It does
**not** prove application correctness, dependency health, or deploy readiness.

The job does not install packages, run tests or linters, publish artifacts, or
reference repository secrets.

## Manual run (runbook)

1. Open the repository **Actions** tab and select the `CI` workflow.
2. Use **Run workflow** (`workflow_dispatch`). There are no workflow inputs to
   fill in.
3. Confirm the `build` job on `ubuntu-latest` completes the checkout plus the
   two `echo` steps.

Use this when you need a run without a `main` push or a PR targeting `main`.

## Extending CI

When real project checks exist, replace the placeholder `run:` steps. Keep
commands non-interactive and repeatable on both PRs and pushes to `main`.
Pin actions explicitly (the current file uses `actions/checkout@v3`):

```yaml
steps:
  - uses: actions/checkout@v3
  - name: Install dependencies
    run: <dependency install command>
  - name: Run tests
    run: <test command>
```

Adding real install/test steps also requires the matching tooling and lockfiles
in the tree. If you add another workflow file, document it here—the default
branch currently has only `blank.yml`.

## Troubleshooting

| Symptom | Cause / what to do |
| --- | --- |
| Push to a feature branch did not start `CI` | Automatic triggers only watch `main`. Open a PR targeting `main`, or use **Run workflow**. |
| `CI` is green but nothing was tested | Expected: the job only echoes placeholders. |
| Expected Python lint/pytest | That experiment is not on `main`. See `AGENTS.md` (unmerged `Daan198-patch-1`). |
| Manual dispatch has nothing to configure | `workflow_dispatch` is declared without `inputs`. |

## Local verification (docs-only)

There is no local build or test suite. For documentation changes:

```bash
git diff --check
git status --short
```
