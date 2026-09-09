# Contributing to OpenLane

Thanks for building with us. This is a focused guide — the short version first, details after.

## TL;DR

1. Find or open an issue (bugs → `bug`, ideas → `enhancement`).
2. Fork, branch (`feat/<area>-<slug>` or `fix/<area>-<slug>`), commit with conventional commits.
3. `make check` must pass locally (lint + sqlc diff + tests).
4. PR against `main`. Link the issue. Keep the diff minimal.

## Ground rules

- **Smallest working diff wins.** No speculative abstractions, no "while I'm here" refactors — split those into their own PRs.
- **API before UI.** New features land API + tests first, then UI.
- **Every migration touches RLS.** Any new table gets `workspace_id` + policies. CI enforces this.
- **No secrets in code, ever.** Not even test ones. CI runs secret scanning with push protection.
- **Test what you ship.** New logic needs the smallest test that fails if it breaks. Security-relevant changes need an IDOR/authz test.
- **Conventional commits**: `feat(portal):`, `fix(api):`, `chore(db):`, `docs:`.

## Development setup

```bash
git clone https://github.com/openlanelabs/openlane
cd openlane
docker compose up -d        # postgres + redis + vaults3
make dev                    # api + worker + web with hot reload
make check                  # lint + sqlc diff + test
```

Requirements: Go 1.22+, Node 20+, Docker. Nothing else.

## Repo layout

```text
apps/web/          Next.js — internal app + customer portal (no business logic)
apps/api/          Go Chi REST + webhooks + MCP
apps/worker/       Go River jobs + agent runners
db/                goose migrations + sqlc queries + RLS policies
packages/contracts/ OpenAPI 3.1 — source of truth (generates TS client + Go types)
infra/             docker compose + helm
e2e/               Playwright
docs/              spec + ADRs
```

## Where things go

| Change | Where |
|---|---|
| New endpoint | `packages/contracts/openapi.yaml` → regenerate → handler in `apps/api` |
| New table | `db/migrations` + RLS policies + `db/queries` |
| Background work | River job in `apps/worker` |
| UI surface | `apps/web` — uses only the generated TS client |
| Agent | `apps/worker/agents` — needs approval gate + eval fixtures |

## Code review expectations

Reviewers check, in order:

1. **Correctness** — does it do what the issue says, including edge cases?
2. **Security** — RLS on new tables, authz checks, no IDOR, sanitized inputs
3. **API contract** — OpenAPI updated, no breaking change without `/v2` discussion
4. **Tests** — the smallest runnable check for new logic
5. **Size** — can this be smaller?

## Releasing

- `main` is always deployable. Protected by rulesets (see `.github/rulesets.json`).
- Releases are tagged `vX.Y.Z` with generated notes.
- Container images: `ghcr.io/openlanelabs/{api,worker,web}`.

## License

By contributing, you agree your contributions are licensed under **AGPL-3.0** (or the applicable commercial license for enterprise modules).
