# OpenCode config (dotfiles)

## Install

Copy (or symlink) everything into `~/.config/opencode/`:

```sh
mkdir -p ~/.config/opencode
rsync -a --delete ./Projects/dotfiles/opencode/ ~/.config/opencode/
```

## Daily workflow (Orchestrator)

This setup is built around the `orchestrator` agent and a repo-local plan folder:
`./.codex/plans/<id>/`.

1) Start OpenCode in your repo and pick the orchestrator:

```sh
cd /path/to/your/repo
opencode --agent orchestrator
```

2) Initialize a plan folder (creates Markdown handoff files in your repo):

```text
/plan-init JIRA-1234
```

3) Fill `./.codex/plans/JIRA-1234/00_task.md` (context, goals, constraints, references).

4) Ask the orchestrator to delegate:
- `@architect` writes architecture/DDD decisions to `10_architekt.md`
- `@db-guardian` writes DB notes/queries to `20_db.md`
- `@implementer` implements and updates `99_status.md`

Tip: keep `00_task.md` as the source of truth and point agents only to the plan folder.

## Secrets / env vars

Create your own env file (or export vars in your shell profile). Example:

```sh
cp ~/.config/opencode/opencode.env.example ~/.config/opencode/opencode.env
```

Then load it in your shell (zsh example):

```sh
set -a
source ~/.config/opencode/opencode.env
set +a
```

## What’s included

- `opencode.json` — global config (permissions, plugins, providers/models, MCP stubs)
- `agents/*.md` — agents (primary + subagents)
- `commands/*.md` — reusable commands (e.g. `/plan-init`)
- `templates/*` — templates used by commands (plans/handoff)

## Notes

- MCP servers are **enabled by default**.
- If you previously had secrets inside `opencode.json`, assume they are compromised and **rotate** them.
