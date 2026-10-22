# Flofy reusable workflows

Reusable GitHub Actions workflows shared across Flofy repositories.

## Goals

- Avoid expensive CI runs while pull requests are still drafts.
- Run validation when a pull request becomes ready for review.
- Share common Node.js checks without forcing every repository to use the same build setup.
- Keep deployment previews and other external CI systems independently configurable.

## Work in progress

The first reusable workflow will cover Node.js projects with configurable package manager and commands. See the workflow documentation and examples as they are added.
