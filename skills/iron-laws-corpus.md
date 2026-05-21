---
id: iron-laws-corpus
name: Iron Laws Corpus
kind: skill
physics_domain: general
status: draft
contributors:
  - pourion
source_article: toward-a-simulation-organism
summary: >
  Append-only corpus of validated heuristics — iron laws — for solver design.
  Each law names a condition, a recommended atom or technique, and the evidence
  base. Future agent sessions consult this corpus instead of re-deriving choices.
plugin_repo_path: skills/iron-laws-corpus.md
tags:
  - knowledge-base
  - heuristics
  - solver-design
created: 2026-05-21
---

# Iron Laws Corpus

Durable, append-only collection of validated solver-design heuristics. Each entry
names a condition (when this rule applies), a recommendation (which atom or
technique to use), and the evidence base (how we know).

> **Status: draft.** Bootstrapped with two illustrative laws from the founding essay.
> Future contributors append validated heuristics from their own experiments. New
> entries should cite the experimental or analytical evidence that supports them.

## Why iron laws

An iron law is a heuristic that has survived enough experiments across enough
problem classes that the agent stops re-deriving it. Skills compound: when laws
accumulate, the agent's effective starting point on a new problem improves
monotonically.

## Format

Every law has the same shape:

```yaml
- id: <slug>
  condition: <when does this apply?>
  recommendation: <which atom / technique?>
  evidence: <citations or experiment IDs>
  added: <YYYY-MM-DD>
  status: provisional | validated | iron
```

## Current laws

### `prefer-implicit-time-stepping-for-stiff-systems`

- **Condition:** Stiff time integration (largest eigenvalue ≫ smallest, e.g.
  chemical kinetics, advection-diffusion with disparate scales).
- **Recommendation:** Implicit (BDF, Radau) time integrator over explicit RK.
- **Evidence:** Classical numerical-analysis result; verifiable on Robertson and
  Van der Pol test problems with order-of-magnitude wall-clock difference.
- **Added:** 2026-05-21 · **Status:** provisional

### `decompose-residuals-spatially-before-frequency-analysis`

- **Condition:** Diagnosing a stubborn simulation-experiment gap.
- **Recommendation:** First localize the residual by region of interest; then, if
  the region is identified, decompose by frequency band within that region.
- **Evidence:** Practitioner heuristic; derives from [[missing-physics-detector]].
- **Added:** 2026-05-21 · **Status:** provisional

## How to add a law

Open a PR adding a new section above. Include the citation or experiment ID that
supports the rule. The maintainers review against the agent's accumulated corpus
before promoting a law from `provisional` → `validated` → `iron`.

## References

- [Toward a Simulation Organism](https://stencil.pub/journal/toward-a-simulation-organism/)
  (Mistani 2026)
