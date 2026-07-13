---
title: 'Gaussian distributions'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Gaussian measures**

**Real Gaussian measures**

## Definition: Real Gaussian measure {#def:gaussianReal lean="ProbabilityTheory.gaussianReal"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

The real Gaussian measure with mean $\mu \in \mathbb{R}$ and variance $\sigma^2 > 0$ is the measure on $\mathbb{R}$ with density $\frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2 \sigma^2}\right)$ with respect to the Lebesgue measure.
  The real Gaussian measure with mean $\mu \in \mathbb{R}$ and variance $0$ is the Dirac measure $\delta_\mu$.
  We denote this measure by $\mathcal{N}(\mu, \sigma^2)$.

## Lemma: charFun_gaussianReal {#lem:charFun_gaussianReal lean="ProbabilityTheory.charFun_gaussianReal" uses="def:gaussianReal, def:charFun"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

The characteristic function of a real Gaussian measure with mean $\mu$ and variance $\sigma^2$ is given by
$x \mapsto \exp\left(i \mu x - \frac{\sigma^2 x^2}{2}\right)$.

## Lemma: centralMoment_two_mul_gaussianReal {#lem:centralMoment_two_mul_gaussianReal lean="ProbabilityTheory.centralMoment_two_mul_gaussianReal" uses="def:gaussianReal"}

The central moment of order $2n$ of a real Gaussian measure $\mathcal{N}(\mu, \sigma^2)$ is given by

$$
\begin{align*}
  \mathbb{E}[(X - \mu)^{2n}] = \sigma^{2n} (2n - 1)!! \: ,
\end{align*}
$$

in which $(2n - 1)!! = (2n - 1)(2n - 3) \cdots 3 \cdot 1$ is the double factorial of $2n - 1$.

### Proof

