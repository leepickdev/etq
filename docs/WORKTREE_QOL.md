# Worktree QoL

Use this when a seat works in a branch, a detached worktree, or a resumed agent
session. The goal is to avoid losing work to ephemeral directories and to keep
project context separate from runner chat history.

## Stable Lane Worktrees

Prefer durable worktrees for lane work:

```sh
mkdir -p ../_worktrees
git worktree add ../_worktrees/APP-001-impl-seat lane/APP-001-domain-foundation
cd ../_worktrees/APP-001-impl-seat
```

Use `/tmp` only for disposable experiments. If a task needs review, return, or
resumption, put the worktree under a predictable project-owned or sibling
directory such as `_worktrees/`.

Recommended naming:

```text
_worktrees/<task-id>-<seat-id>
_worktrees/APP-001-impl-seat
_worktrees/APP-002-review-seat
```

## Resume Discipline

Agent resume restores conversation context. It does not prove repo context.

After any resume, run:

```sh
etiquette whereami --project "$PWD" --seat <seat> --task <task>
git status -sb
git branch --show-current
```

If the runner asks whether to resume in the old session directory or the
current directory, choose the current directory only when it is the intended
project worktree for the task. Do not resume a repo-local task inside a global
coordination repo or unrelated workspace.

## Seat Rebind

After TUI/cmux cutoff, cold restart, role/task change, runner/model/vendor swap,
or directory ambiguity, verify `whereami --json`, `doctor`, `bus status 8`,
branch, and worktree before pickup. Then run lifecycle readiness. Rebind grants
no authority; stale memory is context only.

## If A Worktree Is Gone

Do not reconstruct from chat. Recreate from Git:

```sh
git worktree list
git branch --list 'lane/*'
mkdir -p ../_worktrees
git worktree add ../_worktrees/APP-001-impl-seat lane/APP-001-domain-foundation
cd ../_worktrees/APP-001-impl-seat
etiquette whereami --project "$PWD" --seat impl-seat --task APP-001
```

If the branch was never committed or pushed, treat the lost worktree as lost
work unless there is a durable receipt, patch, or runbook artifact. Do not claim
completion from memory.

## Evidence And Return

Keep detailed execution notes in the session runbook:

```text
docs/work/sessions/session-<task>/RUNBOOK.md
```

Return through the repo-local packet/event flow. Before asking a reviewer to
pick up the task, verify:

```sh
etiquette return check --project "$PWD" --task <task> --seat <seat>
etiquette diagnostics no-return --project "$PWD" --task <task> --seat <seat>
```

For remote/headless runners, use the hard gate:

```sh
etiquette return check --project "$PWD" --task <task> --seat <seat> --remote-runner
```

## Forbidden Shortcuts

- Do not treat an agent transcript as the branch, task, or receipt.
- Do not use a global handshake bus for routine repo-local execution.
- Do not keep long-running implementation work only in `/tmp`.
- Do not ask a reviewer to act until the branch and repo-local return are
  visible.
- Do not merge, close, publish, or promote because a worktree exists.
