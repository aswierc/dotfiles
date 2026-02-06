---
description: After approval, run implementation for a plan id
agent: orchestrator
---

The user has approved implementation.

Plan id: `$ARGUMENTS`

Rules:
- Implement stage-by-stage from `./.codex/plans/$ARGUMENTS/${ARGUMENTS}_plan.md` (each checkbox = separate commit/MR).
- Delegate actual code changes to `@implementer`.
- Keep changes small and update `30_dev.md` + `99_status.md` as you go.

Now delegate to `@implementer` for the folder `./.codex/plans/$ARGUMENTS/`.

