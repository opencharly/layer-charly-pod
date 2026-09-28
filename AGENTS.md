# AGENTS.md — layer-charly-pod

Standalone candy repo for the `charly-pod` concept candy — it ships no install
content and owns the `pod` family's `pod` `skill:` entity (the `kind: pod` /
deploy schema reference). The entity lives in `charly.yml` at the repo root;
`candy/plugin-marketplace` regenerates the standalone opencharly/marketplace
corpus from it.

Canonical files:

- `charly.yml` — the `charly-pod:` concept candy entity plus one `skill:`
  entity: `pod-skill` (`name: pod`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-pod:pod` — the owning skill for the `kind: pod` / deploy schema (entry
  shape, tree-position nesting, the substrate kinds, sidecars). Load before
  editing the `pod-skill:` entity.
- `/charly-core:deploy` — the verb-level deploy surface (`charly fleet add`,
  `charly fleet del`, `charly update`). Load when a change touches deploy verbs
  rather than the schema.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, package sections, service declarations).
  Load before editing any entity field or plan step.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.
- The candy is documentation-only: its `plan:` is a `true` no-op plus a `true`
  `check:` that the skill entity is present and generated into the marketplace.
  There is no live bed.

## Modify this repo

- The `skill:` entity is the projected usage source. Edit it here, never the
  generated `SKILL.md` in the marketplace corpus; a corpus regeneration
  (`charly marketplace generate`) projects it.
- When the `kind: pod` / deploy schema changes, update the `pod-skill:` entity
  in the same change so the corpus does not drift.
- Keep the concept candy's `plan:` no-op; it exists only to carry the entity.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
