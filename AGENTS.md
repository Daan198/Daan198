# AGENTS.md

## Repository context

This is a near-empty GitHub profile/configuration repository. The current branch
contains:

- `.github/workflows/blank.yml` - a starter GitHub Actions workflow that runs
  placeholder `echo` commands.
- `README.md` - human-facing documentation for the repository and current CI.

There is no application code, dependency manifest, build system, service
configuration, or test suite in the current branch.

## Development workflow

- Do not install dependencies unless a manifest is added.
- Do not start services; none are configured.
- Keep documentation-only changes focused on existing repository behavior.
- Prefer updating `README.md` for human-facing workflow and troubleshooting
  notes instead of creating overlapping docs.

## Verification

Because the repository has no build, test, or lint commands, use lightweight
repository checks for documentation-only changes:

```bash
git diff --check
git status --short
```

If code, package manifests, or CI steps are added later, update this file and
`README.md` with the exact commands needed to verify those changes locally.

## CI notes

The only current CI workflow is `.github/workflows/blank.yml`. It runs on:

- push events to `main`
- pull requests targeting `main`
- manual `workflow_dispatch` runs

The `build` job checks out the repository with `actions/checkout@v3` and runs
two placeholder shell steps. It does not validate source code, dependencies, or
deployments.

## Branch notes

- `main` contains the current repository baseline and starter CI workflow.
- Remote branch `Daan198-patch-1` has contained an unmerged Python CI experiment
  and a `login` placeholder file. Do not document those as active behavior
  unless they are merged into the working branch.
