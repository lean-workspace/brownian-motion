---
title: 'Classes of martingales and related processes'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

The main reference for this part is [@he2019semimartingale].

Notations for classes of processes:

- $\mathcal{V}$: finite variation processes ([Finite variation process, $\mathcal{V}$](#def:HasFiniteVariation))
- $\mathcal{V}^+$: non-decreasing finite variation processes
- $\mathcal{A}$: adapted processes with integrable variation ([Integrable variation, $\mathcal{A}$](#def:HasIntegrableVariation))
- $\mathcal{A}^+$: non-decreasing adapted integrable processes
- $\mathcal{M}$: càdlàg martingales (TODO: [@he2019semimartingale] add uniform integrability)
- $\mathcal{M}^c$: continuous martingales
- $\mathcal{M}^2$: square-integrable martingales ([Square integrable martingales](#def:IsSquareIntegrable))
- $\mathcal{C}_{\mathrm{loc}}$ for a class $\mathcal{C}$: processes that are locally in $\mathcal{C}$

Note: [@he2019semimartingale] use $\mathcal{W}$ for $\mathcal{M} \cap \mathcal{A}$.

**Jumps of a process**

## Definition: Jumps of a process {#def:jump}

The jumps of a process $X : T \to \Omega \to E$ is the process $\Delta X : T \to \Omega \to E$ defined by $(t, \omega) \mapsto X_t(\omega) - X_{t^-}(\omega)$ .

## Definition: Jump part {#def:jumpPart uses="def:jump"}

The jump part (or purely discontinuous part) of a process $X : T \to \Omega \to E$ is the process $X^d : T \to \Omega \to E$ defined by $(t, \omega) \mapsto \sum_{0 < s \le t} \Delta X_s(\omega)$ .

## Definition: Continuous part {#def:continuousPart uses="def:jumpPart"}

The continuous part of a process $X : T \to \Omega \to E$ is the process $X^c : T \to \Omega \to E$ defined by $(t, \omega) \mapsto X_t(\omega) - X^d_t(\omega)$ .

## Definition: Large jumps {#def:largeJump uses="def:jump"}

The large jump part of a process $X : T \to \Omega \to E$ at level $\varepsilon$ is the process $X^{d, \varepsilon} : T \to \Omega \to E$ defined by $(t, \omega) \mapsto \sum_{0 < s \le t} \Delta X_s(\omega) \mathbb{1}_{\{\Vert \Delta X_s(\omega) \Vert > \varepsilon\}}$ .

**Integrable variation**

## Definition: Extended variation {#def:eVariationOn lean="eVariationOn"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

The (extended-real-valued) variation of a function $f : T \to E$ on a set $s$ inside a linear order is the supremum of $\sum_i \mathrm{edist}(f(u_{i+1}, f(u_i)))$ over all finite increasing sequences $u : N \to T$ in $s$.
We denote it by $V_f(s)$ .

## Definition: Bounded variation {#def:BoundedVariationOn lean="BoundedVariationOn" uses="def:eVariationOn"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A function $f : T \to E$ is of bounded variation on a set $s$ if its variation $V_f(s)$ is finite.

## Definition: Locally bounded variation {#def:LocallyBoundedVariationOn lean="LocallyBoundedVariationOn" uses="def:BoundedVariationOn"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A function $f : T \to E$ is of locally bounded variation on a set $s$ if for every $a, b$ in $s$, the variation $V_f(s \cap [a, b])$ is finite.

## Lemma: LocallyBoundedVariationOn.countable_not_continuous_at {#lem:LocallyBoundedVariationOn.countable_not_continuous_at uses="def:LocallyBoundedVariationOn"}

The set of points of discontinuity of a function of locally bounded variation is at most countable.

### Proof

Mathlib has the result for monotone functions and has the fact that a function of locally bounded variation is the difference of two monotone functions.

## Definition: Finite variation process, $\mathcal{V}$ {#def:HasFiniteVariation uses="def:LocallyBoundedVariationOn"}

A process $X : T \to \Omega \to E$ is of finite variation if it is right-continuous and for every $\omega \in \Omega$, the path $t \mapsto X_t(\omega)$ is of locally bounded variation on $T$ .

We denote by $\mathcal{V}$ the class of finite variation processes.

## Lemma: HasFiniteVariation.isCadlag {#lem:HasFiniteVariation.isCadlag uses="def:HasFiniteVariation, def:IsCadlag"}

A finite variation process is càdlàg.

### Proof

Right-continuity is by definition. Left limits exist because a function of locally bounded variation has left limits (that should be in Mathlib's file about locally bounded variation).

## Definition: variationProcess {#def:variationProcess uses="def:eVariationOn, def:LocallyBoundedVariationOn"}

The variation of a process $X : T \to \Omega \to E$ is the process $V_X : T \to \Omega \to \mathbb{R}$ defined by $(t, \omega) \mapsto V_{X(\omega)}([0,t])$ .

## Lemma: monotone_variationProcess {#lem:monotone_variationProcess uses="def:variationProcess"}

The variation process $V_X$ of a process $X$ is non-decreasing.

## Lemma: rightContinuous_variationProcess {#lem:rightContinuous_variationProcess uses="def:variationProcess"}

The variation process $V_X$ of a right-continuous process $X$ is right-continuous.

## Definition: Integrable variation, $\mathcal{A}$ {#def:HasIntegrableVariation uses="def:HasIntegrableSup, def:variationProcess"}

We say that a stochastic process $X$ has integrable variation if its variation process $V_X$ ([variationProcess](#def:variationProcess)) is integrable ([Integrable supremum](#def:HasIntegrableSup)).

We denote by $\mathcal{A}$ the class of adapted processes with integrable variation.

We denote by $\mathcal{A}^+$ the class of non-decreasing adapted integrable processes.

We denote by $\mathcal{V}^+$ the class of non-decreasing adapted processes.

**Square integrable martingales**

In this section, $E$ denotes a complete normed space.

## Definition: Square integrable martingales {#def:IsSquareIntegrable lean="ProbabilityTheory.IsSquareIntegrable" uses="def:Martingale"}

Let $T$ be a linear order with bottom element 0, on which we have a filtration $\mathcal{F}$ satisfying the usual conditions.
We say that a martingale $M : T \to \Omega \to E$ is square integrable if it is càdlàg and $\sup_{t \in T} \Vert M_t \Vert_{L^2} < \infty$ (Lean remark: use `eLpNorm (M t) 2`).

**The Hilbert space of square integrable martingales**

## Lemma: IsSquareIntegrable.module {#lem:IsSquareIntegrable.module lean="ProbabilityTheory.IsSquareIntegrable.add, ProbabilityTheory.IsSquareIntegrable.smul" uses="def:IsSquareIntegrable"}

If $M$ and $N$ are square integrable martingales and $a \in \mathbb{R}$, then $M + N$ and $a M$ are square integrable martingales.

## Lemma: IsSquareIntegrable.submartingale_sq {#lem:IsSquareIntegrable.submartingale_sq lean="ProbabilityTheory.IsSquareIntegrable.submartingale_sq_norm" uses="def:IsSquareIntegrable, def:Submartingale"}

If $M$ is a square integrable martingale, then $\Vert M \Vert^2$ is a submartingale.

### Proof {uses="lem:Martingale.submartingale_convex_comp"}

Apply [Martingale.submartingale_convex_comp](#lem:Martingale.submartingale_convex_comp) with the convex function $f: x \mapsto \Vert x \Vert^2$ .

## Lemma: IsSquareIntegrable.eLpNorm_two_mono {#lem:IsSquareIntegrable.eLpNorm_two_mono lean="ProbabilityTheory.IsSquareIntegrable.eLpNorm_mono" uses="def:IsSquareIntegrable"}

For $M$ a square integrable martingale, the function $t \mapsto \Vert M_t \Vert_{L^2}$ is non-decreasing.

### Proof {uses="lem:IsSquareIntegrable.submartingale_sq"}

By [IsSquareIntegrable.submartingale_sq](#lem:IsSquareIntegrable.submartingale_sq), $\Vert M_t \Vert^2$ is a submartingale.
Thus, for $s \le t$ ,

$$
\begin{align*}
  \Vert M_s \Vert_{L^2}^2
  &= \mathbb{E}[\Vert M_s \Vert^2]
  \\
  &\le \mathbb{E}[\Vert M_t \Vert^2]
  \\
  &= \Vert M_t \Vert_{L^2}^2
  \: .
\end{align*}
$$

## Lemma: IsSquareIntegrable.tendsto_limitProcess {#lem:IsSquareIntegrable.tendsto_limitProcess lean="ProbabilityTheory.IsSquareIntegrable.ae_tendsto_limitProcess, ProbabilityTheory.IsSquareIntegrable.tendsto_eLpNorm_two_limitProcess" uses="def:IsSquareIntegrable, def:limitProcess"}

For $M$ a square integrable martingale, we have $M_t \to M_\infty$ almost surely and in $L^2$ as $t \to \infty$ .

### Proof {uses="thm:tendsto_limitProcess_of_cadlag"}

TODO: use a martingale convergence theorem. Check whether [tendsto_limitProcess_of_cadlag](#thm:tendsto_limitProcess_of_cadlag) is what we need.

## Lemma: IsSquareIntegrable.sup_eLpNorm_eq_eLpNorm_limitProcess {#lem:IsSquareIntegrable.sup_eLpNorm_eq_eLpNorm_limitProcess uses="def:IsSquareIntegrable, def:limitProcess"}

For $M$ a square integrable martingale,

$$
\begin{align*}
  \sup_{t \in T} \Vert M_t \Vert_{L^2}
  &= \Vert M_\infty \Vert_{L^2}
  \: .
\end{align*}
$$

### Proof {uses="lem:IsSquareIntegrable.eLpNorm_two_mono, lem:IsSquareIntegrable.tendsto_limitProcess"}

## Definition: L2Martingales {#def:L2Martingales uses="def:IsSquareIntegrable"}

We denote by $\mathcal{M}^2(E)$ or simply $\mathcal{M}^2$ the space of equivalence classes with respect to indistinguishability of square integrable martingales $T \to \Omega \to E$ .

## Lemma: L2Martingales.module {#lem:L2Martingales.module uses="def:L2Martingales"}

The space $\mathcal{M}^2(E)$ is a real vector space.

### Proof {uses="lem:IsSquareIntegrable.module"}

## Definition: L2Martingales.norm {#def:L2Martingales.norm uses="def:L2Martingales, def:limitProcess"}

We define a norm on $\mathcal{M}^2$ by

$$
\begin{align*}
  \Vert M \Vert = \Vert M_\infty \Vert_{L^2}
  \: .
\end{align*}
$$

## Lemma: L2Martingales.norm_eq_zero {#lem:L2Martingales.norm_eq_zero uses="def:L2Martingales.norm"}

For $M \in \mathcal{M}^2(E)$, $\Vert M \Vert = 0$ if and only if $M = 0$.

### Proof {uses="lem:IsSquareIntegrable.sup_eLpNorm_eq_eLpNorm_limitProcess"}

By [IsSquareIntegrable.sup_eLpNorm_eq_eLpNorm_limitProcess](#lem:IsSquareIntegrable.sup_eLpNorm_eq_eLpNorm_limitProcess), $\Vert M \Vert = 0$ if and only if for all $t \in T$, $\Vert M_t \Vert_{L^2} = 0$ .

## Definition: L2Martingales.inner {#def:L2Martingales.inner uses="def:L2Martingales.norm"}

We define an inner product on $\mathcal{M}^2$ by

$$
\begin{align*}
  \langle M, N \rangle_{\mathcal{M}^2} = \mathbb{E}[M_\infty N_\infty]
  \: .
\end{align*}
$$

## Theorem: hilbertSpace_L2Martingales {#thm:hilbertSpace_L2Martingales uses="def:L2Martingales.inner, lem:L2Martingales.norm_eq_zero"}

The space $\mathcal{M}^2$ is a Hilbert space.

### Proof {uses="cor:doob_lp_norm, lem:L2Martingales.module"}

We already know that $\mathcal{M}^2$ is an inner product space.
We need to show that it is complete.

It suffices to show that every Cauchy sequence with a distance bound converges to a limit in $\mathcal{M}^2$.
Namely, we can consider sequences $(M^n)_{n \in \mathbb{N}}$ in $\mathcal{M}^2$ such that for $n, m \ge N$, $\Vert M^n - M^m \Vert < 2^{-N}$ (See `Metric.complete\_of\_convergent\_controlled\_sequences`, or the `EMetric` version).

Let then $(M^n)_{n \in \mathbb{N}}$ be such a Cauchy sequence.

TODO

**Elementary stochastic integrals**

## Lemma: eLpNorm_elemStochIntegralBilin_le {#lem:eLpNorm_elemStochIntegralBilin_le uses="def:IsSquareIntegrable, def:elemStochIntegralBilin"}

For $V \in \mathcal{E}_{T, F}$ bounded by a constant $D$, $M \in \mathcal{M}^2(E)$ and a continuous bilinear map $B: E \times F \to G$,

$$
\begin{align*}
  \Vert (V \bullet_B M)_t \Vert_{L^2}
  \le 2 D \: \Vert B \Vert \: \sup_t \Vert M_t \Vert_{L^2}
\end{align*}
$$

TODO: this can be improved to $D \: \Vert B \Vert \: \Vert M_t \Vert_{L^2}$?

### Proof

Let $C$ be a bound on $\Vert M_t \Vert_{L^2}$ for all $t \in T$ .
Let $(s_k < t_k)_{k \in \{1, ..., n\}}$ and $\eta_k$ be the intervals and random variables defining $V$ .
Let $D$ be a bound on $\Vert\eta_k\Vert$.
Then, for all $t$ ,

$$
\begin{align*}
  \Vert (V \bullet_B M)_t \Vert_{L^2}
  &\le \sum_{k=1}^n \Vert B(M^t_{t_k} - M^t_{s_k}, \eta_k) \Vert_{L^2}
  \: .
\end{align*}
$$

Since only at most one term of that sum is non-zero for each fixed $t$ , we can bound the sum by the maximum of its terms.
It suffices then to bound each term of that sum.

TODO: here we supposed that the intervals of the simple process are disjoint. Check with our Lean def.

For each $k$ ,

$$
\begin{align*}
  \Vert B(M^t_{t_k} - M^t_{s_k}, \eta_k) \Vert_{L^2}
  &\le \left\Vert \Vert B \Vert \: \Vert M^t_{t_k} - M^t_{s_k} \Vert  \: \Vert \eta_k \Vert \right\Vert_{L^2}
  \\
  &\le \Vert B \Vert \: \Vert M^t_{t_k} - M^t_{s_k} \Vert_{L^2} \: D
  \\
  &\le 2 \Vert B \Vert \: C \: D
  \: .
\end{align*}
$$

## Lemma: isSquareIntegrable_elemStochIntegralBilin {#lem:isSquareIntegrable_elemStochIntegralBilin uses="def:IsSquareIntegrable, def:elemStochIntegralBilin"}

For $V \in \mathcal{E}_{T, F}$, $M \in \mathcal{M}^2(E)$ and a continuous bilinear map $B: E \times F \to G$, the elementary stochastic integral $V \bullet_B M$ is in $\mathcal{M}^2(G)$.

### Proof {uses="lem:cadlag_elemStochIntegralBilin, lem:Martingale.elemStochIntegral, lem:eLpNorm_elemStochIntegralBilin_le"}

By [cadlag_elemStochIntegralBilin](#lem:cadlag_elemStochIntegralBilin), $V \bullet_B M$ is càdlàg, and we know that it is a martingale by [Martingale.elemStochIntegral](#lem:Martingale.elemStochIntegral) .
It remains to show that $\sup_{t \in T} \Vert (V \bullet_B M)_t \Vert_{L^2} < \infty$ .
By [eLpNorm_elemStochIntegralBilin_le](#lem:eLpNorm_elemStochIntegralBilin_le), this supremum is bounded by $2 D \Vert B \Vert \sup_{t \in T} \Vert M_t \Vert_{L^2}$, which is finite since $M \in \mathcal{M}^2(E)$ and $V$ is bounded.

## Lemma: inner_elemStochIntegral {#lem:inner_elemStochIntegral uses="def:IsSquareIntegrable, def:elemStochIntegralBilin, lem:isSquareIntegrable_elemStochIntegralBilin"}

For $V \in \mathcal{E}_{T, \mathbb{R}}$ and $M, N \in \mathcal{M}^2$, we have

$$
\begin{align*}
  \langle V \bullet_{\mathbb{R}} M, N \rangle_{\mathcal{M}^2}
  &= V \bullet_{\mathbb{R}} \langle M, N \rangle_{\mathcal{M}^2}
  \: .
\end{align*}
$$

**Locally square integrable martingales**

**Definition and basic properties**

## Definition: Locally square-integrable martingales {#def:IsLocallySquareIntegrable lean="ProbabilityTheory.IsLocallySquareIntegrable" uses="def:IsSquareIntegrable, def:locally"}

A process is locally square-integrable if it locally satisfies the square-integrable martingale property.
We denote that class of processes by $\mathcal{M}^2_{\mathrm{loc}}$ .

## Lemma: IsSquareIntegrable.isLocallySquareIntegrable {#lem:IsSquareIntegrable.isLocallySquareIntegrable lean="ProbabilityTheory.IsSquareIntegrable.isLocallySquareIntegrable" uses="def:IsSquareIntegrable, def:IsLocallySquareIntegrable"}

Every square-integrable martingale is locally square-integrable: $\mathcal{M}^2 \subseteq \mathcal{M}^2_{\mathrm{loc}}$ .

### Proof {uses="lem:implies_locally"}

This follows from [implies_locally](#lem:implies_locally).

## Lemma: IsLocallySquareIntegrable.isLocalSubmartingale_sq_norm {#lem:IsLocallySquareIntegrable.isLocalSubmartingale_sq_norm lean="ProbabilityTheory.IsLocallySquareIntegrable.isLocalSubmartingale_sq_norm" uses="def:IsLocallySquareIntegrable, def:IsLocalSubmartingale"}

If $M \in \mathcal{M}^2_{\mathrm{loc}}$, then $\Vert M \Vert^2$ is a càdlàg local submartingale.

### Proof {uses="lem:IsSquareIntegrable.submartingale_sq"}

## Lemma: IsLocalMartingale.isLocallySquareIntegrable_of_continuous {#lem:IsLocalMartingale.isLocallySquareIntegrable_of_continuous uses="def:IsLocalMartingale, def:IsLocallySquareIntegrable"}

A continuous local martingale is locally square-integrable: $\mathcal{M}^c_{\mathrm{loc}} \subseteq \mathcal{M}^2_{\mathrm{loc}}$ .

**Predictable quadratic variation**

## Definition: Predictable quadratic variation {#def:quadraticVariation lean="ProbabilityTheory.quadraticVariation" uses="def:IsLocallySquareIntegrable, def:IsCadlag, thm:local_doobMeyer, lem:IsLocallySquareIntegrable.isLocalSubmartingale_sq_norm"}

For $M \in \mathcal{M}^2_{\mathrm{loc}}$ with càdlàg paths, the predictable
quadratic variation of $M$ is defined as the predictable part of the Doob-Meyer decomposition of the local submartingale $\Vert M \Vert^2$ .
We denote it by $\langle M \rangle$ .

## Lemma: predictable_quadraticVariation {#lem:predictable_quadraticVariation uses="def:quadraticVariation"}

The predictable quadratic variation $\langle M \rangle$ of $M \in \mathcal{M}^2_{\mathrm{loc}}$ is a predictable process.

### Proof {uses="thm:local_doobMeyer"}

## Lemma: cadlag_quadraticVariation {#lem:cadlag_quadraticVariation uses="def:quadraticVariation"}

The predictable quadratic variation $\langle M \rangle$ of $M \in \mathcal{M}^2_{\mathrm{loc}}$ is càdlàg.

### Proof {uses="thm:local_doobMeyer"}

## Lemma: locallyIntegrable_quadraticVariation {#lem:locallyIntegrable_quadraticVariation uses="def:quadraticVariation"}

The predictable quadratic variation $\langle M \rangle$ of $M \in \mathcal{M}^2_{\mathrm{loc}}$ is locally integrable.

### Proof {uses="thm:local_doobMeyer"}

## Lemma: quadraticVariation_zero {#lem:quadraticVariation_zero uses="def:quadraticVariation"}

$\langle M \rangle_0 = 0$ .

### Proof {uses="thm:local_doobMeyer"}

## Lemma: monotone_quadraticVariation {#lem:monotone_quadraticVariation uses="def:quadraticVariation"}

The predictable quadratic variation $\langle M \rangle$ of $M \in \mathcal{M}^2_{\mathrm{loc}}$ is non-decreasing.

### Proof {uses="thm:local_doobMeyer"}

## Lemma: local_martingale_sub_quadraticVariation {#lem:local_martingale_sub_quadraticVariation uses="def:quadraticVariation"}

For $M \in \mathcal{M}^2_{\mathrm{loc}}$, the process $\Vert M_t \Vert^2 - \langle M \rangle_t$ is a local martingale.

### Proof {uses="thm:local_doobMeyer"}

## Definition: Predictable covariation {#def:covariation uses="def:IsLocallySquareIntegrable, def:quadraticVariation"}

For $M, N \in \mathcal{M}^2_{\mathrm{loc}}$, the predictable covariation $\langle M, N \rangle$ is a stochastic process defined by polarization of the predictable quadratic variation:

$$
\begin{align*}
  \langle M, N \rangle_t = \frac{1}{4}\left(\langle M+N \rangle_t - \langle M-N \rangle_t \right)
  \: .
\end{align*}
$$

## Lemma: predictable_covariation {#lem:predictable_covariation uses="def:covariation"}

The predictable covariation $\langle M, N \rangle$ of $M, N \in \mathcal{M}^2_{\mathrm{loc}}$ is a predictable process.

### Proof {uses="lem:predictable_quadraticVariation"}

## Lemma: cadlag_covariation {#lem:cadlag_covariation uses="def:covariation"}

The predictable covariation $\langle M, N \rangle$ of $M, N \in \mathcal{M}^2_{\mathrm{loc}}$ is càdlàg.

### Proof {uses="lem:cadlag_quadraticVariation"}

## Lemma: covariation_zero {#lem:covariation_zero uses="def:covariation"}

$\langle M, N \rangle_0 = 0$ .

### Proof {uses="lem:quadraticVariation_zero"}

## Lemma: local_martingale_sub_covariation {#lem:local_martingale_sub_covariation uses="def:covariation"}

For $M, N \in \mathcal{M}^2_{\mathrm{loc}}$, the process $\langle M_t, N_t \rangle_E - \langle M, N \rangle_t$ is a local martingale.

### Proof {uses="lem:local_martingale_sub_quadraticVariation"}

$$
\begin{align*}
  &\langle M_t, N_t \rangle_E - \langle M, N \rangle_t
  \\
  &= \frac{1}{4}\left( \left(\Vert M_t + N_t \Vert^2 - \langle M+N \rangle_t\right) - \left(\Vert M_t - N_t \Vert^2 - \langle M-N \rangle_t\right) \right)
  \: .
\end{align*}
$$

The two differences are local martingales by [local_martingale_sub_quadraticVariation](#lem:local_martingale_sub_quadraticVariation), so their linear combination is also a local martingale.

## Lemma: covariation_eq_inner {#lem:covariation_eq_inner uses="def:covariation, def:IsSquareIntegrable"}

Let $M$ and $N$ be square integrable martingales. Then

$$
\begin{align*}
  \mathbb{E}\left[\langle M,N \rangle_\infty\right] = \langle M - M_0, N - N_0 \rangle_{\mathcal{M}^2}
  \: .
\end{align*}
$$

## Lemma: quadraticVariation_brownian {#lem:quadraticVariation_brownian uses="def:brownian, def:quadraticVariation"}

Let $B$ be a standard Brownian motion. Then the quadratic variation of $B$ is given by $\langle B \rangle_t = t$ .

**Local martingales**

## Lemma: IsLocalMartingale.locally_hasIntegrableVariation_largeJumps {#lem:IsLocalMartingale.locally_hasIntegrableVariation_largeJumps uses="def:IsLocalMartingale, def:HasIntegrableVariation, def:largeJump"}

The large jump process of a local martingale is a process with locally integrable variation (it's in $(\mathcal{A} \cap \mathcal{M})_{\mathrm{loc}}$).

## Theorem: local_martingale_decomposition {#thm:local_martingale_decomposition uses="def:IsLocalMartingale"}

Let $M$ be a local martingale.
Then for any $\varepsilon > 0$, $M$ can be decomposed as $M = M_0 + U + V$, where $U$ is a locally bounded martingale (local version of both bounded and martingale) with $\vert \Delta U \vert \le \varepsilon$ and $U_0 = 0$ and $V$ is a local martingale with locally integrable variation ($V \in (\mathcal{M} \cap \mathcal{A})_{\mathrm{loc}}$) and $V_0 = 0$.

### Proof {uses="lem:IsLocalMartingale.locally_hasIntegrableVariation_largeJumps"}

See  [@he2019semimartingale], 7.17

Remark:
$U$ is locally bounded, hence locally square integrable, so we can use the integration machinery for those to define an integral.
$V$ has locally integrable variation so we can integrate it with Stieltjes integrals.

**Semimartingales**

## Definition: Semimartingale {#def:IsSemimartingale uses="def:IsLocalMartingale, def:HasFiniteVariation, def:adapted"}

A process $X$ is a semimartingale if it can be decomposed as $X = M + A$, where $M$ is a local martingale ($M \in \mathcal{M}_{\mathrm{loc}}$) and $A$ is an adapted process with finite variation.

TODO: it's adapted and cadlag.

## Lemma: IsSemimartingale.decomposition {#lem:IsSemimartingale.decomposition uses="def:IsSemimartingale"}

A semimartingale $X$ can be decomposed as $X = M + A$, where $M$ is a locally bounded martingale with bounded jumps and $A$ is an adapted process with finite variation.

### Proof {uses="thm:local_martingale_decomposition"}

Decompose $X = M + A$ as in [Semimartingale](#def:IsSemimartingale).
Then decompose $M$ as in [local_martingale_decomposition](#thm:local_martingale_decomposition) with $\varepsilon = 1$.
Then $M = M_0 + U + V$ with $U$ a locally bounded martingale with $\vert \Delta U \vert \le 1$ and $V$ a local martingale with locally integrable variation.
Then $X = (M_0 + U) + (A + V)$, with $U$ a locally bounded martingale with bounded jumps and $A + V$ an adapted process of finite variation (since $V$ has locally integrable variation, hence finite variation).

## Definition: Continuous martingale part {#def:IsSemimartingale.continuousMartingalePart uses="def:IsSemimartingale, lem:IsSemimartingale.decomposition"}

TODO. Denoted by $X^c$.

## Definition: Quadratic covariation of semimartingales {#def:quadCovariation uses="def:IsSemimartingale, def:quadraticVariation, def:IsSemimartingale.continuousMartingalePart"}

Let $X$ and $Y$ be semimartingales. Their quadratic covariation $[X, Y]$ is defined as

$$
\begin{align*}
  [X, Y]_t = X_0 Y_0 + \langle X^c, Y^c \rangle_t + \sum_{0 < s \le t} \Delta X_s \Delta Y_s
  \: .
\end{align*}
$$

TODO: this is an adapted process with finite variation (it's in $\mathcal{V}$).

## Definition: Quadratic variation of a semimartingale {#def:quadVariation uses="def:quadCovariation"}

The quadratic variation of a semimartingale $X$ is defined as $[X] = [X, X]$ .

TODO: $[X]$ is an adapted increasing process.

## Definition: Special semimartingale {#def:IsSpecialSemimartingale uses="def:IsSemimartingale, def:HasIntegrableVariation"}

A semimartingale $X$ is a special semimartingale if it can be decomposed as $X = M + A$, where $M$ is a local martingale and $A$ is an adapted process with locally integrable variation.

## Theorem: IsSpecialSemimartingale.decomposition {#lem:IsSpecialSemimartingale.decomposition uses="def:IsSpecialSemimartingale"}

A special semimartingale $X$ can be decomposed as $X = M + A$, where $M$ is a local martingale and $A$ is a predictable process with finite variation and $A_0 = 0$.

