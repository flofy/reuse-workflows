# Usage

## Call the shared Node.js workflow

Copy `.github/workflows/caller-example.yml` into the consuming repository as `.github/workflows/ci.yml`, then adapt the commands to the scripts that actually exist in that project.

The reusable workflow supports:

- Node.js version selection, defaulting to Node.js 24.
- npm or pnpm dependency installation.
- Optional lint, typecheck, test, and build commands.
- A 15-minute job timeout.
- Skipping validation for draft pull requests.

For pnpm projects, set `package-manager: pnpm`. The default install command is `pnpm install --frozen-lockfile`; pnpm 10 is installed by default. Override the install command if a repository needs a different version or setup.

## Draft pull request behavior

The caller workflow must include these pull request event types:

```yaml
pull_request:
  types: [opened, synchronize, reopened, ready_for_review]
```

The reusable job checks `github.event.pull_request.draft` and skips while the PR is a draft. When the PR is marked ready, GitHub emits `ready_for_review` and the job runs. Pushes to `main` still run validation.

Use a concurrency group in the caller workflow to cancel superseded runs for the same PR. GitHub Actions concurrency is configured at the caller level in the example.

## Important

- This workflow centralizes GitHub Actions checks; it does not control Netlify, Cloudflare, or other external build systems.
- Do not assume every repository has the same scripts. Empty command inputs skip those steps.
- Prefer a reviewed version tag such as `@v1` over `@main` for production callers once releases are published.
- A skipped draft job is not a substitute for validation: mark the PR ready only after reviewing the diff and running the relevant checks locally where practical.