$$
\begin{align*}
	\mathbb{E}[(X - \mu)^{2n}] &= \int_{-\infty}^\infty (x - \mu)^{2n} \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} \mathrm dx \\
	&= \int_{-\infty}^\infty x^{2n} \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{x^2}{2 \sigma^2}} \mathrm dx \\
	&= 2 \int_{0}^\infty x^{2n} \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{x^2}{2 \sigma^2}} \mathrm dx \\
	&= 2 \int_{0}^\infty {\sqrt{2 \sigma^2 x}}^{2n} \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-x)} \frac{\sigma^2}{\sqrt{2 \sigma^2 x'}} \mathrm dx \\
	&= \frac{\sigma^{2n} 2^n}{\sqrt{\pi}} \int_{0}^\infty x^{n - 1/2} e{-x} \mathrm dx \\
	&= \frac{\sigma^{2n} 2^n}{\sqrt{\pi}} \Gamma(n + 1/2) \\
	&= \frac{\sigma^{2n} 2^n}{\Gamma(1/2)} \left( \prod_{k=0}^{n-1} (k + 1/2) \right) \Gamma(1/2) \\
	&= \sigma^{2n} \prod_{k=0}^{n-1} (2k + 1) \\
	&= \sigma^{2n} (2n - 1)!!
\end{align*}
$$

**Gaussian measures on a Banach space**

That kind of generality is not needed for this project, but we happen to have results about Gaussian measures on a Banach space in Mathlib, so we will use them.
The main reference for this section is [hairer2009introduction].

Let $F$ be a separable Banach space.

## Definition: Gaussian measure {#def:IsGaussian lean="ProbabilityTheory.IsGaussian" uses="def:gaussianReal"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A measure $\mu$ on $F$ is Gaussian if for every continuous linear form $L \in F^*$, the pushforward measure $L_* \mu$ is a Gaussian measure on $\mathbb{R}$.

## Lemma: IsGaussian.IsProbabilityMeasure {#lem:IsGaussian.IsProbabilityMeasure uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A Gaussian measure is a probability measure.

## Theorem: isGaussian_iff_charFunDual_eq {#thm:isGaussian_iff_charFunDual_eq lean="ProbabilityTheory.isGaussian_iff_charFunDual_eq" uses="def:IsGaussian, def:charFunDual"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A finite measure $\mu$ on $F$ is Gaussian if and only if for every continuous linear form $L \in F^*$, the characteristic function of $\mu$ at $L$ is

$$
\begin{align*}
  \hat{\mu}(L) = \exp\left(i \mu[L] - \mathbb{V}_\mu[L] / 2\right) \: ,
\end{align*}
$$

in which $\mathbb{V}_\mu[L]$ is the variance of $L$ with respect to $\mu$.

### Proof {uses="thm:ext_of_charFunDual, lem:charFun_gaussianReal"}

\paragraph{Transformations of Gaussian measures}

## Lemma: isGaussian_map {#lem:isGaussian_map lean="ProbabilityTheory.isGaussian_map" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $F, G$ be two Banach spaces, let $\mu$ be a Gaussian measure on $F$ and let $T : F \to G$ be a continuous linear map.
Then $T_*\mu$ is a Gaussian measure on $G$.

## Lemma: isGaussian_add_const {#lem:isGaussian_add_const uses="def:IsGaussian"}

Let $\mu$ be a Gaussian measure on $F$ and let $c \in F$.
Then the measure $\mu$ translated by $c$ (the map of $\mu$ by $x \mapsto x + c$) is a Gaussian measure on $F$.

## Lemma: isGaussian_conv {#lem:isGaussian_conv lean="ProbabilityTheory.isGaussian_conv" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

The convolution of two Gaussian measures is a Gaussian measure.

\paragraph{Fernique's theorem}

## Theorem: exists_integrable_exp_sq_of_map_rotation_eq_self {#thm:exists_integrable_exp_sq_of_map_rotation_eq_self lean="ProbabilityTheory.exists_integrable_exp_sq_of_map_rotation_eq_self"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $\mu$ be a finite measure on $F$ such that $\mu \times \mu$ is invariant under the rotation of angle $-\frac{\pi}{4}$.
Then there exists $C > 0$ such that the function $x \mapsto \exp (C \Vert x \Vert ^ 2)$ is integrable with respect to $\mu$.

## Lemma: IsGaussian.map_rotation_eq_self {#lem:IsGaussian.map_rotation_eq_self lean="ProbabilityTheory.IsGaussian.map_rotation_eq_self_of_forall_strongDual_eq_zero" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For a centered Gaussian measure $\mu$, $\mu \times \mu$ is invariant by rotation.

### Proof {uses="lem:isGaussian_conv"}

## Theorem: Fernique's theorem {#thm:IsGaussian.exists_integrable_exp_sq lean="ProbabilityTheory.IsGaussian.exists_integrable_exp_sq" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For a Gaussian measure, there exists $C > 0$ such that the function $x \mapsto \exp (C \Vert x \Vert ^ 2)$ is integrable.

### Proof {uses="thm:isGaussian_iff_charFunDual_eq, lem:IsGaussian.IsProbabilityMeasure, thm:exists_integrable_exp_sq_of_map_rotation_eq_self, lem:IsGaussian.map_rotation_eq_self"}

## Lemma: IsGaussian.memLp_id {#lem:IsGaussian.memLp_id lean="ProbabilityTheory.IsGaussian.memLp_id" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A Gaussian measure $\mu$ has finite moments of all orders.
In particular, there is a well defined mean $m_\mu := \mu[\mathrm{id}]$, and for all $L \in F^*$, $\mu[L] = L(m_\mu)$.

### Proof {uses="thm:IsGaussian.exists_integrable_exp_sq"}

A Gaussian measure has finite second moment by [IsGaussian.memLp_id](#lem:IsGaussian.memLp_id), hence its covariance bilinear form is well defined.

**Gaussian measures on a finite dimensional Hilbert space**

We specialize directly from Banach space to finite dimensional Hilbert space since that's what we need in this project, although there are results for Gaussian measures on infinite dimensional Hilbert spaces that would worth stating.

## Lemma: isGaussian_iff_charFun_eq {#lem:isGaussian_iff_charFun_eq lean="ProbabilityTheory.isGaussian_iff_charFun_eq" uses="def:IsGaussian, def:charFunDual, def:charFun"}

A finite measure $\mu$ on a Hilbert space $E$ is Gaussian if and only if for every $t \in E$, the characteristic function of $\mu$ at $t$ is

$$
\begin{align*}
  \hat{\mu}(t) =  \exp\left(i \mu[\langle t, \cdot \rangle] - \mathbb{V}_\mu[\langle t, \cdot \rangle] / 2\right) \: .
\end{align*}
$$

### Proof {uses="thm:isGaussian_iff_charFunDual_eq"}

By [isGaussian_iff_charFunDual_eq](#thm:isGaussian_iff_charFunDual_eq), $\mu$ is Gaussian iff for every continuous linear form $L \in E^*$, the characteristic function of $\mu$ at $L$ is

$$
\begin{align*}
  \hat{\mu}(L) = \exp\left(i \mu[L] - \mathbb{V}_\mu[L] / 2\right) \: .
\end{align*}
$$

Every continuous linear form $L \in E^*$ can be written as $L(x) = \langle t, x \rangle$ for some $t \in E$, hence we have that $\mu$ is Gaussian iff for every $t \in E$,

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(i \mu[\langle t, \cdot \rangle] - \mathbb{V}_\mu[\langle t, \cdot \rangle] / 2\right) \: .
\end{align*}
$$

Let $E$ be a separable Hilbert space. We denote by $\langle \cdot, \cdot \rangle$ the inner product on $E$ and by $\Vert \cdot \Vert$ the associated norm.

## Lemma: IsGaussian.charFun_eq {#lem:IsGaussian.charFun_eq lean="ProbabilityTheory.IsGaussian.charFun_eq" uses="def:IsGaussian, def:charFun, def:covInnerBilin"}

The characteristic function of a Gaussian measure $\mu$ on $E$ is given by

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(i \langle t, m_\mu \rangle - \frac{1}{2} C'_\mu(t, t)\right) \: .
\end{align*}
$$

### Proof {uses="lem:isGaussian_iff_charFun_eq, lem:IsGaussian.memLp_id, lem:covarianceBilin_same_eq_variance"}

By [isGaussian_iff_charFun_eq](#lem:isGaussian_iff_charFun_eq), for every $t \in E$,

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(i \mu[\langle t, \cdot \rangle] - \mathbb{V}_\mu[\langle t, \cdot \rangle] / 2\right) \: .
\end{align*}
$$

By [IsGaussian.memLp_id](#lem:IsGaussian.memLp_id), $\mu$ has finite first moment and $\mu[\langle t, \cdot \rangle] = \langle t, m_\mu \rangle$. By the same lemma, $\mu$ has finite second moment and for any $t$ we have $\mathbb{V}_\mu[\langle t, \cdot\rangle] = C'_\mu(t, t)$.

## Lemma: isGaussian_iff_gaussian_charFun {#lem:isGaussian_iff_gaussian_charFun lean="ProbabilityTheory.isGaussian_iff_gaussian_charFun, ProbabilityTheory.gaussian_charFun_congr" uses="def:IsGaussian, def:charFun, def:covMatrix"}

A finite measure $\mu$ on $E$ is Gaussian if and only if there exists $m \in E$ and $C$ positive semidefinite such that for all $t \in E$, the characteristic function of $\mu$ at $t$ is

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(i \langle t, m \rangle - \frac{1}{2} C(t, t)\right) \: ,
\end{align*}
$$

If that's the case, then $m = m_\mu$ and $C = C'_\mu$.

Note that this lemma does not say that there exists a Gaussian measure for any such $m$ and $C$.
We will prove that later.

> **Proof.** 
  \uses{lem:IsGaussian.charFun_eq, lem:charFun_map_eq_charFunDual_smul, thm:ext_of_charFun}
[IsGaussian.charFun_eq](#lem:IsGaussian.charFun_eq) states that the characteristic function of a Gaussian measure has the wanted form.

Suppose now that there exists $m \in E$ and $C$ positive semidefinite such that for all $t \in E$, $\hat{\mu}(t) = \exp\left(i \langle t, m \rangle - \frac{1}{2} C(t, t)\right)$.

We need to show that for all $L \in E^*$, $L_*\mu$ is a Gaussian measure on $\mathbb{R}$.
Such an $L$ can be written as $\langle u, \cdot \rangle$ for some $u \in E$.
Let then $u \in E$. We compute the characteristic function of $\langle u, \cdot\rangle_*\mu$ at $x \in \mathbb{R}$ with [charFun_map_eq_charFunDual_smul](#lem:charFun_map_eq_charFunDual_smul):

$$
\begin{align*}
  \widehat{\langle u, \cdot\rangle_*\mu}(x)
  &= \hat{\mu}(x \cdot u)
  \\
  &= \exp\left(i x \langle u, m \rangle - \frac{1}{2} x^2 C(u, u)\right)
  \: .
\end{align*}
$$

This is the characteristic function of a Gaussian measure on $\mathbb{R}$ with mean $\langle u, m \rangle$ and variance $C(u, u)$.
By [ext_of_charFun](#thm:ext_of_charFun), $\langle u, \cdot\rangle_*\mu$ is Gaussian, hence $\mu$ is Gaussian.

By [IsGaussian.charFun_eq](#lem:IsGaussian.charFun_eq), we deduce that for any $t \in E$ we have
$$\exp\left(i\langle t, m \rangle - \frac{1}{2} C(t, t)\right) = \exp\left(i\langle t, m_\mu \rangle - \frac{1}{2} C'_\mu(t, t)\right).$$
In particular, for any $t$ there exists $n_t \in \mathbb{Z}$ such that
$$i\langle t, m \rangle - \frac{1}{2} C(t, t) = i\langle t, m_\mu \rangle - \frac{1}{2} C'_\mu(t, t) + 2i\pi n_t.$$
We deduce that $n$ is a continuous map from $E$ to $\mathbb{Z}$, and thus must be constant because $E$ is connected. By looking at the value at $t = 0$, we deduce that for any $t$, $n_t = 0$. Looking at real and imaginary parts we obtain that for any $t$,
$$\langle t, m \rangle = \langle t, m_\mu \rangle \quad \text{and} \quad C(t, t) = C'_\mu(t, t).$$
We immediately deduce that $m = m_\mu$. Moreover, because $C$ and $C'_\mu$ are symmetric, they are characterized by their values on the diagonal. Indeed, for any $x, y$,
$$C(x, y) = \frac{1}{2} (C(x + y, x + y) - C(x, x) - C(y, y)).$$
We deduce that $C = C'_\mu$.

## Lemma: IsGaussian.ext_iff {#lem:IsGaussian.ext_iff lean="ProbabilityTheory.IsGaussian.ext, ProbabilityTheory.IsGaussian.ext_iff" uses="def:IsGaussian, def:covInnerBilin"}

Two Gaussian measures $\mu$ and $\nu$ on a separable Hilbert space are equal if and only if they have same mean and same covariance.

### Proof {uses="thm:ext_of_charFun, lem:IsGaussian.charFun_eq"}

The forward direction is immediate.

For the converse direction, it is enough to show that $\mu$ and $\nu$ have the same characteristic function by [ext_of_charFun](#thm:ext_of_charFun). As they are both Gaussian, their characteristic functions only depend on their mean and covariance by [IsGaussian.charFun_eq](#lem:IsGaussian.charFun_eq). Thus they are equal.

## Definition: Standard Gaussian measure {#def:stdGaussian lean="ProbabilityTheory.stdGaussian" uses="def:gaussianReal"}

Let $(e_1, \ldots, e_d)$ be an orthonormal basis of $E$ and let $\mu$ be the standard Gaussian measure on $\mathbb{R}$.
The standard Gaussian measure on $E$ is the pushforward measure of the product measure $\mu \times \ldots \times \mu$ by the map $x \mapsto \sum_{i=1}^d x_i \cdot e_i$.

The fact that this definition does not depend on the choice of basis will be a consequence of the fact that its characteristic function does not depend on the basis.

## Lemma: integral_eval_pi {#lem:integral_eval_pi lean="MeasureTheory.integral_comp_eval"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For $\mu_1, \ldots, \mu_d$ probability measures on $\mathbb{R}$ and $f : \mathbb{R} \to \mathbb{R}$ integrable with respect to $\mu_i$, we have

$$
\begin{align*}
  \int_x f(x_i) \, d(\mu_1 \times \ldots \times \mu_d)(x)
  = \int_x f(x) \, d\mu_i
  \: .
\end{align*}
$$

### Proof

As $f$ is integrable, we can use Fubini theorem to obtain that
$$\int f(x_i) \, d(\mu_1 \times \ldots \times \mu_d)(x) = \int f(x) \, d\mu_i(x) \times \prod_{j \ne i} \int 1 \, d\mu_j(x) = \int f(x) \, d\mu_i(x)$$
because the $\mu_j$s are probability measures.

## Lemma: isCentered_stdGaussian {#lem:isCentered_stdGaussian lean="ProbabilityTheory.integral_strongDual_stdGaussian" uses="def:stdGaussian"}

The standard Gaussian measure on $E$ is centered, i.e., $\mu[L] = 0$ for every $L \in E^*$.

### Proof {uses="lem:integral_eval_pi"}

## Lemma: isProbabilityMeasure_stdGaussian {#lem:isProbabilityMeasure_stdGaussian lean="ProbabilityTheory.isProbabilityMeasure_stdGaussian" uses="def:stdGaussian"}

The standard Gaussian measure is a probability measure.

## Lemma: charFun_stdGaussian {#lem:charFun_stdGaussian lean="ProbabilityTheory.charFun_stdGaussian" uses="def:stdGaussian, def:charFun"}

The characteristic function of the standard Gaussian measure on $E$ is given by

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(-\frac{1}{2} \Vert t \Vert^2 \right) \: .
\end{align*}
$$

### Proof {uses="lem:charFun_gaussianReal"}

Denote by $\nu$ the standard Gaussian measure on $\mathbb{R}$. This is a straightforward computation:

$$
\begin{align*}
  \hat{\mu}(t) = \int \exp\left(i\langle t, \sum_{j=1}^d x_j \cdot e_j \rangle\right) d(\nu \times \ldots \times \nu)(dx) &= \int \exp\left(\sum_{j=1}^d ix_j\langle t, e_j \rangle\right) d(\nu \times \ldots \times \nu)(dx) \\
  &= \int \prod_{j=1}^d \exp\left(ix_j\langle t, e_j \rangle\right) d(\nu \times \ldots \times \nu)(dx) \\
  &= \prod_{j=1}^d \int \exp\left(ix\langle t, e_j \rangle\right) d\nu(x) \\
  &= \prod_{j=1}^d \exp\left(-\frac{\langle t, e_j \rangle^2}{2}\right) \\
  &= \exp\left(-\frac{1}{2} \Vert t \Vert^2 \right).
\end{align*}
$$

## Lemma: isGaussian_stdGaussian {#lem:isGaussian_stdGaussian lean="ProbabilityTheory.isGaussian_stdGaussian" uses="def:stdGaussian, def:IsGaussian"}

The standard Gaussian measure on $E$ is a Gaussian measure.

### Proof {uses="lem:isGaussian_iff_gaussian_charFun, lem:charFun_stdGaussian, lem:isProbabilityMeasure_stdGaussian"}

Since the standard Gaussian is a probability measure (hence finite), we can apply [isGaussian_iff_gaussian_charFun](#lem:isGaussian_iff_gaussian_charFun) that states that it suffices to show that the characteristic function has a particular form.
That form is given by [charFun_stdGaussian](#lem:charFun_stdGaussian), taking $m=0$ and $C = \langle\cdot, \cdot\rangle$.

## Lemma: integral_id_stdGaussian {#lem:integral_id_stdGaussian lean="ProbabilityTheory.integral_id_stdGaussian" uses="def:stdGaussian"}

The mean of the standard Gaussian measure is $0$.

### Proof {uses="lem:integral_eval_pi"}

## Lemma: covMatrix_stdGaussian {#lem:covMatrix_stdGaussian lean="ProbabilityTheory.covMatrix_stdGaussian" uses="def:stdGaussian, def:covMatrix"}

The covariance matrix of the standard Gaussian measure is the identity matrix.

### Proof {uses="lem:isGaussian_iff_gaussian_charFun, lem:charFun_stdGaussian"}

From [charFun_stdGaussian](#lem:charFun_stdGaussian), we know that for all $t \in \mathbb{R}$,
$$\hat{\mu}(t) = \exp\left(-\frac{\|t\|^2}{2}\right) = \exp\left(-\frac{\langle t, \mathrm{I}t\rangle}{2}\right).$$
As the identity is positive semidefinite, we deduce from [isGaussian_iff_gaussian_charFun](#lem:isGaussian_iff_gaussian_charFun) that $\Sigma_\mu$ is the identity matrix.

## Definition: Multivariate Gaussian {#def:multivariateGaussian lean="ProbabilityTheory.multivariateGaussian" uses="def:stdGaussian"}

The multivariate Gaussian measure on $\mathbb{R}^d$ with mean $m \in \mathbb{R}^d$ and covariance matrix $\Sigma \in \mathbb{R}^{d \times d}$, with $\Sigma$ positive semidefinite, is the pushforward measure of the standard Gaussian measure on $\mathbb{R}^d$ by the map $x \mapsto m + \Sigma^{1/2} x$.
We denote this measure by $\mathcal{N}(m, \Sigma)$.

## Lemma: integral_id_multivariateGaussian {#lem:integral_id_multivariateGaussian lean="ProbabilityTheory.integral_id_multivariateGaussian" uses="def:multivariateGaussian"}

The mean of the multivariate Gaussian measure $\mathcal{N}(m, \Sigma)$ is $m$.

### Proof {uses="lem:integral_id_stdGaussian"}

## Lemma: covMatrix_multivariateGaussian {#lem:covMatrix_multivariateGaussian lean="ProbabilityTheory.covarianceBilin_multivariateGaussian" uses="def:multivariateGaussian"}

The covariance matrix of the multivariate Gaussian measure $\mathcal{N}(m, \Sigma)$ is $\Sigma$.

### Proof {uses="lem:covMatrix_stdGaussian"}

## Lemma: isGaussian_multivariateGaussian {#lem:isGaussian_multivariateGaussian lean="ProbabilityTheory.isGaussian_multivariateGaussian" uses="def:multivariateGaussian, def:IsGaussian"}

A multivariate Gaussian measure is a Gaussian measure.

### Proof {uses="lem:isGaussian_stdGaussian, lem:isGaussian_add_const, lem:isGaussian_map"}

The multivariate Gaussian measure is the pushforward of the standard Gaussian measure by an affine map, and is thus Gaussian by [isGaussian_add_const](#lem:isGaussian_add_const) and [isGaussian_map](#lem:isGaussian_map).

## Theorem: charFun_multivariateGaussian {#thm:charFun_multivariateGaussian lean="ProbabilityTheory.charFun_multivariateGaussian" uses="def:multivariateGaussian, def:charFun"}

The characteristic function of a multivariate Gaussian measure $\mathcal{N}(m, \Sigma)$ is given by

$$
\begin{align*}
  \hat{\mu}(t) = \exp\left(i \langle m, t \rangle - \frac{1}{2} \langle t, \Sigma t \rangle\right)
  \: .
\end{align*}
$$

### Proof {uses="lem:isGaussian_multivariateGaussian, lem:IsGaussian.charFun_eq, lem:integral_id_multivariateGaussian, lem:covMatrix_multivariateGaussian"}

Since the multivariate Gaussian measure is a Gaussian measure, we can apply [IsGaussian.charFun_eq](#lem:IsGaussian.charFun_eq) to it.
It suffices then to show that the mean and the covariance matrix of the multivariate Gaussian measure are equal to $m$ and $\Sigma$, respectively.
This is given by [integral_id_multivariateGaussian](#lem:integral_id_multivariateGaussian) and [covMatrix_multivariateGaussian](#lem:covMatrix_multivariateGaussian).

**Gaussian processes**

## Definition: Gaussian process {#def:IsGaussianProcess lean="ProbabilityTheory.IsGaussianProcess" uses="def:IsGaussian"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A process $X : T \to \Omega \to E$ is Gaussian if for every finite subset $t_1, \ldots, t_n \in T$, the random vector $(X_{t_1}, \ldots, X_{t_n})$ has a Gaussian distribution.

## Lemma: isGaussianProcess_of_modification {#lem:isGaussianProcess_of_modification lean="ProbabilityTheory.IsGaussianProcess.congr" uses="def:IsGaussianProcess"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X, Y : T \to \Omega \to E$ be two stochastic processes that are modifications of each other (that is, for all $t \in T$, $X_t =_{a.e.} Y_t$).
If $X$ is a Gaussian process, then $Y$ is a Gaussian process as well.

### Proof {uses="lem:map_eq_of_modification"}

Being a Gaussian process is defined in terms of the distribution of finite-dimensional random vectors.
By [map_eq_of_modification](#lem:map_eq_of_modification), the random vector $(Y_{t_1}, \ldots, Y_{t_n})$ has the same distribution as the random vector $(X_{t_1}, \ldots, X_{t_n})$ for all $t_1, \ldots, t_n \in T$.

