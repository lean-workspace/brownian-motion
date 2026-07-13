---
title: "Brownian motion"
type: "blueprint-chapter"
tags:
  - "blueprint"
---

Scaffold chapter, migrated from the "Brownian motion" chapter of the
[upstream blueprint](https://remydegenne.github.io/brownian-motion/blueprint/):
the construction of the process itself, from the pre-Brownian process on the
Gaussian projective limit to the Hölder-continuous modification. Dependency
edges into material not yet migrated (Gaussian projective families and the
Kolmogorov-Chentsov theorem) are omitted until those chapters exist here.

## Definition: pre-Brownian process {#def:preBrownian lean="ProbabilityTheory.preBrownian"}

Let $\Omega = \mathbb{R}^{\mathbb{R}_+}$ and consider the probability space
$(\Omega, P_B)$, where $P_B$ is the projective limit of the Gaussian
projective family. The identity on that space is a function
$\Omega \to \mathbb{R}_+ \to \mathbb{R}$; reordering the arguments defines a
stochastic process $X : \mathbb{R}_+ \to \Omega \to \mathbb{R}$, which we
call the *pre-Brownian process*.

## Lemma: The pre-Brownian process is Gaussian {#lem:isGaussianProcess_preBrownian lean="ProbabilityTheory.isGaussianProcess_preBrownian" uses="def:preBrownian"}

The pre-Brownian process $X$ is a Gaussian process.

### Proof

For any $t_1, \ldots, t_n \in \mathbb{R}_+$, the distribution of
$(X_{t_1}, \ldots, X_{t_n})$ is a finite-dimensional distribution of $P_B$,
and therefore is Gaussian.

## Definition: Brownian motion {#def:brownian lean="ProbabilityTheory.brownian" uses="def:preBrownian"}

By the localized Hölder-modification theorem (Kolmogorov-Chentsov), there
exists a modification $B$ of the pre-Brownian process such that all the paths
of $B$ are Hölder continuous of all orders $\gamma \in (0, 1/2)$. We call $B$
the *Brownian motion* on $\mathbb{R}_+$.

## Lemma: Hölder continuity of the paths {#lem:isHolderWith_brownian lean="ProbabilityTheory.memHolder_brownian" uses="def:brownian"}

The paths of the Brownian motion are locally Hölder continuous of all orders
$\gamma \in (0, 1/2)$.

### Proof

Cover $\mathbb{R}_+$ by $T_n := [0, n + 1)$, which has bounded covering
numbers with exponent $1$. The pre-Brownian process satisfies the Kolmogorov
condition with exponents $(2n + 4, n + 2)$ for all $n$, so the modification
used to define the Brownian motion has locally Hölder continuous paths for
all orders $\gamma \in (0, \sup_n (n + 1)/(2n + 4)) = (0, 1/2)$.

## Lemma: Continuity of the paths {#lem:continuous_brownian lean="ProbabilityTheory.continuous_brownian" uses="def:brownian"}

The paths of the Brownian motion are continuous.

### Proof

The paths are $1/4$-Hölder continuous, therefore continuous.
