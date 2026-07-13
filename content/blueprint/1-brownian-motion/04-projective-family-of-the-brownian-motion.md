---
title: 'Projective family of the Brownian motion'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Kolmogorov extension theorem**

This theorem has been formalized by Rémy Degenne and Peter Pfaffelhuber in the repository \href{https://github.com/RemyDegenne/kolmogorov_extension4}{kolmogorov\_extension4}.

## Definition: Projective family {#def:IsProjectiveMeasureFamily lean="MeasureTheory.IsProjectiveMeasureFamily"}

A family of measures $P$ indexed by finite sets of $T$ is projective if, for finite sets $J \subseteq I$, the projection from $E^I$ to $E^J$ maps $P_I$ to $P_J$.

## Definition: Projective limit {#def:IsProjectiveLimit lean="MeasureTheory.IsProjectiveLimit" uses="def:IsProjectiveMeasureFamily"}

A measure $\mu$ on $E^T$ is the projective limit of a projective family of measures $P$ indexed by finite sets of $T$ if, for every finite set $I \subseteq T$, the projection from $E^T$ to $E^I$ maps $\mu$ to $P_I$.

## Theorem: Kolmogorov extension theorem {#thm:kolmogorovExtension lean="MeasureTheory.projectiveLimit, MeasureTheory.IsProjectiveLimit.unique, MeasureTheory.isProjectiveLimit_projectiveLimit, MeasureTheory.isFiniteMeasure_projectiveLimit, MeasureTheory.isProbabilityMeasure_projectiveLimit" uses="def:IsProjectiveLimit, def:IsProjectiveMeasureFamily"}

Let $\mathcal{X}$ be a Polish space, equipped with the Borel $\sigma$-algebra, and let $T$ be an index set.
Let $P$ be a projective family of finite measures on $\mathcal{X}$.
Then the projective limit $\mu$ of $P$ exists, is unique, and is a finite measure on $\mathcal{X}^T$.
Moreover, if $P_I$ is a probability measure for every finite set $I \subseteq T$, then $\mu$ is a probability measure.

**Projective family of Gaussian measures**

We build a projective family of Gaussian measures indexed by $\mathbb{R}_+$.
In order to do so, we need to define specific Gaussian measures on finite index sets $\{t_1, \ldots, t_n\}$.
We want to build a multivariate Gaussian measure on $\mathbb{R}^n$ with mean $0$ and covariance matrix $C_{ij} = \min(t_i, t_j)$ for $1 \leq i,j \leq n$.

We prove that the matrix $C_{ij} = \min(t_i, t_j)$ is positive semidefinite, which means that there exists a Gaussian distribution with mean 0 and covariance matrix $C$.

## Definition: Gram matrix {#def:gramMatrix lean="Matrix.gram"}

Let $v_1, \ldots, v_n$ be vectors in an inner product space $E$.
The Gram matrix of $v_1, \ldots, v_n$ is the matrix in $\mathbb{R}^{n \times n}$ with entries $G_{ij} = \langle v_i, v_j \rangle$ for $1 \leq i,j \leq n$.

## Lemma: posSemidef_gramMatrix {#lem:posSemidef_gramMatrix lean="Matrix.posSemidef_gram" uses="def:gramMatrix"}

A gram matrix is positive semidefinite.

### Proof

Symmetry is obvious from the definition.
Let $x \in E$. Then

$$
\begin{align*}
  \langle x, G x \rangle
  &= \sum_{i,j} x_i x_j \langle v_i, v_j \rangle
  \\
  &= \langle \sum_i x_i v_i, \sum_j x_j v_j \rangle
  \\
  &= \left\Vert \sum_i x_i v_i \right\Vert^2
  \\
  &\ge 0
  \: .
\end{align*}
$$

## Lemma: C_eq_gramMatrix {#lem:C_eq_gramMatrix uses="def:gramMatrix"}

Let $I = \{t_1, \ldots, t_n\}$ be a finite subset of $\mathbb{R}_+$.
For $i \le n$, let $v_i = \mathbb{I}_{[0, t_i]}$ be the indicator function of the interval $[0, t_i]$, as an element of $L^2(\mathbb{R})$.
Then the Gram matrix of $v_1, \ldots, v_n$ is equal to the matrix $C_{ij} = \min(t_i, t_j)$ for $1 \leq i,j \leq n$.

### Proof

By definition of the inner product in $L^2(\mathbb{R})$,

$$
\begin{align*}
  \langle v_i, v_j \rangle
  &= \int_{\mathbb{R}} \mathbb{I}_{[0, t_i]}(x) \mathbb{I}_{[0, t_j]}(x) \: dx
  = \min(t_i, t_j)
  \: .
\end{align*}
$$

## Lemma: posSemidef_brownianCov {#lem:posSemidef_brownianCov lean="ProbabilityTheory.posSemidef_brownianCovMatrix"}

For $I = \{t_1, \ldots, t_n\}$ a finite subset of $\mathbb{R}_+$, let $C \in \mathbb{R}^{n \times n}$ be the matrix $C_{ij} = \min(t_i, t_j)$ for $1 \leq i,j \leq n$.
Then $C$ is positive semidefinite.

### Proof {uses="lem:C_eq_gramMatrix, lem:posSemidef_gramMatrix"}

$C$ is a Gram matrix by [C_eq_gramMatrix](#lem:C_eq_gramMatrix).
By [posSemidef_gramMatrix](#lem:posSemidef_gramMatrix), it is positive semidefinite.

\paragraph{Definition of the projective family and extension}

## Definition: Projective family of the Brownian motion {#def:gaussianProjectiveFamily lean="ProbabilityTheory.gaussianProjectiveFamily" uses="def:multivariateGaussian, lem:posSemidef_brownianCov"}

For $I = \{t_1, \ldots, t_n\}$ a finite subset of $\mathbb{R}_+$, let $P^B_I$ be the multivariate Gaussian measure on $\mathbb{R}^n$ with mean $0$ and covariance matrix $C_{ij} = \min(t_i, t_j)$ for $1 \leq i,j \leq n$.
We call the family of measures $P^B_I$ the _projective family of the Brownian motion_.

## Lemma: isProjectiveMeasureFamily_gaussianProjectiveFamily {#lem:isProjectiveMeasureFamily_gaussianProjectiveFamily lean="ProbabilityTheory.isProjectiveMeasureFamily_gaussianProjectiveFamily" uses="def:gaussianProjectiveFamily, def:IsProjectiveMeasureFamily"}

The projective family of the Brownian motion is a projective family of measures.

### Proof {uses="lem:isGaussian_multivariateGaussian, lem:covMatrix_map, lem:integral_id_multivariateGaussian, lem:covMatrix_multivariateGaussian, lem:IsGaussian.ext_iff"}

Let $J \subseteq I$ be finite subsets of $\mathbb{R}_+$.
We need to show that the restriction from $\mathbb{R}^I$ to $\mathbb{R}^J$ (denote it by $\pi_{IJ}$) maps $P^B_I$ to $P^B_J$.

The restriction is a continuous linear map from $\mathbb{R}^I$ to $\mathbb{R}^J$.
The map of a Gaussian measure by a continuous linear map is Gaussian ([isGaussian_map](#lem:isGaussian_map)).
It thus suffices to show that the mean and covariance matrix of the map are equal to the ones of $P^B_J$ by [IsGaussian.ext_iff](#lem:IsGaussian.ext_iff).

The mean of the map is $0$, since the mean of $P^B_I$ is $0$ and the map is linear.

Let us turn to the covariance matrix. For any $i \in J$, the map $x : \mathbb{R}^I \mapsto \pi_{IJ}(x) i$ is equal to $x : \mathbb{R}^I \mapsto x i$. Let $i, j \in J$. The covariance of $x : \mathbb{R}^J \mapsto x i$ and $x : \mathbb{R}^J \mapsto x j$ with respect to ${\pi_{IJ}}_*P^B_J$ is equal to the covariance of $x : \mathbb{R}^I \mapsto \pi_{IJ}(x) i$ and $x : \mathbb{R}^I \mapsto \pi_{IJ}(x) j$ with respect to $P^B_I$, which is equal to the covariance of $x : \mathbb{R}^I \mapsto x i$ and $x : \mathbb{R}^I \mapsto x i$ with respect to $P^B_I$, which is equal to $t_i \land t_j$. But this is also the covariance of $x : \mathbb{R}^J \mapsto x i$ and $x : \mathbb{R}^J \mapsto x j$ with respect to $P^B_J$, so we are done.

## Definition: gaussianLimit {#def:gaussianLimit lean="ProbabilityTheory.gaussianLimit" uses="thm:kolmogorovExtension, lem:isProjectiveMeasureFamily_gaussianProjectiveFamily"}

We denote by $P_B$ the projective limit of the projective family of the Brownian motion given by [Kolmogorov extension theorem](#thm:kolmogorovExtension).
This is a probability measure on $\mathbb{R}^{\mathbb{R}_+}$.

