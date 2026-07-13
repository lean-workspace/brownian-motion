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
This workspace starts with a scaffold chapter on the construction of Brownian
motion; the remaining chapters are being migrated. Note that items the
upstream blueprint marks `\mathlibok` (theory already upstreamed to mathlib,
e.g. the Gaussian-measure chapter) refer to declarations outside this
library's modules, which the extractor does not currently walk.
