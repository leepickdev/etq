# Changelog

All published versions of `@etiquekit/etq`. Artifacts for each version are
attached to the matching GitHub Release and served from
https://etiquekit.com/releases/; every set is covered by a signed
`SHA256SUMS` (see SECURITY.md).

## 1.0.9 — 2026-07-06

- Completion gate integrity: `return check` now verifies the receipt the
  task envelope names — a posted packet with the named receipt absent is
  `missing_return`, with the path stated. The deletion test is encoded in
  the contract suite.
- `doctor` warns on a missing git repository (with the exact fix command)
  and on git below the documented 2.40 minimum.

## 1.0.8 — 2026-07-06 (superseded)

- Deviation-survivable CLI: one-line errors (no stack/bundle dumps),
  unenrolled-seat errors list enrolled seats, bun preflight shims with an
  install hint, `--help` exits 0, `post` listed in main help.
- Superseded same-day by 1.0.9, which fixes a completion-gate integrity
  issue found by the pre-publish evaluation; prefer >=1.0.9.

## 1.0.7 — 2026-07-06

- First-run experience: bare invocation prints a compact entry card;
  generated onboarding references only real commands; internal
  authoring docs removed from the package.

## 1.0.6 — 2026-07-06

- Newcomer-pilot documentation fixes: the README quickstart is now runnable
  verbatim (real profile seat names), README and QuickStart share one
  canonical order, the completion gate (receipt → post → return check) is
  documented, and the agent guide addresses installed-package consumers.
- npm package metadata now links this repository (`repository`/`bugs`).

## 1.0.5 — 2026-07-06

- Vocabulary sweep across shipped docs and CLI help text: `journal`,
  `planner`, and `working loop` replace earlier informal terms. Wire schema
  unchanged (`spine_eligible` field name preserved).
- First release built and gated end-to-end by CI, with cross-platform
  reproducible bundles (linux CI bytes match the operator-signed bytes).

## 1.0.4 — 2026-07-05

- Working-discipline guidance ships out of the box: `docs/SEAT_DISCIPLINE.md`
  reorganized by moment of need; `bootstrap local` now renders
  `docs/work/runbooks/WORKING_DISCIPLINE.md` into every project.
- Fix: the git merge-driver install wrote a source-relative path that broke
  in compiled installs; it now resolves the running entrypoint.

## 1.0.3 — 2026-07-06

- QuickStart modernized to the global-install reality (npm / native
  installer / air-gapped tarball). CDN-only; superseded on npm by 1.0.4.

## 1.0.2 — 2026-07-06

- Public README rewrite. CDN-only; superseded on npm by 1.0.4.

## 1.0.1 — 2026-07-05

- First compiled public release: minified single-file bundles, no TypeScript
  source in the package. Dual-artifact signing (npm + CDN names, one signed
  manifest). Published to npm as `@etiquekit/etq`.
