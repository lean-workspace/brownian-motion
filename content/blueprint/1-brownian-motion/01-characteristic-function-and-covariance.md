---
title: 'Characteristic function and covariance'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Characteristic functions**

## Definition: Characteristic function {#def:charFunDual lean="MeasureTheory.charFunDual"}

The characteristic function of a measure $\mu$ on a normed space $E$ is the function $E^* \to \mathbb{C}$ defined by

$$
\begin{align*}
  \hat{\mu}(L) = \int_E e^{i L(x)} \: d\mu(x) \: .
\end{align*}
$$

## Theorem: ext_of_charFunDual {#thm:ext_of_charFunDual lean="MeasureTheory.Measure.ext_of_charFunDual" uses="def:charFunDual"}

In a separable Banach space, if two finite measures have same characteristic function, they are equal.

## Definition: Characteristic function {#def:charFun lean="MeasureTheory.charFun"}

The characteristic function of a measure $\mu$ on an inner product space $E$ is the function $E \to \mathbb{C}$ defined by

$$
\begin{align*}
  \hat{\mu}(t) = \int_E e^{i \langle t, x \rangle} \: d\mu(x) \: .
\end{align*}
$$

This is equal to the normed space version of the characteristic function applied to the linear map $x \mapsto \langle t, x \rangle$.

## Theorem: ext_of_charFun {#thm:ext_of_charFun lean="MeasureTheory.Measure.ext_of_charFun" uses="def:charFun"}

In a separable Hilbert space, if two finite measures have same characteristic function, they are equal.

## Lemma: charFun_map_eq_charFunDual_smul {#lem:charFun_map_eq_charFunDual_smul lean="MeasureTheory.charFun_map_eq_charFunDual_smul" uses="def:charFun, def:charFunDual"}

Let $\mu$ be a measure on $F$ and let $L \in F^*$. Then

$$
\begin{align*}
  \widehat{L_*\mu}(x) &= \hat{\mu}(x \cdot L) \: .
\end{align*}
$$

## Lemma: charFunDual_map {#lem:charFunDual_map lean="MeasureTheory.charFunDual_map" uses="def:charFunDual"}

Let $\mu$ be a measure on a normed space $E$ and let $L$ be a continuous linear map from $E$ to $F$.
Then for all $L' \in F^*$,

$$
\begin{align*}
  \widehat{L_*\mu}(L') = \hat{\mu}(L' \circ L) \: .
\end{align*}
$$

**Covariance**

Let $F$ be a Banach space and $E$ be a Hilbert space.

## Definition: Covariance {#def:covarianceBilin lean="ProbabilityTheory.covarianceBilinDual, ProbabilityTheory.covarianceBilinDual_apply, ProbabilityTheory.covarianceBilinDual_apply'"}

The covariance bilinear form of a measure $\mu$ on $F$ with finite second moment is the continuous bilinear form $C_\mu : F^* \times F^* \to \mathbb{R}$ with

$$
\begin{align*}
  C_\mu(L_1, L_2)
  &= \int_x (L_1(x) - L_1(m_\mu)) (L_2(x) - L_2(m_\mu)) \: d\mu(x)
  \\
  &= \int_x L_1(x - m_\mu) L_2(x- m_\mu) \: d\mu(x)
  \: .
\end{align*}
$$

## Lemma: covarianceBilin_same_eq_variance {#lem:covarianceBilin_same_eq_variance lean="ProbabilityTheory.covarianceBilinDual_self_eq_variance" uses="def:covarianceBilin"}

For $\mu$ a measure on $F$ with finite second moment and $L \in F^*$, $C_\mu(L, L) = \mathbb{V}_\mu[L]$.

## Definition: Covariance in a Hilbert space {#def:covInnerBilin lean="ProbabilityTheory.covarianceBilin"}

The covariance bilinear form of a finite measure $\mu$ with finite second moment on a Hilbert space $E$ is the continuous bilinear form $C_\mu : E \times E \to \mathbb{R}$ with

