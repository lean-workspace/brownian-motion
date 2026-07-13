# Brownian Motion — Lean Workspace

Interactive blueprint companion for
[RemyDegenne/brownian-motion](https://github.com/RemyDegenne/brownian-motion),
the Lean 4 formalization of standard Brownian motion, now extended toward
stochastic integration. All 15 chapters of the upstream blueprint render here
as native chapters whose statuses, dependency edges, and source snippets are
recomputed from the compiled library — nothing is hand-maintained.

```bash
lake exe cache get             # prebuilt mathlib (transitive dependency)
lake build +BrownianMotion     # compile the pinned upstream library
npm install && npm run dev     # site at http://localhost:8080
npm run blueprint:sync         # refresh kernel statuses after Lean changes
```

## Attribution

The mathematics here is the work of the
[brownian-motion](https://github.com/RemyDegenne/brownian-motion) project:
**"Formalization of a Brownian motion and of stochastic integrals in Lean"
by Rémy Degenne and Peter Pfaffelhuber**. Per-part credits, as recorded in
the upstream blueprint:

- **Brownian motion** — blueprint by Rémy Degenne and Peter Pfaffelhuber;
  formalization by Rémy Degenne, Markus Himmel, David Ledvinka, Etienne
  Marion, and Peter Pfaffelhuber, with additional contributions from Jonas
  Bayer, Lorenzo Loccioli, Pietro Monticone, Alessio Rondelli, and Jérémy
  Scanvic
- **Stochastic integral** — blueprint by Rémy Degenne, Lorenzo Luccioli,
  Etienne Marion, Alessio Rondelli, and Kexing Ying (formalization open —
  anyone is welcome to contribute)
- **Original blueprint site** —
  [remydegenne.github.io/brownian-motion/blueprint](https://remydegenne.github.io/brownian-motion/blueprint/)

The blueprint prose is converted from the upstream LaTeX sources, licensed
[Apache-2.0](UPSTREAM-LICENSE.txt); the Lean library itself is consumed as a
pinned Lake dependency. `vendor/upstream/` carries a copy of the pinned
revision's `.lean` sources so deployed site builds can render declaration
snippets without a Lake checkout — refresh it when bumping the pin. The
mathematical references cited by the blueprint live in `bibliography.bib`
(the upstream blueprint's `bib.bib`) and render as linked citations. The
workspace machinery comes from the Lean Workspace template
([PolyForm Shield](LICENSE.txt), third-party notices in
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)).
