## Phase 1 — pnpm standardization and package-manager cleanup

### Objectives

- Use pnpm as the only package manager across local and CI workflows.
- Remove conflicting or redundant package-manager files.

### Tasks

1. Ensure `package.json` has `packageManager` pinned to pnpm.
2. Ensure `pnpm-lock.yaml` exists and is updated.
3. Remove npm/yarn lock artifacts listed above when present.
4. Normalize scripts and workflow commands to `pnpm`.
5. Align README command examples with pnpm-only usage.

### Validation

- `pnpm install` succeeds.
- No conflicting lockfiles remain.
- CI uses pnpm for dependency install and script execution.

---
