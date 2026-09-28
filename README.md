# charly-pod

The `charly-pod` family — the owning skill for the `kind: pod` / deploy schema.

The `charly-pod` candy is a **concept candy**: it ships no install content and
owns the `pod` family's `skill:` entity whose name has no namesake candy — the
`pod` skill. It is a thin schema pointer documenting the `kind: pod` and deploy
entity shapes: the `charly.yml` entry, tree-position nesting (no authored
`nested:` / `peer:` fields — membership is read from the tree), the substrate
kind at the deploy edge (`pod:` / `vm:` / `kubernetes:` / `local:` / `android:`
/ `group:`), and sidecars.

The verb-level operations (`charly fleet add`, `charly fleet del`,
`charly update`) are owned by `/charly-core:deploy`.
`candy/plugin-marketplace` regenerates the standalone
[opencharly/marketplace](https://github.com/opencharly/marketplace) corpus from
this entity, so the skill is authored here and projected there.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `charly-pod` (concept candy) |
| Install content | none — a `true` no-op `plan:` |
| Owns | 1 `skill:` entity: `pod` |
| Projected to | `marketplace/pod/skills/` |
| Service / port | none |

## How to use it

This repo is consumed as a **skill source**, not as an image layer. Edit the
`skill:` entity in `charly.yml`; the marketplace regeneration projects it into
the `/charly-pod:pod` page. To reference the repo directly, compose it in a box.
A box is a `candy:` node carrying the box's `base:` image and a nested `candy:`
list of layer refs (the nested `candy:` is the composition list; the outer
`candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    base: fedora          # the box's base image
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-charly-pod:v2026.243.2152'
```

A `pod` entity declares the co-scheduled containers and the volumes / network /
sidecars they share; the deploy node binds it to a substrate. The runtime verbs
live in `/charly-core:deploy`, not in this repo.

## Layout

- `charly.yml` — the `charly-pod:` concept candy entity plus the `pod-skill:`
  entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-pod:pod`
- Verb-level skill: `/charly-core:deploy`
- Sibling kind skills: `/charly-image:image`, `/charly-vm:vm`, `/charly-kubernetes:kubernetes`, `/charly-local:local-spec`
- Authoring reference: `/charly-image:layer`
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
