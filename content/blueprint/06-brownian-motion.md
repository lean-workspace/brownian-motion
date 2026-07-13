---
title: 'Brownian motion'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Stochastic process with continuous paths**

## Definition: pre-Brownian process {#def:preBrownian lean="ProbabilityTheory.preBrownian" uses="def:gaussianLimit"}

Let $\Omega = \mathbb{R}^{\mathbb{R}_+}$ and consider the probability space $(\Omega, P_B)$ (where $P_B$ is the measure defined in [gaussianLimit](#def:gaussianLimit)).
The identity on that space is a function $\Omega \to \mathbb{R}_+ \to \mathbb{R}$.
We reorder the arguments to define a stochastic process $X : \mathbb{R}_+ \to \Omega \to \mathbb{R}$, which we call the pre-Brownian process.

## Lemma: isGaussianProcess_preBrownian {#lem:isGaussianProcess_preBrownian lean="ProbabilityTheory.isGaussianProcess_preBrownian" uses="def:preBrownian, def:IsGaussianProcess"}

The pre-Brownian process $X$ of [pre-Brownian process](#def:preBrownian) is a Gaussian process.

### Proof {uses="lem:isGaussian_multivariateGaussian"}

For any $t_1, \ldots, t_n \in \mathbb{R}_+$, the distribution of $(X_{t_1}, \ldots, X_{t_n})$ is given by a finite-dimensional distribution of $P_B$, and therefore is Gaussian.

## Lemma: hasLaw_preBrownian_sub {#lem:hasLaw_preBrownian_sub lean="ProbabilityTheory.hasLaw_preBrownian_sub" uses="def:preBrownian"}

Let $X$ be the pre-Brownian process of [pre-Brownian process](#def:preBrownian).
Then, for all $s, t \in \mathbb{R}_+$, the random variable $X_t - X_s$ is a Gaussian random variable with mean $0$ and variance $|t - s|$.

### Proof {uses="lem:isGaussianProcess_preBrownian, lem:isGaussian_map"}

The map

$$
\begin{align*}
  L : \mathbb{R}^2 &\to \mathbb{R} \\
  (x_1, x_2) &\mapsto x_2 - x_1
\end{align*}
$$

is a continuous linear map, and $(X_s, X_t)$ is Gaussian by [isGaussianProcess_preBrownian](#lem:isGaussianProcess_preBrownian), therefore $X_t - X_s$ is Gaussian by [isGaussian_map](#lem:isGaussian_map). By definition of $P_B$, we have

$$
\mathbb{E}[X_t - X_s] = \mathbb{E}[X_t] - \mathbb{E}[X_s] = 0 - 0 = 0,
$$

and

$$
\mathrm{Var}(X_t - X_s) = \mathrm{Var}(X_t) - 2\mathrm{Cov}(X_t, X_s) + \mathrm{Var}(X_s) = t - 2(t \land s) + s = t \lor s - t \land s = |t - s|.
$$

Therefore $X_t - X_s$ is Gaussian with mean $0$ and variance $|t - s|$.

## Lemma: isKolmogorovProcess_preBrownian {#lem:isKolmogorovProcess_preBrownian lean="ProbabilityTheory.isKolmogorovProcess_preBrownian" uses="def:preBrownian"}

The pre-Brownian process $X$ of [pre-Brownian process](#def:preBrownian) satisfies the Kolmogorov condition for exponents $(2n,n)$ with constant $(2n - 1)!!$ for all $n \in \mathbb{N}$.
That is, for all $s, t \in \mathbb{R}_+$, we have

$$
\begin{align*}
  \mathbb{E} \left[ |X_t - X_s|^{2n} \right] \le (2n - 1)!! |t - s|^n
  \: .
\end{align*}
$$

### Proof {uses="lem:centralMoment_two_mul_gaussianReal, lem:hasLaw_preBrownian_sub"}

$X_t - X_s$ is a Gaussian random variable with mean $0$ and variance $|t - s|$ ([hasLaw_preBrownian_sub](#lem:hasLaw_preBrownian_sub)).
Thus, by [centralMoment_two_mul_gaussianReal](#lem:centralMoment_two_mul_gaussianReal), we have

$$
\begin{align*}
  \mathbb{E} \left[ |X_t - X_s|^{2n} \right]
  = (2n - 1)!! |t - s|^n
  \: .
\end{align*}
$$

## Definition: Brownian motion {#def:brownian lean="ProbabilityTheory.brownian" uses="thm:localized_holder_modification_sup, def:preBrownian, lem:isKolmogorovProcess_preBrownian, lem:hasBoundedCoveringNumberCover_nnreal"}

By [localized_holder_modification_sup](#thm:localized_holder_modification_sup), there exists a modification $B$ of the pre-Brownian process such that all the paths of $B$ are Hölder continuous of all orders $\gamma \in (0, 1/2)$.
We call $B$ the _Brownian motion_ on $\mathbb{R}_+$.

## Lemma: isGaussianProcess_brownian {#lem:isGaussianProcess_brownian lean="ProbabilityTheory.isGaussianProcess_brownian" uses="def:brownian, def:IsGaussianProcess"}

The Brownian motion is a Gaussian process.

### Proof {uses="lem:isGaussianProcess_of_modification, lem:isGaussianProcess_preBrownian"}

The pre-Brownian process is a Gaussian process by [isGaussianProcess_preBrownian](#lem:isGaussianProcess_preBrownian).
The Brownian motion is a modification of the pre-Brownian process by [Brownian motion](#def:brownian).
Thus, the Brownian motion is a Gaussian process as well by [isGaussianProcess_of_modification](#lem:isGaussianProcess_of_modification).

## Lemma: isHolderWith_brownian {#lem:isHolderWith_brownian lean="ProbabilityTheory.memHolder_brownian" uses="def:brownian"}

The paths of the Brownian motion are locally Hölder continuous of all orders $\gamma \in (0, 1/2)$.

### Proof {uses="lem:hasBoundedCoveringNumberCover_nnreal, lem:isKolmogorovProcess_preBrownian, thm:localized_holder_modification_sup"}

Consider the cover of $\mathbb{R}_+$ given by $T_n := [0, n + 1)$. By [hasBoundedCoveringNumberCover_nnreal](#lem:hasBoundedCoveringNumberCover_nnreal), this cover has bounded covering numbers with exponent $1$. Moreover, by [isKolmogorovProcess_preBrownian](#lem:isKolmogorovProcess_preBrownian), the pre-Brownian process satisfies the Kolmogorov condition with exponents $(2n + 4, n + 2)$ for all $n \in \mathbb{N}$.
In particular, for all $n \in \mathbb{N}$, $2n + 4 > 1$. Applying [localized_holder_modification_sup](#thm:localized_holder_modification_sup) we deduce that the modification used in [Brownian motion](#def:brownian) has locally Hölder continuous paths for all orders $\gamma \in (0, \sup_n (n + 1) / (2n + 4))$.
Clearly for all $n \in \mathbb{N}$ we have $(n + 1) / (2n + 4) \leqslant 2$, and this quantity tends to $2$ as $n$ goes to infinity. Therefore the Brownian motion has Hölder continuous paths of order $\gamma$ for all $\gamma \in (0, 1 / 2)$.

## Lemma: continuous_brownian {#lem:continuous_brownian lean="ProbabilityTheory.continuous_brownian" uses="def:brownian"}

The paths of the Brownian motion are continuous.

### Proof {uses="lem:isHolderWith_brownian"}

The paths are $1/4$-Hölder continuous by [isHolderWith_brownian](#lem:isHolderWith_brownian) because $0 < 1/4 < 1/2$, therefore they are continuous.

## Lemma: hasLaw_brownian_eval {#lem:hasLaw_brownian_eval lean="ProbabilityTheory.hasLaw_brownian_eval" uses="def:brownian"}

For $t \in \mathbb{R}_+$, the law of $B_t$ (the Brownian motion at time $t$) is the real Gaussian measure $\mathcal{N}(0,t)$.

### Proof {uses="def:gaussianLimit"}

The Brownian motion $B$ is a modification of the pre-Brownian process, and therefore has same finite dimensional distributions. By [gaussianLimit](#def:gaussianLimit), $B_t$ has law $\mathcal{N}(0,t)$.

## Lemma: hasLaw_brownian_sub {#lem:hasLaw_brownian_sub lean="ProbabilityTheory.hasLaw_brownian_sub" uses="def:brownian"}

For $s, t \in \mathbb{R}_+$, the law of $B_t - B_s$ is the real Gaussian measure $\mathcal{N}(0,\vert t - s \vert)$.

### Proof {uses="lem:hasLaw_preBrownian_sub"}

The Brownian motion $B$ is a modification of the pre-Brownian process, and therefore has same finite dimensional distributions. By [hasLaw_preBrownian_sub](#lem:hasLaw_preBrownian_sub), $B_t - B_s$ has law $\mathcal{N}(0,\vert t - s \vert)$.

## Definition: HasIndepIncrements {#def:HasIndepIncrements lean="ProbabilityTheory.HasIndepIncrements"}

We say that a stochastic process $X : T \to \Omega \to E$ has independent increments if for all $t_1, \ldots, t_n \in T$ with $t_1 \le t_2 \le \cdots \le t_n$, the random variables $X_{t_2} - X_{t_1}, X_{t_3} - X_{t_2}, \ldots, X_{t_n} - X_{t_{n-1}}$ are independent.

## Lemma: hasIndepIncrements_brownian {#lem:hasIndepIncrements_brownian lean="ProbabilityTheory.hasIndepIncrements_brownian" uses="def:brownian, def:HasIndepIncrements"}

The Brownian motion has independent increments.

### Proof

Let $t_1 \le t_2 \le \ldots \le t_n$ be $n$ times in $\mathbb{R}_+$.
Then $(B_{t_2} - B_{t_1}, B_{t_3} - B_{t_2}, \ldots, B_{t_n} - B_{t_{n-1}})$ is a linear transformation of $(B_{t_1}, \ldots, B_{t_n})$, hence it is Gaussian.
We can compute its mean (which is $0$) and its covariance matrix.
The covariance matrix is diagonal, which means the the random variables are uncorrelated.
Because they are jointly Gaussian, this implies that they are independent.

**Wiener measure on the continuous functions**

We want to turn the Brownian motion into a measure on the continuous functions $C(\mathbb{R}_+, \mathbb{R})$ with the Borel sigma-algebra generated by the compact-open topology.

## Definition: Auxiliary Wiener measure {#def:wienerMeasureAux lean="ProbabilityTheory.wienerMeasureAux" uses="def:brownian, def:gaussianLimit, lem:continuous_brownian"}

The pushforward of the measure $P_B$ of [gaussianLimit](#def:gaussianLimit) by the Brownian motion $B$ is a measure on the continuous functions on $\mathbb{R}^{\mathbb{R}_+}$, with the sigma-algebra induced by the product sigma-algebra on $\mathbb{R}^{\mathbb{R}_+}$.

**Lean remark**: the auxiliary Wiener measure is a measure on the subtype `\{f  // Continuous f\`}. This is not the same type as $C(\mathbb{R}_+, \mathbb{R})$.

## Theorem: ContinuousMap.borel_eq_iSup_comap_eval {#thm:ContinuousMap.borel_eq_iSup_comap_eval lean="ProbabilityTheory.ContinuousMap.borel_eq_iSup_comap_eval"}

The Borel sigma-algebra on $C(\mathbb{R}_+, \mathbb{R})$ coming from the compact-open topology is equal to the smallest sigma-algebra for which the evaluation maps $f \mapsto f(t)$ are measurable for every $t \in \mathbb{R}_+$.

### Proof

We prove that this holds for $C(X, Y)$ as long as $X$ and $Y$ are second-countable topological spaces endowed with their Borel sigma-algebra, $X$ is locally compact (i.e.\ each point of $X$ has a basis of compact neighbourhoods), and $Y$ is regular (i.e.\ for any $C \subseteq Y$ closed and $y \notin C$, there exist disjoint open subsets $U, V \subseteq Y$ such that $C \subseteq U$ and $y \in V$). The proof is taken from \href{https://math.stackexchange.com/questions/4789531/when-does-the-borel-sigma-algebra-of-compact-convergence-coincide-with-the-pr}{this stackexchange question}.

We denote by $\mathcal{T}_1$ and $\mathcal{T}_2$ the two sigma-algebras.

First of all, the evaluation maps are continuous for the compact-open topology, and therefore measurable for $\mathcal{T}_1$. We deduce that $\mathcal{T}_2 \subseteq \mathcal{T}_1$.

Let us turn to the converse direction. For any $A \subseteq X$ and $B \subseteq Y$, denote

$$
M(A, B) := \{f \in C(X, Y), f(A) \subset B\}.
$$

The compact-open topology is generated by the sets of the form $M(K, U)$, for $K$ compact and $U$ open. Because $X$ and $Y$ are second-countable and $X$ is locally compact, $C(X, Y)$ is second-countable. Therefore it is enough to show that for any $K$ compact and $U$ open, $M(K, U) \in \mathcal{T}_2$. We now fix $K$ and $U$.

Consider $(V_n)_{n \in \mathbb{N}}$ a countable family of subsets of $Y$ which generates the topology (it exists by second-countability assumption). Clearly we have that

$$
\bigcup_{\overline{V_n} \subseteq U} V_n \subseteq U.
$$

Conversely, consider $y \in U$. Because $Y$ is regular, the set of $\overline{V_n}$ such that $y \in V_n$ is a basis of neighbourhoods of $y$. Indeed, consider $A$ an open neighbourhood of $y$. Then $A^c$ is a closed set which does not contain $y$. Therefore there exist disjoint open sets $B$ and $C$ such that $y \in B$ and $A^c \subseteq C$. There exists $n \in \mathbb{N}$ such that $x \in V_n \subseteq B$. Therefore $V_n \subseteq C^c$, so $\overline{V_n} \subseteq C^c \subseteq A$, and we are done. This proves that we have in fact

$$
U = \bigcup_{\overline{V_n} \subseteq U} V_n = \bigcup_{\overline{V_n} \subseteq U} \overline{V_n}.
$$

Consider now $f \in M(K, U)$. We then have

$$
f(K) \subseteq \bigcup_{\overline{V_n} \subseteq U} V_n.
$$

Because $K$ is compact and $f$ is continuous, $f(K)$ is compact. But each $V_n$ is open, so there exists a finite set $\hat{f}$ of natural integers such that for any $n \in \hat{f}$, $\overline{V_n} \subseteq U$, and

$$
f(K) \subseteq \bigcup_{n \in \hat{f}} V_n \subseteq \bigcup_{n \in \hat{f}} \overline{V_n}.
$$

Conversely, if there exists a finite set $\hat{f}$ such that for any $n \in \hat{f}$, $\overline{V_n} \subseteq U$, and

$$
f(K) \subseteq \bigcup_{n \in \hat{f}} \overline{V_n},
$$

then $f(K) \subseteq U$. We can therefore write that

$$
M(K, U) = \bigcup_{\substack{I \subseteq \mathbb{N} \\ I \text{ finite} \\ \forall n \in I, \overline{V_n} \subseteq U}} M\left(K, \bigcup_{i \in I} \overline{V_i}\right).
$$

This is a countable union, so we just have to prove that each term is measurable.

We now fix a finite set $I$ as in the union above. Because $X$ is second countable, there exists $Q$ a countable dense subset of $K$. For any $f$ continuous, because $Q$ is dense and $\bigcup_{i \in I} \overline{V_i}$ is closed, we have

$$
f(K) \subset \bigcup_{i \in I} \overline{V_i} \Longleftrightarrow f(Q) \subset \bigcup_{i \in I} \overline{V_i}.
$$

In other words, $M\left(K, \bigcup_{i \in I} \overline{V_i}\right) = M\left(Q, \bigcup_{i \in I} \overline{V_i}\right)$. We can write

$$
M\left(Q, \bigcup_{i \in I} \overline{V_i}\right) = \bigcap_{q \in Q} (f \mapsto f(q))^{-1} \bigcup_{i \in I} \overline{V_i},
$$

and it is enough to show that each term in the intersection is measurable. Because $\bigcup_{i \in I} \overline{V_i}$ is closed, it is measurable. It therefore remains to prove that $f \mapsto f(q)$ is measurable for all $q \in Q$, but this is obvious from the definition of $\mathcal{T}_2$. This concludes the proof.

## Definition: MeasurableEquiv.continuousMap {#def:MeasurableEquiv.continuousMap lean="ProbabilityTheory.MeasurableEquiv.continuousMap" uses="thm:ContinuousMap.borel_eq_iSup_comap_eval"}

The identity is a measurable equivalence between the continuous functions of $\mathbb{R}^{\mathbb{R}_+}$ with the subset sigma-algebra obtained from the product sigma-algebra, and $C(\mathbb{R}_+, \mathbb{R})$ with the Borel sigma-algebra coming from the compact-open topology.

Mathematically this says nothing more than the equality of sigma-algebras of [ContinuousMap.borel_eq_iSup_comap_eval](#thm:ContinuousMap.borel_eq_iSup_comap_eval) but in Lean we have two different types so we need an equivalence.

## Definition: Wiener measure {#def:wienerMeasure lean="ProbabilityTheory.wienerMeasure" uses="def:MeasurableEquiv.continuousMap, def:wienerMeasureAux"}

The Wiener measure on $C(\mathbb{R}_+, \mathbb{R})$ with the Borel sigma-algebra is the map of the auxiliary Wiener measure by the measurable equivalence of definition [MeasurableEquiv.continuousMap](#def:MeasurableEquiv.continuousMap).

TODO: add the main properties of the Brownian motion and the Wiener measure.
We need to be able to tell that we have built the correct objects.

\putbib

**Overview**

We describe the construction of a stochastic integral.

**Status** The formalization is ongoing.

**Blueprint authors** Rémy Degenne, Lorenzo Luccioli, Etienne Marion, Alessio Rondelli, Kexing Ying. Anyone is welcome to contribute!

**Formalization authors** Anyone is welcome to contribute!

