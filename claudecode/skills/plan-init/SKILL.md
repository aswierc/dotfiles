---
name: plan-init
description: Create a gated plan folder in ./.codex/plans/<id>/ (00_task.md + <id>_plan.md + stubs).
---

Create a plan folder in the current repository:
- Location: `./.codex/plans/<id>/`
- Files: `00_task.md`, `<id>_plan.md`, `10_architekt.md`, `20_db.md`, `30_dev.md`, `99_status.md`, `README.md`

Use the first argument as the id.

Steps:
1) Validate `<id>` (letters/numbers/._- only; must not be empty).
2) Create the folder if it does not exist.
3) Copy template `~/.claude/templates/plans/00_task.md` to `./.codex/plans/<id>/00_task.md` and replace `<id>` placeholder.
4) Create `<id>_plan.md` with a 3–8 stage checklist (each item = one commit/MR).
5) Create stub Markdown files: `10_architekt.md`, `20_db.md`, `30_dev.md`, `99_status.md`, plus `README.md` enumerating files.

Keep output minimal: confirm paths created and list the directory.

