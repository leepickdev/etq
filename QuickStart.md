# Quick Start

Get from zero to a governed working project in about two minutes.

Prereqs: Git, Node 18+ (for npm install) or Bun `>=1.3.0`.

## 1. Get The CLI

The published package:

```sh
npm install -g @etiquekit/etq
# or project-local: npm install @etiquekit/etq
# @etiquekit/core is installed as the local plane's public contract dependency
etq --help
```

Bootstrap a project and run your first cycle:

```sh
cd your-repo
etq bootstrap local --project . --task-prefix DEMO --ask
etq doctor --project .            # expect: rig_doctor: pass
# then follow the printed join/pickup commands
```

Private or air-gapped rollout: use [docs/TEAM_HANDOFF.md](docs/TEAM_HANDOFF.md).

## 2. Initialize A Project

From the project repo:

```sh
ETQ=${ETQ:-etiquette}
"$ETQ" setup --target codex --project "$PWD"
"$ETQ" handoff --project "$PWD" --task-prefix APP
"$ETQ" bootstrap local --project "$PWD" --task-prefix APP --ask
"$ETQ" whereami --project "$PWD" --seat impl-seat --task APP-001
"$ETQ" doctor --project "$PWD"
"$ETQ" join --project "$PWD" --seat impl-seat
"$ETQ" pickup --project "$PWD" --seat impl-seat --task APP-001 --allow-current-project --text
"$ETQ" console board --project "$PWD" --text
```

`bootstrap local` creates repo-local state, seats, task envelopes, pickup docs,
events, and runbooks. It does not grant, publish, merge, close, or promote.
With `--ask`, it asks for the first-run shape, explains that seats are roles and
runtimes are temporary occupants, confirms the default write boundary, and stays
non-blocking in CI or scripted runs.

## 3. Orient The Live Seat

Run `whereami` whenever a developer or agent resumes, changes directories, or
inherits a worktree:

```sh
"$ETQ" whereami --project "$PWD" --seat impl-seat --task APP-001
"$ETQ" pickup --project "$PWD" --seat impl-seat --task APP-001 --allow-current-project --text
```

Runner resume recovers chat context; `whereami` confirms the repo, branch, task
envelope, and runbook. For branch hygiene, read [docs/WORKTREE_QOL.md](docs/WORKTREE_QOL.md).
For in-session pickup UX, use the `seat-session-bootstrap` skill.

## 4. Check And Record Evidence

Create checkable dispatch examples, then run the generated command:

```sh
"$ETQ" dispatch scaffold --project "$PWD" --task-id APP-001 --seat impl-seat
"$ETQ" dispatch check --project "$PWD" --task-id APP-001 --seat impl-seat
```

`dispatch check` derives the scaffold paths from `--task-id`, prints the
resolved path map it used, and accepts explicit path flags only when you need
to override the convention.

`dispatch record` writes local metadata and receipt refs; it does not merge,
close, publish, or grant.

## 5. Stop Conditions

Seat packs: `provision-seat claude-code`, `provision-seat codex`, `provision-seat gemini`, `provision-seat ollama`, `provision-seat openrouter`.
Stop when authority is unclear, validation cannot run, writes exceed the envelope, a secret appears, or the session is unbounded.
