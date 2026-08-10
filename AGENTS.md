# AGENTS.md

Guidance for coding agents working in this repository.

## Repository context

This is a near-empty GitHub profile/configuration repository. On the current
branch you should expect:

- `.github/workflows/blank.yml` — starter GitHub Actions workflow (`CI`) with
  placeholder `echo` steps
- `README.md` — human-facing description of the repository and CI behavior

There is no application code, dependency manifest, build system, service
configuration, or test suite on the current branch.

## Development constraints

- Do not install dependencies unless a manifest is added.
- Do not start services; none are configured.
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
- manual `workflow_dispatch`

The `build` job uses `actions/checkout@v3` and two placeholder shell steps. It
does not validate source code, dependencies, or deployments.

## Unmerged remote experiments

Do **not** treat these as active default-branch behavior unless they land on
the working branch:

- `Daan198-patch-1` — historically included a `login` placeholder and a
  `python-package.yml` workflow experiment
