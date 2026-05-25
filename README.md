# Daan198 Repository

This repository currently serves as a lightweight GitHub profile/configuration
repository. Its only active automation is a starter GitHub Actions workflow.
Treat the workflow as a placeholder until application code, tests, or deployment
targets are added.

## Repository structure

| Path | Purpose |
| --- | --- |
| `.github/workflows/blank.yml` | Starter GitHub Actions workflow named `CI`. |
| `AGENTS.md` | Notes for automation agents working in this repository. |

There is no application source tree, package manifest, dependency lockfile, test
suite, or deployment configuration in the current branch.

## Current automation

### GitHub Actions CI

- **Workflow file:** `.github/workflows/blank.yml`
- **Workflow name:** `CI`
- **Primary job:** `build`
- **Runner:** `ubuntu-latest`

The workflow checks out the repository and runs two shell-script steps:

```yaml
- uses: actions/checkout@v3

- name: Run a one-line script
  run: echo Hello, world!

- name: Run a multi-line script
  run: |
    echo Add other actions to build,
    echo test, and deploy your project.
```

These commands do not build, test, package, or deploy application code. They
only confirm that GitHub Actions can start a workflow run.

## When CI runs

The workflow is configured to run in three cases:

1. A push to the `main` branch.
2. A pull request targeting the `main` branch.
3. A manual run from the GitHub Actions `workflow_dispatch` control.

Pushes to other branches do not trigger this workflow unless the branch filter
in `.github/workflows/blank.yml` is changed.

## Extending CI safely

When application code is added, replace the placeholder `echo` steps with
project checks that match the new stack. A typical progression is:

1. Install the runtime and dependencies.
2. Run formatting or lint checks.
3. Run unit tests.
4. Build or package the artifact.
5. Add deployment only after build and test jobs are reliable.

Keep CI commands deterministic and non-interactive so they can run on pull
requests and unattended pushes.

## Local development expectations

At the moment there is nothing to install or run locally:

- No dependency manager is configured.
- No build command exists.
- No test runner or lint command is configured.
- No local services are required.

If any of those change, update this README with the exact setup, verification,
and troubleshooting commands developers should use.

## Troubleshooting

- **Workflow did not run:** Confirm the change was pushed to `main`, opened as a
  pull request targeting `main`, or started manually through `workflow_dispatch`.
- **Workflow passes but does not test code:** This is expected until the
  placeholder `echo` commands are replaced with real project commands.
- **Checkout-related failures:** The workflow uses `actions/checkout@v3`; update
  the action version if repository policy requires a newer pinned version.
- **Missing runtime or dependency commands:** Add the appropriate setup action
  and install command before introducing lint, test, build, or deployment steps.

## Documentation maintenance

Update this README whenever repository behavior changes. In particular, document
new jobs, required secrets, branch filters, local setup commands, deployment
targets, and any checks that developers should run before opening a pull
request.
