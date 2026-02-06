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

This workflow is intentionally **gated**:
1) `@explorer` (read-only) + `@architect` (short design)
2) STOP
3) Only after your explicit approval, implementation starts.

1) Start OpenCode in your repo and pick the orchestrator:

```sh
cd /path/to/your/repo
opencode --agent orchestrator
```

2) Initialize a plan folder (creates Markdown handoff files in your repo):

```text
/plan-init JIRA-1234
```

This creates:
- `./.codex/plans/JIRA-1234/00_task.md` — context/goals/refs
- `./.codex/plans/JIRA-1234/JIRA-1234_plan.md` — staged checklist (each checkbox = one commit/MR)

3) Fill `./.codex/plans/JIRA-1234/00_task.md`.
4) Ask the orchestrator to run the initial analysis phase:
- `@explorer` maps relevant files (read-only, minimal output)
- `@architect` writes `10_architekt.md` (compact bullets, no ADRs)

5) Review `JIRA-1234_plan.md` and `10_architekt.md`, then approve implementation with one of:
- `GO`
- `APPROVE`
- `OK IMPLEMENT`

6) Start implementation (explicit command):

```text
/go-implement JIRA-1234
```

Tip: keep the plan folder as the source of truth and point agents to `./.codex/plans/JIRA-1234/`.

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
- `commands/*.md` — reusable commands (e.g. `/plan-init`, `/go-implement`)
- `templates/*` — templates used by commands (plans/handoff)

## Notes

- MCP servers are **enabled by default**. If startup is slow or MCP tools time out, disable unneeded servers in `opencode.json`.
- If you previously had secrets inside `opencode.json`, assume they are compromised and **rotate** them.
