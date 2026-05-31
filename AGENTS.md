# stonerelay — Agent Instructions

Obsidian community plugin for Notion → Obsidian vault sync. TypeScript + esbuild + Vitest. Forked from ran-codes/obsidian-notion-database-sync.

## Non-negotiables

- **Never** `git add -A` or `git add .` — stage explicit paths only.
- **Never** commit `.env*` files or secret values.
- **Always** run tests before marking done.
- **Always** commit + push when work is complete.

## Build + test

```bash
# Build (type-check + esbuild bundle)
npm run build  # tsc -noEmit -skipLibCheck && node esbuild.config.mjs production

# Test (Vitest — Obsidian API is mocked, no external services needed)
npm test  # vitest run

# Integration tests (requires NOTION_API_KEY)
VITEST_INTEGRATION=1 npm run test:integration
```

## Repo layout

```
stonerelay/
├── src/                    # Plugin source
├── tests/                  # Unit tests (Obsidian mocked via tests/obsidian-mock.ts)
├── esbuild.config.mjs      # Build config
├── manifest.json           # Obsidian plugin manifest
└── main.js                 # Built output (esbuild)
```

## Verification gate

1. `npm run build` — PASS
2. `npm test` — PASS (275+ unit tests)
3. Commit staged changes
4. `git push`

## Cursor Cloud specific instructions

- **All 275+ unit tests pass without external services.** Obsidian API is fully mocked via `tests/obsidian-mock.ts`.
- **Integration tests** require `NOTION_API_KEY` env var and are skipped by default.
- **No lint script**: type-checking is part of the build command (`tsc -noEmit -skipLibCheck`).
