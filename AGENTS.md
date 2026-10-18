<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

## Design principles

- **DRY:** Keep each piece of knowledge in one place. Extract genuinely repeated logic without coupling unrelated features or creating abstractions for coincidentally similar code.
- **SOLID:** Give modules a single responsibility, keep interfaces focused, and depend on clear contracts. Make implementations replaceable without changing their consumers, and extend behavior through composition when practical.
- **KISS:** Choose the simplest clear solution that meets the current requirements. Prefer readable code and straightforward control flow.
- **YAGNI:** Implement only what the current task requires. Avoid speculative abstractions, configuration, dependencies, and extension points.
- **Separation of concerns:** Keep routing, presentation, business logic, and data access distinct. Keep business rules out of route files and UI components when they deserve their own modules.
- **Composition over inheritance:** Build behavior by combining small components, functions, and modules. Prefer explicit dependencies over class hierarchies.

## Project structure

Organize application code by feature under `src/features`. Keep Next.js routing and application composition in `src/app`, and global or cross-feature code in `src/shared`.

```text
src/
├── app/                     # Routes, layouts, providers, and application composition
├── features/
│   └── <feature>/           # A cohesive business capability
│       ├── index.ts         # Public API for consumers outside this feature
│       ├── components/      # Feature-specific UI
│       ├── hooks/           # Feature-specific hooks
│       ├── api/             # Feature-specific API
|       ├── dal/             # Feature-specific data access layer
│       ├── utilities/       # Feature-specific utilities
│       └── types/           # Feature-specific types
└── shared/                  # Globals and code used by multiple features and/or app
    ├── components/          # Shared UI primitives
    ├── hooks/               # Shared hooks
    ├── utilities/           # Shared utilities
    ├── config/              # Global configuration
    ├── styles/              # Global styles and design tokens
    └── types/               # Shared types
```

- Create folders only when needed; the tree is a placement guide, not required scaffolding.
- Keep code owned by one feature inside that feature, including its tests and supporting assets. Colocate tests with the code they verify.
- Use `shared` for project-wide globals or code used in more than one place across multiple features and/or `app`. Reuse solely within one feature belongs in that feature. A route importing a feature's public API does not make that feature shared code.
- Keep `shared` independent of `features` and `app`. Features may depend on `shared`; `app` composes features and shared modules. Features must not import from `app`.

## Feature public APIs

- Expose each feature's supported external components, functions, and types through its root `index.ts`. Export only what consumers need, using explicit named exports.
- Consumers in `app` or other features must import from the feature's public API, never its internal paths. For example, use `@/features/<feature>` instead of `@/features/<feature>/components/<component>`.
- Within a feature, use direct relative imports for internal modules instead of importing through its own public API, which can create circular dependencies.
- Keep cross-feature dependencies minimal and acyclic. Compose features in `app` when possible; move code into `shared` only when it meets the shared ownership rules above.
- Keep Next.js server/client boundaries intact. Do not mix server-only implementations into an entry point consumed by client components; add explicit public entry points such as `server.ts` or `client.ts` when needed, and treat other internal paths as private.
