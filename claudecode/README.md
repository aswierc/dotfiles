# Claude Code dotfiles

This directory provides a **GitHub-friendly**, **project-agnostic** Claude Code setup that mirrors the workflow used in `opencode/`.

Core idea: use a **gated agentic loop**:
1) Explore (read-only)
2) Architect (short bullets)
3) STOP
4) Only after explicit approval, implement stage-by-stage

Plan files live in the **same place** as OpenCode:
`./.codex/plans/<id>/`.

## Install

Copy (or symlink) into `~/.claude/`:

```sh
mkdir -p ~/.claude
rsync -a --delete ./Projects/dotfiles/claudecode/ ~/.claude/
```

## Daily workflow

1) Start Claude Code in your repo (Plan Mode recommended for the first phase).
2) Create a plan folder:

```text
/plan-init JIRA-1234
```

3) Fill `./.codex/plans/JIRA-1234/00_task.md`.
4) Ask Claude to:
   - run the custom subagent **explorer** (read-only) to map relevant files,
   - then run the custom subagent **architect** to write `10_architekt.md` (compact).
5) Review `JIRA-1234_plan.md` and `10_architekt.md`. When you’re happy, explicitly approve:
   - `GO` / `APPROVE` / `OK IMPLEMENT`
6) Start implementation:

```text
/go-implement JIRA-1234
```

Optional DB step:
- Run the `db-guardian` subagent to validate queries, EXPLAIN plans, and indexing notes, and to fill `20_db.md`.

## What’s included

- `CLAUDE.md` — global rules for the gated loop and token discipline
- `settings.json` — user-level settings (no secrets)
- `agents/*.md` — custom subagents (explorer, architect, db-guardian, implementer)
- `skills/*/SKILL.md` — skills that act as slash commands (`/plan-init`, `/go-implement`)
- `templates/*` — templates used by `/plan-init`
