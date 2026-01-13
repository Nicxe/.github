## Shared GitHub Actions workflows

This repository contains **reusable GitHub Actions workflows** used across all repos in this workspace.

### Design goals

- **Consistency**: Same workflow names, triggers and behavior across repos.
- **No duplicate runs**: Use `push` triggers (not `pull_request`) and `concurrency` to cancel stale runs.
- **Pinned actions**: Avoid `@main` where possible (e.g. HACS action).

### How repos consume these workflows

Each repo contains thin wrapper workflows in `.github/workflows/` that call into this repo:

- `Release` → `reusable-release.yml`
- `Validate` → `reusable-validate-integration.yml` or `reusable-validate-plugin.yml`
- `Dependabot auto-merge` → `reusable-dependabot-automerge.yml`

Wrappers should reference a stable ref (recommended: a tag like `v1`).
