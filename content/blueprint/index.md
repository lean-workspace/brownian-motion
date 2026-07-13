---
title: "Brownian Motion blueprint"
description: "Companion blueprint for RemyDegenne/brownian-motion — reference chapters over the upstream Lean library, statuses computed from the kernel."
type: "blueprint-index"
tags:
  - "blueprint"
---

Companion blueprint for
[RemyDegenne/brownian-motion](https://github.com/RemyDegenne/brownian-motion),
the Lean 4 formalization of standard Brownian motion (Gaussian projective
families, the Kolmogorov extension theorem, and a Kolmogorov-Chentsov
continuity theorem), now extended toward stochastic integration.

The mathematics is the work of the upstream project — _Formalization of a
Brownian motion and of stochastic integrals in Lean_ by Rémy Degenne and
Peter Pfaffelhuber. The Brownian-motion part: blueprint by Rémy Degenne and
Peter Pfaffelhuber; formalization by Rémy Degenne, Markus Himmel, David
Ledvinka, Etienne Marion, and Peter Pfaffelhuber, with additional
contributions from Jonas Bayer, Lorenzo Loccioli, Pietro Monticone, Alessio
Rondelli, and Jérémy Scanvic. The stochastic-integral part: blueprint by
Rémy Degenne, Lorenzo Luccioli, Etienne Marion, Alessio Rondelli, and Kexing
Ying. The prose here is converted from the upstream LaTeX sources
(Apache-2.0).

The Lean code lives upstream and is pinned as a Lake dependency; chapters here
are reference chapters whose items point at upstream declarations with
`lean="..."`. Statuses, dependency edges, and source snippets are recomputed
from the compiled environment on every sync — nothing here is hand-maintained:

```bash
lake exe cache get            # prebuilt mathlib (transitive dependency)
lake build +BrownianMotion    # compile the upstream library
npm run blueprint:sync        # extract kernel truth + regenerate the canvas
```

The original leanblueprint site remains at
[remydegenne.github.io/brownian-motion/blueprint](https://remydegenne.github.io/brownian-motion/blueprint/).
All 15 chapters are migrated as native chapters (620 items), spanning two
parts: the construction of Brownian motion, and the stochastic integral in
progress. Note that items the upstream blueprint marks `\mathlibok` (theory
already upstreamed to mathlib) refer to declarations outside this library's
modules, which the extractor does not currently walk — they render without a
kernel status until the extractor learns to resolve named declarations from
dependencies.
