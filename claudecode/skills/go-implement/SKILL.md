---
name: go-implement
description: After user approval, start implementation for a plan id (stage-by-stage).
---

The user has approved implementation for plan id `$1`.

Steps:
1) Verify `./.codex/plans/$1/` exists and contains `$1_plan.md` and `10_architekt.md`.
2) If missing, ask the user to run `/plan-init $1` or fill missing files.
3) Delegate implementation to the `implementer` subagent for folder `./.codex/plans/$1/`.

