# Global Claude Code rules

## Core workflow (gated)

Default loop for any non-trivial task:
1) **explorer subagent** (read-only) to find relevant files and entry points.
2) **architect subagent** to produce short, actionable design notes.
3) **STOP**. Do not edit code, do not run tests, do not exit plan mode.
4) Only after the user explicitly approves with one of: `GO`, `APPROVE`, `OK IMPLEMENT`:
   - (Optional) run a DB review pass (db-guardian) if the change touches SQL.
   - proceed to implementation stage-by-stage (each stage = one commit/MR).

## Planning artifacts

All plans live in the repo under:
`./.codex/plans/<id>/`

Required outputs for a plan id `<id>`:
- `00_task.md` — context/goals/constraints/refs
- `<id>_plan.md` — staged checklist (each checkbox = one commit/MR)
- `10_architekt.md` — architecture notes (compact bullets, no ADRs)
- `30_dev.md` — implementation notes/risks
- `99_status.md` — status + how to run/test

## Token discipline

- Prefer file tools (read/glob/grep) over large copy/paste.
- Keep outputs compact; prefer bullets over prose.
- For exploration: return file paths and “next file to open” suggestions; avoid reading many files at once.

## Safety

- Never touch production or external databases.
- Prefer local/dev containers for DB work.
