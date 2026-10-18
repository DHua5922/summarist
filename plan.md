# Plan: pnpm + Biome + quality gates (as discussed)

## Problem
We want this starter Next.js project to be clean and consistent across setup, code quality, and CI guardrails:
1. pnpm-only package management (remove npm/yarn leftovers),
2. Biome-based linting/formatting aligned with best practices,
3. dead-code checks using Knip,
4. TypeScript checks for type errors,
5. bundle-size checks using `size-limit`,
6. GitHub Actions quality workflow to enforce these checks.

## Agreed scope and decisions
- Include **config/scripts + CI + README updates** in scope.
- Biome strictness: **recommended baseline** (high-signal, low-noise).
- Clean up package-manager artifacts:
  - `package-lock.json`
  - `yarn.lock` (if present)
  - `npm-shrinkwrap.json` (if present)
- For size-limit, use a **minimal starter budget** appropriate for a skeleton app.

## Phase 6 — GitHub Actions quality workflow
### Objectives
- Enforce code-quality gates consistently on **every branch** via CI.

### Tasks
1. Create/update a GitHub Action workflow for quality checks.
2. Configure triggers so the workflow runs for pushes/pull requests on every branch.
3. Ensure workflow runs with pnpm and includes:
   - Knip dead-code check,
   - TypeScript typecheck,
   - Biome linting and formatting checks,
   - size-limit bundle-size check.
4. Keep workflow permissions minimal and setup cache-friendly.
5. Document CI quality workflow at a high level in README.

### Validation
- Workflow triggers correctly on pushes/pull requests for every branch.
- CI fails when any configured quality check fails.

---

## Completion checklist
1. `pnpm typecheck`
2. `pnpm lint`
3. `pnpm format` (or check equivalent used by CI)
4. `pnpm knip`
5. `pnpm size`
6. `pnpm test` (if present in project scripts)

## Notes
- Keep changes surgical and limited to this setup scope.
- Avoid unrelated refactors while implementing these phases.
- Preserve current app behavior while improving developer/CI guardrails.
