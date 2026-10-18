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

## Phase 3 — Dead code checks with Knip

### Objectives

- Detect and prevent unused files/exports/dependencies.

### Tasks

1. Add/verify Knip configuration file and scope.
2. Add/verify `pnpm knip` script.
3. Tune exclusions only where intentional and documented.
4. Document dead-code check usage in README.

### Validation

- `pnpm knip` runs cleanly.
- CI fails on new dead-code issues.

---

## Phase 4 — TypeScript checks for type errors
### Objectives
- Enforce static type safety in local development and CI.

### Tasks
1. Add/verify `pnpm typecheck` script (`tsc --noEmit`).
2. Ensure `tsconfig` supports project/test typing requirements.
3. Document typecheck command in README.
4. Add typecheck to CI quality workflow.

### Validation
- `pnpm typecheck` passes.
- CI fails on type errors.

---

## Phase 5 — Bundle-size guardrails with size-limit
### Objectives
- Add automated bundle-size protection early while the app is still small.

### Tasks
1. Add `size-limit` dependencies/config if missing.
2. Add/verify `pnpm size` script.
3. Configure a minimal starter budget (initial conservative cap).
4. Document the size check in README.
5. Add size check to quality CI workflow.

### Validation
- `pnpm size` runs and enforces the configured budget.
- CI fails if budget is exceeded.

---