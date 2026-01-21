# OpenCode handoff (template)

Goal: exchange context between `orchestrator` → subagents through `.md` files.

Suggested workflow in a repo:
1) Create: `./.opencode/handoff/<id>/`
2) Copy `00_task.md` as `./.opencode/handoff/<id>/00_task.md`
3) Set output paths in `00_task.md`:
   - `10_architekt.md` (architecture)
   - `20_db.md` (DB)
   - `30_dev.md` (implementation notes)
   - `99_status.md` (status/run/test)

