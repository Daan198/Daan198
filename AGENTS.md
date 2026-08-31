# AGENTS.md

Guidance for coding agents working in this repository.

## Repository context

This is a near-empty GitHub profile/configuration repository. The repo name
matches the account, so `README.md` on `main` is also the public profile README.

On the current branch you should expect:

- `.github/workflows/blank.yml` — starter GitHub Actions workflow (`CI`) with
  placeholder `echo` steps
- `README.md` — human-facing description of the repository, CI, runbook, and
  troubleshooting

There is no application code, dependency manifest, build system, service
configuration, or test suite on the current branch.

## Development constraints

- Do not install dependencies unless a manifest is added.
- Do not start services; none are configured.
- Do not invent application, Python, or login behavior from unmerged branches.
- Keep documentation-only changes focused on verified repository behavior.
- Prefer updating `README.md` for human-facing workflow and troubleshooting
  notes instead of adding overlapping doc pages.

## Verification

Because there is no build, test, or lint command, use lightweight checks for
documentation-only changes:

```bash
git diff --check
git status --short
```

If code, package manifests, or real CI steps are added later, update this file
and `README.md` with the exact local verification commands.

## CI notes

Workflow: `.github/workflows/blank.yml` (`CI`)

Runs on:

- push to `main`
- pull requests targeting `main`
- manual `workflow_dispatch` (no inputs)

The `build` job uses `actions/checkout@v3` and two placeholder shell steps. It
does not validate source code, dependencies, or deployments. It does not
reference secrets.

## Unmerged remote experiments

Do **not** treat these as active default-branch behavior unless they land on
the working branch:

- `Daan198-patch-1` — historically included a `login` placeholder and a
  GitHub starter `python-package.yml` (Python 3.9–3.11, flake8, pytest). That
  workflow is not active on `main`.
