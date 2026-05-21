---
id: missing-physics-detector
name: Missing Physics Detector
kind: skill
physics_domain: general
status: draft
contributors:
  - pourion
source_article: toward-a-simulation-organism
summary: >
  Identifies systematic residuals between simulation and ground truth that suggest
  missing physical terms in the solver's governing equations.
plugin_repo_path: skills/missing-physics-detector.md
tags:
  - diagnosis
  - residuals
  - missing-physics
created: 2026-05-21
---

# Missing Physics Detector

Looks at residuals between simulation predictions and ground truth (analytic
solutions, benchmark calculations, or physical measurements) and flags systematic
patterns that suggest one or more physics terms are missing from the governing
equations — as distinct from numerical error, under-resolution, or boundary-condition
mismatch.

> **Status: draft.** Derived from the founding essay
> [*Toward a Simulation Organism*](https://stencil.pub/journal/toward-a-simulation-organism/).
> Please refine: concrete diagnostic procedures, classification of failure modes,
> and worked examples are all welcome contributions.

## When to use

- A model has been calibrated and converged numerically, but a stubborn 10–20% gap
  remains between simulation and experiment.
- The gap shows a *pattern* — concentrated near specific features, scales, or
  operating conditions — rather than uniform noise.
- The team has run out of obvious numerical or geometric fixes.

## How it works

1. **Decompose the residual.** Split the gap into components by region of interest,
   frequency band, temporal regime, and material/geometry feature.
2. **Look for systematic structure.** Random residuals are noise; systematic
   residuals correlate with a physical scale or feature class.
3. **Propose candidate physics terms.** For each pattern, hypothesize which
   neglected term in the governing equations would produce that residual signature.
   Examples: surface tension near liquid–vapor interfaces; second-order gradient
   terms near deep sub-wavelength features; non-local closure terms in turbulent
   flows.
4. **Test the candidate.** Add the proposed term to the solver, hold all other
   choices fixed, rerun. Compare the residual everywhere — does the gap close
   locally without re-opening gaps elsewhere?
5. **Persist the lesson.** If the candidate term improves agreement broadly, promote
   it to an *iron law* and write it to [[iron-laws-corpus]] with the conditions
   under which it applies.

## Examples

*(Contributors welcome to add worked examples here — electromagnetic, fluid,
structural, thermal.)*

## References

- [Toward a Simulation Organism](https://stencil.pub/journal/toward-a-simulation-organism/)
  (Mistani 2026), DOI [10.5281/zenodo.20331251](https://doi.org/10.5281/zenodo.20331251)
