# Task: <title>

## Context
- <why are we doing this?>

## Goals (acceptance)
- [ ] <goal 1>
- [ ] <goal 2>

## Non-goals
- <explicitly out of scope>

## Constraints
- Tech: <language/framework/...>
- Runtime/infra: <db/queues/...>
- Style: <DDD/TDD/...>

## References (links/files)
- <paths to relevant code>
- <docs links>

## Deliverables (files to produce)
- `./.opencode/handoff/<id>/10_architekt.md` — architecture/DDD/invariants/ADR
- `./.opencode/handoff/<id>/20_db.md` — schema/queries/EXPLAIN/indexes/migrations
- `./.opencode/handoff/<id>/30_dev.md` — implementation plan + risks
- `./.opencode/handoff/<id>/99_status.md` — status + how to run/test

## Open questions
- <question 1>
- <question 2>

## Notes for agents
### @architect
- Don’t edit code. Write results to `10_architekt.md`.

### @db-guardian
- Don’t edit application code. Write results to `20_db.md`.

### @implementer
- Implement based on `10_architekt.md` and `20_db.md`. Update `99_status.md`.

