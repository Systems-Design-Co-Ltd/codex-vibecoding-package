# codex-vibecoding-package

Toolkit and playbook for building VibeCoding-compatible codex agents.
This repo hosts shared guidelines (in `AGENTS.md`) and execution plans
(`PLANS.md`) plus any future SDK source code.

## Repository Layout

- `AGENTS.md`: ground rules for every contributor.
- `PLANS.md`: canonical ExecPlan template and working log.
- `docs/`: backing docs (requirements, plan snapshots, changelog, etc.).

Add product code under `src/`, prompts under `assets/`, shared helpers
under `src/lib/`, and CI or workflow files under `.github/` as the
project grows.

## Quick Start

```bash
pnpm install
pnpm dev --filter codex-vibecoding-package
pnpm build
pnpm test
pnpm lint
```

Run commands from the repo root using the Node version in `.nvmrc`.
Prepare `.env.local` before touching external APIs, and prune the pnpm
store (`pnpm store prune`) if caches misbehave.

**Before committing:** `pnpm lint && pnpm typecheck && pnpm test`. Share
results in every PR alongside `pnpm build`.

## Working Agreements

- Follow TypeScript strict mode, prettier/eslint defaults, and
Conventional Commit messages.
- Prefer feature flags (`config/feature-toggles.json`) for risky work.
- Update `docs/changelog.md` and relevant requirements docs with every
feature.
- Reference order: latest chat > `AGENTS.md` in cwd > root `AGENTS.md` >
other docs.

## AGENTS.md Creation Cheat Sheet

1. Copy the existing scaffold when bootstrapping a new workspace or
   package.
2. Fill in the project overview, directory map, and command table so a
   newcomer can ship within one sprint.
3. Capture lint/test/build expectations, code-style rules, PR checklist,
   and “Don’ts” that must stay red-lined.
4. Document escalation paths and priority rules (e.g., chat instructions
   vs. AGENTS vs. README) so conflicts resolve deterministically.

Whenever priorities, tooling, or policies change, edit `AGENTS.md` first
and reference it from PR descriptions so downstream agents inherit the
update.

## PLANS.md / ExecPlan Authoring Flow

1. Open `PLANS.md` as soon as work exceeds a single-file edit, spans
   >30 minutes, or involves multiple stakeholders.
2. Duplicate the ExecPlan template section and write a goal-oriented
   summary describing the desired behavior and validation strategy.
3. Break delivery into milestone lists with concrete commands, files to
   touch, risks, and verification steps; keep the doc self-contained for
   a brand-new contributor.
4. Update progress, discoveries, and design decisions directly inside
   the plan as you work so anyone can resume from the latest entry.

Never ship a feature without an up-to-date plan; treat `PLANS.md` as
your long-term memory and link it in issues/PRs for traceability.

## Next Steps

1. Read `docs/requirements/README.md` for acceptance criteria before
   feature work.
2. Add the missing source tree (e.g., `src/index.ts`, agent modules,
   Vitest setup) per the guidelines above.
3. Configure CI under `.github/workflows/` mirroring the local pnpm
   commands once the codebase exists.

