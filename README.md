# Daan198

Public GitHub profile and configuration repository (`Daan198/Daan198`).
GitHub’s repository description is “Config files for my GitHub profile.”

The default branch currently ships a starter GitHub Actions workflow only—there
is no application source, package manifest, or deploy pipeline.

A `README.md` on `main` is also the public GitHub profile README for this
account. Keep the top of this file short if the profile page should stay brief;
put operational detail in the sections below.

## Layout

| Path | Role |
| --- | --- |
| [`.github/workflows/blank.yml`](.github/workflows/blank.yml) | Only workflow on `main` (display name `CI`) |
| [`AGENTS.md`](AGENTS.md) | Constraints for coding agents |

GitHub Issues are disabled on this repository. Use pull requests for discussion
and change review.

## Developer setup

No language toolchain, package manager, or local services are required.

```bash
git clone https://github.com/Daan198/Daan198.git
cd Daan198
```

Edit files, then open a pull request targeting `main`. That PR is what starts
automatic `CI` (pushes to feature branches do not).

## CI workflow

- Workflow display name: `CI` (Actions tab)
- File: [`.github/workflows/blank.yml`](.github/workflows/blank.yml)
- State: active

### Triggers

| Event | Scope |
| --- | --- |
| `push` | `main` |
| `pull_request` | targeting `main` |
| `workflow_dispatch` | manual run from the Actions tab (no inputs defined) |

There is no `concurrency` group, so overlapping runs are not cancelled.

### Job: `build`

Runs on `ubuntu-latest` and executes:

1. `actions/checkout@v3` — checks out the repository into `$GITHUB_WORKSPACE`
2. **Run a one-line script** — `echo Hello, world!`
3. **Run a multi-line script** — two `echo` lines (placeholder build/test/deploy
   guidance)

The workflow does not set `shell:`. On GitHub-hosted runners the `run:` steps
use bash with `set -e` (`/usr/bin/bash -e {0}`).

A green run means the runner started and executed those shell steps. It does
**not** prove application correctness, dependency health, or deploy readiness.

The job does not install packages, run tests or linters, publish artifacts, or
reference repository secrets. The workflow does not set a `permissions:` block.

### Expected log output

Successful `run:` steps print:

```text
Hello, world!
Add other actions to build,
test, and deploy your project.
```

Recent pull-request checks for this workflow have finished in about 5–11
seconds.

### `actions/checkout@v3` and Node 20

`actions/checkout@v3` still targets Node.js 20. Current GitHub-hosted runners
force that action onto Node.js 24 and emit a job warning similar to:

```text
Node.js 20 is deprecated. The following actions target Node.js 20 but are being
forced to run on Node.js 24: actions/checkout@v3.
```

That warning does **not** fail the job. Replacing the placeholder steps will
not remove it; bumping the checkout action (for example to `@v4` or a SHA pin)
will. Until then, treat the warning as expected noise, not a broken workflow.

## Manual run (runbook)

1. Open the repository **Actions** tab and select the `CI` workflow (not the
   filename `blank.yml`).
2. Use **Run workflow** (`workflow_dispatch`). There are no workflow inputs to
   fill in.
3. Confirm the `build` job on `ubuntu-latest` completes checkout plus the two
   `echo` steps, and that the log contains the expected output above.

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
in the tree. If you add another workflow file under `.github/workflows/`,
document it here—the default branch currently has only `blank.yml`.

## Troubleshooting

| Symptom | Cause / what to do |
| --- | --- |
| Push to a feature branch did not start `CI` | Automatic triggers only watch `main`. Open a PR targeting `main`, or use **Run workflow**. |
| Cannot find workflow `blank.yml` in Actions | The UI lists the workflow `name:` (`CI`). The file is still `.github/workflows/blank.yml`. |
| `CI` is green but nothing was tested | Expected: the job only echoes placeholders. |
| Job warning about Node.js 20 / `checkout@v3` | Expected on current runners; the job still succeeds. See above. |
| Expected Python lint/pytest | That experiment is not on `main`. See `AGENTS.md` (unmerged `Daan198-patch-1`). |
| Manual dispatch has nothing to configure | `workflow_dispatch` is declared without `inputs`. |
| Cannot file a GitHub Issue | Issues are disabled for this repository; use a pull request. |

## Local verification (docs-only)

There is no local build or test suite. For documentation changes:

```bash
git diff --check
git status --short
```
