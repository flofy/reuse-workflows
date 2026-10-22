# Flofy reusable workflows

Reusable GitHub Actions workflows shared across Flofy repositories.

## Available workflows

- [Reusable Node.js CI](.github/workflows/node-ci.yml): configurable npm/pnpm installation and optional lint, typecheck, test, and build commands.
- [Caller example](.github/workflows/caller-example.yml): sample consumer workflow with draft-aware CI and concurrency cancellation.
- [Usage guide](docs/usage.md): setup instructions, draft PR behavior, and adoption notes.

## Design goals

- Avoid expensive GitHub Actions runs while pull requests are still drafts.
- Run validation when a pull request becomes ready for review.
- Share common checks without forcing every repository to use the same scripts.
- Keep deployment previews and other external CI systems independently configurable.

## Adoption

The initial workflow is under review. Consumers currently reference `@main` in the example; after the first review, publish a version tag such as `v1` and prefer that tag in consuming repositories.
