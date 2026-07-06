# Changelog

All published versions of `@etiquekit/etq`. Artifacts for each version are
attached to the matching GitHub Release and served from
https://etiquekit.com/releases/; every set is covered by a signed
`SHA256SUMS` (see SECURITY.md).

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
