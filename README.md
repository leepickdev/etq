# Etiquette

**Govern agent-assisted engineering work with seats, evidence, and promotion
gates.** Local-first: your repo is the ledger, receipts are the proof, and no
server ever sees your code.

When several coding agents (and humans) work the same repository, the hard
part isn't running them — it's knowing **who did what, on whose authority,
and what proved it worked**. Etiquette gives each participant a *seat*, each
unit of work a *task envelope*, each completion a *receipt*, and each merge a
*promotion gate* — recorded as plain files and git history you can audit.

Docs: https://etiquekit.com/docs/ · Agents start at: https://etiquekit.com/llms.txt

> This repository is Etiquette's public home: issue tracking, changelog,
> security policy, and signed release artifacts. The source is private while
> the pilot program runs — the same model as other proprietary CLIs with
> public GitHub presences. Releases here carry the identical signed bytes
> served by npm and etiquekit.com.

## Install

```sh
npm install -g @etiquekit/etq        # etq, etiquette, etiquette-core on PATH
curl -fsSL https://etiquekit.com/install.sh | sh   # or: native installer
```

Requires `bun >= 1.3` and `git >= 2.40`. macOS and Linux. The installer
verifies signatures against a pinned public key before anything executes.

## Sixty seconds to a governed workspace

```sh
etq init --project .                  # provision folders, journal, roster
etq doctor --project .                # readiness — green before work
etq bootstrap local --project . \
    --profile codex-cc-gemini --task-prefix APP
etq setup --target auto --project .   # register your agent CLI (explicit)
etq join --seat dev-a --project .
etq console board --project . --text  # the live task board
```

Per-runtime seat packs: `provision-seat claude-code` · `provision-seat codex`
· `provision-seat gemini` · `provision-seat ollama` · `provision-seat openrouter`.

The daily loop is three verbs:

```sh
etq pickup --seat dev-a --task APP-001 --expect-project-id <id> --text
# ... do the work (you, or your agent) ...
etq return check --task APP-001 --seat dev-a   # the evidence gate
```

Every step appends to the workspace journal — an append-only event log inside
your repo. Nothing leaves your machine: no backend, no telemetry, no account.

## Concepts in one breath

| Concept | Answers |
| --- | --- |
| Seat | What durable work role is acting? |
| Task envelope | What writes, validation, and stop conditions are allowed? |
| Session | Which bounded run produced the evidence? |
| Receipt | What proves the work happened? |
| Promotion gate | Where does candidate work become accepted truth? |

Commands can initialize, check, record evidence, and project read models.
They **do not** grant authority, merge, close work, publish, or promote truth.
Execution returns evidence; it never mints authority.

## Verify releases

The release signing public key has this SHA-256 fingerprint — cross-check it
against the copy at https://etiquekit.com/docs/ before trusting a downloaded
key:

```
917fbced1d6a82897ec3441a1d12947803ca4d42a6bc63d3412dee8bf8c3ce31
```

Then `openssl dgst -sha256 -verify <key> -signature SHA256SUMS.sig SHA256SUMS`
and `shasum -a 256 -c SHA256SUMS`. If any step fails: stop, do not install.
