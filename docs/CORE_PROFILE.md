# Etiquette Core Profile

Etiquette Core is the bare-bones governance flavor for senior engineers who
want the original promise without the managed runtime surface.

Core includes:

- seat readiness and heartbeat;
- workflow mode validation and checks;
- rubric validation, local sandbox receipts, and promotion checks;
- operational dispatch check and record;
- local ledger indexing, search, and show;
- vanilla kernel docs, task cards, receipts, and the local ledger.

Core excludes by default:

- hosted runtime and EKS provisioning;
- MCP server;
- external planning adapter;
- memory-store lifecycle and drains;
- agent-plane profiles;
- console/site;
- remote sync joins and merge-driver setup;
- auth screening and enterprise rollout surfaces.

## Primitive Map

Core records, validates, gates, and dispatches:

| Layer | Core primitive |
| --- | --- |
| Record | seats, owner/readiness, task envelopes, ledger, receipts |
| Reflect | rubrics, local validation, reconciliation by review |
| Gate | human/Git promotion over grants, receipts, and validation |
| Execute | local shell, local worktree, local runner; authority-false |
| Act | dispatch advice, receipt return, next-owner routing |

Full remembers, consolidates, marinates, and projects. Memory stores,
consolidation rollups, marination modules, hosted portals, secure screening,
remote runtime cells, and sharded drains belong there unless explicitly enabled.

Use:

```sh
./bin/etiquette-core help
./bin/etiquette-core workflow explain mixed --json
./bin/etiquette-core seat status --project .
```

The full `./bin/etiquette` CLI still exposes optional runtime, hosted,
adapter, memory, console, sync, and release surfaces.

## Authority Gate

Core keeps authority explicit without adding a daemon or remote plane.

The Core promotion path is:

1. An agent or developer writes candidate work under the task boundary.
2. The candidate includes receipts and validation evidence.
3. A human reviews the diff and receipts.
4. Git merge is the canonical promotion gate.
5. The ledger records the promoted result.

At Core scale, Git is the promotion mechanism. Drains, sharded import, hosted
planes, and runtime cells belong to the Full profile unless explicitly enabled.

Core commands may advise, check, and record evidence. They do not authorize
work, attach grants, merge, close lanes, or promote candidates without the
human review and Git gate.
