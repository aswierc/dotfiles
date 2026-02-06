---
description: Initialize a plan folder in the current repo (.codex/plans/<id>/)
agent: orchestrator
---

Create a plan folder in the current repository:
- location: `./.codex/plans/<id>/`
- files: `00_task.md`, `10_architekt.md`, `20_db.md`, `30_dev.md`, `99_status.md`, `README.md`

Use `$ARGUMENTS` as the plan id.

Run and show results:
!`bash -lc 'set -euo pipefail
ID="${ARGUMENTS:-}"
if [ -z "$ID" ]; then echo "Usage: /plan-init <id>" >&2; exit 1; fi
if ! printf "%s" "$ID" | grep -Eq "^[A-Za-z0-9][A-Za-z0-9._-]*$"; then echo "Invalid id: $ID" >&2; exit 2; fi

BASE=".codex/plans/$ID"
if [ -e "$BASE" ]; then echo "Already exists: $BASE" >&2; exit 3; fi

TEMPLATE="$HOME/.config/opencode/templates/plans/00_task.md"
if [ ! -f "$TEMPLATE" ]; then echo "Missing template: $TEMPLATE" >&2; exit 4; fi

mkdir -p "$BASE"
cp "$TEMPLATE" "$BASE/00_task.md"
perl -pi -e "s/<id>/$ID/g" "$BASE/00_task.md"

PLAN_FILE="$BASE/${ID}_plan.md"
cat > "$PLAN_FILE" <<EOF
# Plan: $ID

Each checkbox below is designed to be a separate commit or MR.

## Stages
- [ ] 1) <stage title>
  - Scope:
  - Files:
  - Tests:
  - Rollback:
  - MR title:

- [ ] 2) <stage title>
  - Scope:
  - Files:
  - Tests:
  - Rollback:
  - MR title:

- [ ] 3) <stage title>
  - Scope:
  - Files:
  - Tests:
  - Rollback:
  - MR title:
EOF

printf "# Architecture (DDD)\\n\\n" > "$BASE/10_architekt.md"
printf "# Database (MySQL)\\n\\n" > "$BASE/20_db.md"
printf "# Implementation\\n\\n" > "$BASE/30_dev.md"
printf "# Status\\n\\n## Done\\n\\n- [ ] Initialized\\n\\n## Need review\\n\\n- [ ] @architect\\n\\n## How to run/test\\n\\n- <fill>\\n" > "$BASE/99_status.md"
printf "# Plan %s\\n\\nFolder: `./%s/`\\n\\nFiles:\\n- `00_task.md`\\n- `%s_plan.md`\\n- `10_architekt.md`\\n- `20_db.md`\\n- `30_dev.md`\\n- `99_status.md`\\n" "$ID" "$BASE" "$ID" > "$BASE/README.md"

echo "Initialized: $BASE"
ls -la "$BASE"
'`
