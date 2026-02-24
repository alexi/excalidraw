## Cloud-specific instructions

### Overview

Excalidraw is a Yarn 1 monorepo (Node >= 18). The main web app lives in `excalidraw-app/` and depends on library packages in `packages/`. See `CLAUDE.md` for project structure, dev commands, and architecture notes.

### Running the dev server

```bash
yarn start         # Vite dev server on http://localhost:3001
```

The app works standalone for core drawing features. External services (collaboration WebSocket on :3002, AI backend on :3016, Excalidraw Plus on :3000) are optional and not needed for local development.

### Key commands

All commands are defined in the root `package.json`:

| Task | Command |
|---|---|
| Lint (ESLint) | `yarn test:code` |
| Type check | `yarn test:typecheck` |
| Tests (snapshot update) | `yarn test:update` |
| Auto-fix lint + format | `yarn fix` |
| Full CI suite | `yarn test:all` |

### Non-obvious notes

- The pre-commit hook in `.husky/pre-commit` is commented out (lint-staged is disabled), so there is no pre-commit enforcement.
- `vitest` tests use `jsdom` environment with `vitest-canvas-mock`; no real browser or display is needed for tests.
- Firebase config in `.env.development` points to a shared dev project; no secrets are needed for basic development.
- The `Error JSON parsing firebase config` warning in app tests is expected and harmless (Firebase config env var is undefined in test context).
