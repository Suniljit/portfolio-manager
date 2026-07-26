# ADR 014 — Local Git Hooks via `pre-commit`

**Status:** Accepted

## Context

CI (`.github/workflows/ci.yml`) runs lint, format-check, typecheck, and tests for both the backend (`uv run ruff check .`, `uv run ruff format --check .`, `uv run ty check`, `uv run pytest`) and frontend (`npm run lint` / oxlint, `npm run format:check` / prettier, `npm run test` / vitest), but none of this runs locally before a commit or push — issues are only caught after a PR is opened.

The repo mixes a Python backend and a JS frontend, which rules out a JS-only hook runner (Husky) without still shelling out to `uv run ...` from inside it.

## Decision

Use the [`pre-commit`](https://pre-commit.com) framework, configured in `.pre-commit-config.yaml` at the repo root, added as a backend dev dependency (`uv add --dev pre-commit`).

- **Backend checks** (`ruff` lint + `ruff format --check`) use the official `astral-sh/ruff-pre-commit` hooks, mirroring the CI commands exactly.
- **Frontend checks** (`oxlint`, `prettier --check`) are `local` hooks that invoke the binaries already installed in `frontend/node_modules/.bin/` directly — no new npm dependency (Husky, lint-staged) needed.
- **Commit-time hooks** (lint + format only) run against staged files only, for fast feedback.
- **Push-time hooks** (`ty check`, `pytest`, `npm run test`) run against the whole repo, matching CI 1:1, via pre-commit's `pre-push` stage. These are intentionally excluded from the commit-time hook set since a full typecheck/test run on every commit would be too slow.
- `default_install_hook_types: [pre-commit, pre-push]` in the config means a single `uv run pre-commit install` registers both git hook types.

## Consequences

- Every contributor must run `uv run pre-commit install` once per clone (documented in [CLAUDE.md](../../CLAUDE.md)) — hooks are not active by default after `git clone`.
- The `ruff-pre-commit` hook version is pinned independently of the `ruff`/`ty` versions in `pyproject.toml` (which have no upper bound); these need to be bumped together manually to avoid the local hook and CI drifting apart.
- Frontend hook entries call `frontend/node_modules/.bin/{oxlint,prettier}` directly, so `npm ci --prefix frontend` must have been run at least once before hooks can pass — consistent with the existing dev setup.
- Slow checks (typecheck, full test suites) only run on `git push`, not `git commit` — a commit can still land locally with a type error or failing test, caught either at push time or by CI on the PR.