$$
\begin{align*}
  C'_\mu(x, y) = \int_z \langle x, z - m_\mu \rangle \langle y, z - m_\mu \rangle \: d\mu(z) \: .
\end{align*}
$$

This is $C_\mu$ applied to the linear maps $L_x, L_y \in E^*$ defined by $L_x(z) = \langle x, z \rangle$ and $L_y(z) = \langle y, z \rangle$.

## Lemma: covInnerBilin_map {#lem:covInnerBilin_map lean="ProbabilityTheory.covarianceBilin_map" uses="def:covInnerBilin"}

Let $E$ and $F$ be two Hilbert spaces with $F$ finite dimensional, $\mu$ a finite measure on $E$ with finite second moment, and $L : E \to F$ a continuous linear map.
Then the covariance bilinear form of the measure $L_*\mu$ is given by

$$
\begin{align*}
  C'_{L_*\mu}(u, v)
  &= C'_\mu(L^\dagger(u), L^\dagger(v))
  \: ,
\end{align*}
$$

in which $L^\dagger : F \to E$ is the adjoint of $L$.

### Proof

$$
\begin{align*}
  C'_{L_*\mu}(u, v)
  &= (L_*\mu)\left[\langle u, x - m_{L_*\mu}\rangle \langle x - m_{L_*\mu}, v \rangle\right]
  \\
  &= \mu\left[\langle u, L(x) - L(m_\mu)\rangle \langle L(x) - L(m_\mu), v \rangle \right]
  \\
  &= \mu\left[\langle L^\dagger(u), x - m_\mu\rangle \langle x - m_\mu, L^\dagger(v) \rangle \right]
  \\
  &= C'_\mu(L^\dagger(u), L^\dagger(v))
  \: .
\end{align*}
$$

## Definition: Covariance matrix {#def:covMatrix lean="ProbabilityTheory.covMatrix, ProbabilityTheory.posSemidef_covMatrix" uses="def:IsGaussian, lem:covarianceBilin_same_eq_variance"}

The covariance matrix of a finite measure $\mu$ with finite second moment on a finite dimensional inner product space $E$ is the positive semidefinite matrix $\Sigma_\mu$ such that for $u, v \in E$,

$$
\begin{align*}
  \langle u, \Sigma_\mu v\rangle = \mu[\langle u, x - m_\mu \rangle \langle x - m_\mu, v \rangle] \: .
\end{align*}
$$

This is the covariance bilinear form $C'_\mu(u, v)$, as a matrix.

## Lemma: covMatrix_map {#lem:covMatrix_map lean="ProbabilityTheory.covMatrix_map" uses="def:covMatrix"}

Let $E$ and $F$ be two finite dimensional inner product spaces, $\mu$ a measure on $E$ with finite second moment, and $L : E \to F$ a continuous linear map.
Then the covariance matrix of the measure $L_*\mu$ has entries

$$
\begin{align*}
  \langle e_i, \Sigma_{L_*\mu} e_j\rangle
  &= \langle L^\dagger(e_i), \Sigma_\mu L^\dagger(e_j)\rangle
  \: ,
\end{align*}
$$

in which $L^\dagger : F \to E$ is the adjoint of $L$.

### Proof {uses="lem:covInnerBilin_map"}

On the left-hand side we have
  
$$
\langle e_i, \Sigma_{L_*\mu} e_j\rangle = C'_{L_*\mu}(e_i, e_j) = C'_\mu(L^\dagger(e_i), L^\dagger(e_j)),
$$

  where the last equality comes from [covInnerBilin_map](#lem:covInnerBilin_map). On the right-hand side we have
  
$$
\langle L^\dagger(e_i), \Sigma_{L_*\mu} L^\dagger(e_j)\rangle = C'_\mu(L^\dagger(e_i), L^\dagger(e_j)),
$$

  which concludes the proof.

