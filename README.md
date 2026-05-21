# Stencil — Simulation Organism Plugin

The community-owned Claude plugin behind [stencil.pub](https://stencil.pub).
Skills, atoms, and reports contributed by Stencil essayists, accumulated into one
plugin focused on simulating the physical world.

## Install

```bash
claude plugin install stencil-pub/stencil
```

## What's in here

- `skills/` — markdown-with-frontmatter skill files. Each is rendered on
  [stencil.pub/plugin/<slug>/](https://stencil.pub/plugin/) and is also loaded by
  Claude Code when the plugin is installed.
- `skills/_schema.json` — the frontmatter schema. The website validates against the
  same schema at build time; CI here validates against it on every PR.

## How to propose a skill

Click "Propose a skill" on [stencil.pub/plugin/](https://stencil.pub/plugin/),
or open a new file at `skills/<your-slug>.md` directly in this repo. The CI checks
your frontmatter against the schema; once approved, the website rebuilds and your
skill appears in the registry.

Anyone can propose. Members of the
[stencil-pub](https://github.com/stencil-pub) GitHub org can commit directly to `main`.

## Where the discussion happens

- Architecture and process: [Stencil journal](https://stencil.pub/journal/)
- Skill ideation and review: [GitHub Discussions](https://github.com/stencil-pub/stencil/discussions)
- Issues with specific skills: GitHub Issues on this repo

## License

Plugin code: **MIT**. Skill markdown: **CC-BY-4.0**. See the website
[About page](https://stencil.pub/about/) for the full licensing stance.

## The vision

See the founding essay:
[Toward a Simulation Organism](https://stencil.pub/journal/toward-a-simulation-organism/)
(DOI [10.5281/zenodo.20331251](https://doi.org/10.5281/zenodo.20331251)).
