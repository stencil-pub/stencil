---
noteId: "e00088f05e1d11f18b2e97153df99a5c"
tags: []

---

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is the **Stencil Claude Code plugin** — a content repository, not a software project. There is no build step and no application code. The deliverable is a set of physics-simulation *skills* written as markdown files with YAML frontmatter under `skills/`. The same files serve two consumers:

1. **Claude Code**, which loads them as plugin skills when the plugin is installed (`plugin.json` points `skills` at `skills/`).
2. **The stencil.pub website** (separate repo `stencil-pub/stencil.pub`), which renders each skill at `stencil.pub/plugin/<id>/` and validates them against an equivalent zod schema at build time.

Because both consumers read the same files, frontmatter is the contract. Keep it agent-neutral (the project plans to support Codex and other agents by adding manifests, not by rewriting skills).

## Validating skills (the only "build/test")

CI (`.github/workflows/validate.yml`) validates every `skills/*.md` (excluding `_`-prefixed files) against `skills/_schema.json` on each PR. To run the same check locally:

```bash
npm install --no-save ajv ajv-formats gray-matter
# then run the inline validator from validate.yml (it writes /tmp/validate.mjs)
```

The validator enforces three things beyond JSON Schema, so watch for these when adding or editing a skill:

- `id` **must equal the filename** without `.md` (e.g. `skills/foo.md` → `id: foo`).
- `plugin_repo_path` **must be** exactly `skills/<id>.md`.
- Frontmatter must match `_schema.json`, which has `additionalProperties: false` — any unrecognized key fails the build.

Required frontmatter keys: `id`, `name`, `kind` (`skill`|`atom`|`report`), `physics_domain` (kebab-case), `status` (`draft`|`community-validated`|`iron-law`), `summary` (≥10 chars), `plugin_repo_path`, `created` (date). Optional: `contributors` (GitHub usernames, no `@`), `source_article`, `tags`, `updated`.

`skills/_schema.json` mirrors the website's zod schema (linked in the schema's `description`). If you change one, the other must change too or the website build will diverge from CI.

## Publishing flow

Merging skill changes to `main` triggers `.github/workflows/notify-website.yml`, which fires a `repository-dispatch` (`skills-updated`) at `stencil-pub/stencil.pub` to rebuild the public site. So a merge to `main` is also a publish — there is no separate deploy.

## Authoring conventions

- Cross-reference other skills with `[[skill-id]]` wiki-links (e.g. `[[iron-laws-corpus]]`). These resolve to other files' `id` and are rendered as links on the website.
- A skill's `status` frontmatter and any in-body `> **Status:** ...` callout should agree.
- `iron-laws-corpus.md` is an append-only knowledge base: add new laws as new `###` sections rather than editing existing ones, and include the evidence/citation. Laws are promoted `provisional → validated → iron` by maintainers.

## Contribution model

Anyone can open a PR adding `skills/<slug>.md`; CI checks the frontmatter. Members of the `stencil-pub` GitHub org can commit directly to `main`. Pouria Mistani (`pourion`) is the founding maintainer.
