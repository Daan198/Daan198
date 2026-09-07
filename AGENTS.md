# AGENTS.md

Guidance for coding agents working in this repository.

## Repository context

This is a near-empty public GitHub profile/configuration repository. The repo
name matches the account, so `README.md` on `main` is also the public profile
README. Keep the README intro short; put runbooks and troubleshooting below it.

On the current branch you should expect:

- `.github/workflows/blank.yml` — starter GitHub Actions workflow (`CI`) with
  placeholder `echo` steps
- `README.md` — human-facing description of the repository, setup, CI, runbook,
  and troubleshooting

There is no application code, dependency manifest, build system, service
configuration, or test suite on the current branch. GitHub Issues are disabled;
do not document an issue tracker.

## Development constraints

- Do not install dependencies unless a manifest is added.
- Do not start services; none are configured.
- Do not invent application, Python, or login behavior from unmerged branches.
- Keep documentation-only changes focused on verified repository behavior.
- Prefer updating `README.md` for human-facing workflow and troubleshooting
  notes instead of adding overlapping doc pages.
- Do not treat a green `CI` run, or a Node.js 20 deprecation warning from
  `actions/checkout@v3`, as evidence of application tests.

## Verification

Because there is no build, test, or lint command, use lightweight checks for
documentation-only changes:

```bash
git diff --check
git status --short
```

Re-read `.github/workflows/blank.yml` before changing CI docs. If code, package
manifests, or real CI steps are added later, update this file and `README.md`
with the exact local verification commands.

## CI notes

Workflow: `.github/workflows/blank.yml` (Actions display name `CI`, currently
active)

Runs on:

- push to `main`
- pull requests targeting `main`
- manual `workflow_dispatch` (no inputs)

The `build` job uses `ubuntu-latest`, `actions/checkout@v3`, and two placeholder
shell steps (`echo Hello, world!` and a two-line echo). It does not validate
source code, dependencies, or deployments. It does not reference secrets or set
`permissions:` / `concurrency:`.

`actions/checkout@v3` currently produces a Node.js 20 deprecation warning on
GitHub-hosted runners; the job still succeeds. Document that warning rather
than treating it as a failed check.

## Unmerged remote experiments

Do **not** treat these as active default-branch behavior unless they land on
the working branch:

- `Daan198-patch-1` — historically included a `login` placeholder and a
  GitHub starter `python-package.yml` (Python 3.9–3.11, flake8, pytest). That
  workflow is not active on `main`.
