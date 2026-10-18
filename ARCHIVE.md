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

## Phase 2 — Biome lint/format configuration hardening

### Objectives

- Enforce consistent formatting and practical linting quality with Biome.

### Tasks

1. Configure `biome.json` for recommended best-practice defaults:
   - recommended rules enabled,
   - Next/React domains where applicable,
   - clean includes/excludes for generated/build output.
2. Keep formatter behavior explicit and deterministic.
3. Ensure scripts support both local and CI flows:
   - `pnpm lint`
   - `pnpm format`
4. Keep rule selection at recommended baseline strictness.

### Validation

- `pnpm lint` passes.
- `pnpm format` is stable/deterministic.
- CI quality workflow includes Biome checks.

---
