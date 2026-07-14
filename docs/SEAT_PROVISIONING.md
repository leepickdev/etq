# Seat Provisioning

Start with one project owner. Add review, QA, or runtime-specific seats only when a concrete task needs them. Use [LANE_PROVISIONING.md](LANE_PROVISIONING.md) when a manager needs to route active work, park future work, or give a new agent a complete pickup bulletin.

## Minimal Flow

1. Install project-local agent guidance with `setup`.
2. Initialize the project with `bootstrap local`.
3. Read `AGENTS.md`, `BOARD.md`, `SESSION_PICKUP.md`, and `SEAT_OPERATING_MANUAL.md`.
4. Run `whereami`, `doctor`, and `status`.
5. Confirm the lead seat.
6. After interrupted sessions, cwd/worktree ambiguity, role changes, or vendor swaps, rerun `whereami`, `doctor`, and `notify poll`.
7. Treat lifecycle/readiness checks as evidence only; they do not authorize work.
8. Have the lead seat `join` and `pickup` the first generated task.
9. Add extra sessions only when starter sessions are not enough.
10. Give each seat its allowed writes and validation.
11. Record a receipt before asking for promotion.

```sh
etiquette setup --target codex --project "$PWD"
etiquette bootstrap local --project "$PWD" --task-prefix APP
etiquette whereami --project "$PWD" --seat impl-seat --task APP-001
etiquette doctor --project "$PWD"
etiquette status --project "$PWD"
etiquette join --project "$PWD" --seat impl-seat
etiquette pickup --project "$PWD" --seat impl-seat --task APP-001 --text
etiquette console board --project "$PWD" --text
```

## Seat Types

Use `control_seat` for local workflow ownership, `execution_seat` for bounded implementation, `review_seat` for pressure testing, and `seat_maintainer` for runtime-specific guidance. Seats are roles. People and model sessions occupy them.

## Greenfield Setup

```sh
etiquette bootstrap local --project "$PWD" --task-prefix FOOD \
  --lead-seat impl-seat --lead-principal developer-1
```

```sh
etiquette whereami --project "$PWD" --seat impl-seat --task FOOD-001
etiquette join --project "$PWD" --seat impl-seat
etiquette pickup --project "$PWD" --seat impl-seat --task FOOD-001 --text
```

The starter runbook is enough for normal pickup. Use `session create` only when an extra ad hoc session needs a different scope. The lead seat coordinates and implements. Add a review seat with `--profile lead-review` only when someone will actually pressure-test. Neither gets merge or promotion authority unless policy grants it. Hooks, readiness, rebind, and lifecycle preflight are evidence only; the task envelope and allowed writes remain the active work authority.

## Child Runners

Use node delegation when a lead seat or runner needs bounded child work without creating a new durable seat.

The parent issues an explicit child lease. The child lease must be a subset of the parent lease: same workflow and lane, shorter or equal TTL, narrower or equal authority scope, subset tools, subset write paths, inherited forbidden actions, reduced child budget, and reduced depth.

Child runners return to their immediate parent. The parent synthesizes one upstream receipt and owns cleanup. A child or headless node is disposable by default; durable seat status still requires enrollment and readiness.

## Runtime Seats
Runtime-specific seats are optional adapters. Add them after task assignment:

```sh
sh templates/seat-packs-v0/bin/provision-seat codex /tmp/dev-codex-seat
sh templates/seat-packs-v0/bin/provision-seat claude-code /tmp/dev-claude-code-seat
sh templates/seat-packs-v0/bin/provision-seat gemini /tmp/dev-gemini-seat
sh templates/seat-packs-v0/bin/provision-seat ollama /tmp/dev-ollama-seat
sh templates/seat-packs-v0/bin/provision-seat openrouter /tmp/dev-openrouter-seat
```

Use `auto` only when exactly one runtime is obvious; use `seat-session-bootstrap` inside a live agent session.

For bounded, cursor-based wake checks on any seat, use the portable core command: `etiquette notify poll --seat <id> --after-seq <n>`. It is read-only and does not grant authority. Seat packs do not bundle coordination-bus monitor skills; monitoring stays operator-armed.

## Readiness

```sh
etiquette seat readiness \
  --project "$PWD" \
  --seat impl-seat \
  --seat-type execution_seat \
  --execution-surface codex \
  --capability-source local_validation \
  --operational-status operational \
  --model-tier frontier_high_reasoning

etiquette seat status --project "$PWD"
```

Agent confidence is not readiness. Readiness is declared capability plus local evidence.

## Managed Runtime Infrastructure
Remote execution is a later layer. Plane provisioning is infra-admin scoped. Workspace provisioning is bounded to the verified initiator and owner. Neither grants workflow authority by itself.

## Rules
- Start with the smallest useful topology.
- Add seats because work requires them.
- Product-write authority requires a task, allowed writes, validation, and the right promotion gate.
- Chat is not canonical record.
- Runtime packs are adapters, not doctrine.
