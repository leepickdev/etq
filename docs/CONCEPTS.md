# Core Concepts

Etiquette is a governance and evidence layer for agent-assisted engineering
work. It does not try to be the agent, the IDE, the chat room, or the cloud
runtime.

## The Loop

```text
seat -> task envelope -> session -> execution -> receipt -> promotion gate
```

Core records, validates, gates, and dispatches. Exec runs and returns evidence.
Full remembers, consolidates, marinates, and projects.

## Seat

A seat is a durable work identity. A human, agent, or runtime can occupy it, but
the seat is the thing the workflow routes to.

Do not confuse:

| Concept | Answers |
| --- | --- |
| Operator principal | Who is accountable for intent or approval? |
| Seat | What durable work role or capability is acting? |
| Runtime | Which tool or model executed? |
| Session | Which bounded run produced evidence? |

## Task Envelope

A task envelope says what work is allowed: owner, mode, allowed writes,
forbidden writes, validation, stop conditions, expected receipt, and next owner.

If a task does not name the write boundary and validation, it is not ready for
autonomous execution.

## Session

A session is a bounded run inside one repo. Use one for a bug fix, feature
slice, review, release canary, or short swarm; not for a product, quarter, or
org.

Rebind reattaches a live session to the current ledger, task, branch, and worktree after interruption or runner/vendor change.

## Receipt

A receipt proves what happened: changed files, validation, runbook refs,
blockers, risks, and next owner. It is evidence; it does not approve itself.

## Ledger

A ledger is the durable work record for a repo or workspace: decisions,
receipts, state changes, and refs. Raw execution chatter belongs in session
runbooks and scratch space.

## Promotion Gate

The promotion gate is where candidate work becomes accepted truth.

The gate is resolved by policy: owner, role, quorum, risk class, changed
surface, and current standing. It should not be hardcoded to one person unless
policy says that person owns the action class.

## Authority Lease

An authority lease is a narrow, expiring permission to spend an existing grant.
Spend can nest, bounded. Mint never nests.

V0 leases cover reversible work, tool use, validation, candidate return, and
local orchestration. They never cover auto-merge, signing, release, protected
branch push, secret rotation, cloud activation, or policy mutation.

Every lease check happens at the canonical point of effect, not from a stale
local cache. Telemetry can observe the action. It is not the audit log.
`can_auto_merge_in_v0: false` is required in V0.

## Node Delegation

Node delegation is topology, not authority.

A parent seat, runner, or orchestrator may delegate bounded work to a child
runner only through an explicit lease.

A child lease must be a strict subset of the parent lease. The subset covers
shorter or equal TTL, narrower or equal authority scope, subset write paths,
subset tools, inherited prohibitions, reduced spawn budget, and reduced depth.

Children return to their immediate parent. The parent synthesizes one upstream
receipt and remains accountable for child cleanup. A child or headless node is
not a durable seat unless it is separately enrolled and passes readiness.

## Exec

Exec is any runtime that does work: a local shell, Codex, Claude Code, Gemini,
Ollama, a script, a container, or a remote runtime cell.

Exec may run, observe, retry safe work, and return evidence. Exec must not
grant, merge, close, promote, or mutate canonical truth.

## Memory

Memory is cited context. It helps a seat find prior decisions, receipts, risks,
and patterns.

Memory proposes. Ledgers authorize. Receipts prove. Audit logs account.

Evidence consolidation creates compact rollups from recorded evidence.
Marination is a separate reflective practice over doctrine, drift, and repeated
failure patterns. Both produce proposals, not silent truth changes.

## Integrations

External tools keep their native jobs: chat is conversation, planning tools are
planning, code hosts are review, observability is incident evidence, and
identity systems are identity.

Etiquette is the accountability spine. External "Done" is not acceptance.
Authentication is not authorization.

## Short Rules

```text
Receipts prove work.
Grants authorize consequential action.
Sessions bound execution noise.
Portals display and coordinate.
Integrations project refs.
Execution returns evidence; it never mints authority.
```
