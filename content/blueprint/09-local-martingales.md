---
title: 'Local martingales'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Local properties**

This section contains material taken mostly from [kallenberg2021, Chapters 10 and 18] and [almostsuremath].

## Definition: preLocalizingSequence {#def:preLocalizingSequence lean="ProbabilityTheory.IsPreLocalizingSequence" uses="def:IsStoppingTime"}

A pre-localizing sequence is a sequence of stopping times $(\tau_n)_{n \in \mathbb{N}}$ such that $\tau_n \to \infty$ as $n \to \infty$ (a.s.).

## Definition: Localizing sequence {#def:localizingSequence lean="ProbabilityTheory.IsLocalizingSequence" uses="def:preLocalizingSequence"}

A localizing sequence is a sequence of stopping times $(\tau_n)_{n \in \mathbb{N}}$ such that $\tau_n$ is non-decreasing and $\tau_n \to \infty$ as $n \to \infty$ (a.s.).
That is, it is a pre-localizing sequence that is also almost surely non-decreasing.

## Lemma: localizingSequence_const_top {#lem:localizingSequence_const_top lean="ProbabilityTheory.isLocalizingSequence_const_top" uses="def:localizingSequence"}

The constant sequence $\tau_n = \infty$ is a localizing sequence.

## Lemma: localizingSequence_min {#lem:localizingSequence_min lean="ProbabilityTheory.IsLocalizingSequence.min" uses="def:localizingSequence"}

Let $(\sigma_n), (\tau_n)$ be localizing sequences.
Then $(\sigma_n \wedge \tau_n)$ is a localizing sequence.

## Lemma: isLocalizingSequence_of_isPreLocalizingSequence {#lem:isLocalizingSequence_of_isPreLocalizingSequence lean="ProbabilityTheory.isLocalizingSequence_of_isPreLocalizingSequence" uses="def:localizingSequence, lem:rightContinuous_basic"}

If $(\tau_n)_{n \in \mathbb{N}}$ is a pre-localizing sequence, then the sequence defined by $\tau'_n = \inf_{m \ge n} \tau_m$ is a localizing sequence.

## Lemma: isPreLocalizingSequence_of_isLocalizingSequence {#lem:isPreLocalizingSequence_of_isLocalizingSequence lean="ProbabilityTheory.isPreLocalizingSequence_of_isLocalizingSequence" uses="def:preLocalizingSequence, def:localizingSequence"}

Let $(\tau_n)_{n \in \mathbb{N}}$ be a localizing sequence and let $(\sigma_{n,k})_{k \in \mathbb{N}}$ be a localizing sequence for each $n$.
Then, there exists a strictly increasing sequence $(k_n)_{n \in \mathbb{N}}$ such that the sequence defined by $\tau'_n = \tau_n \wedge \sigma_{n,k_n}$ is a pre-localizing sequence.

### Proof

For each $n$, since $\sigma_{n,k} \to \infty$ a.s. as $k \to \infty$, we may choose $k_n \in \mathbb{N}$ such that $P(\sigma_{n,k_n} < \tau_n \wedge n) \le 2^{-n}$.
  Then, defining $\tau'_n = \tau_n \wedge \sigma_{n,k_n}$, we have $\tau_n' \to \infty$ by the Borel-Cantelli lemma.

## Lemma: isLocalizingSequence_ae {#lem:isLocalizingSequence_ae lean="ProbabilityTheory.isLocalizingSequence_localizingSequenceOfProp" uses="def:localizingSequence"}

Let $P$ be a predicate on paths and suppose $X$ is a stochastic process satisfying $P$ a.s. Then, defining
  
$$
\tau_n(\omega) =
  \begin{cases}
    \infty & \text{if } X(\omega) \text{ satisfies } P \\
    0 & \text{otherwise}
  \end{cases}
$$

  for all $n \in \mathbb{N}$, the sequence $(\tau_n)_{n \in \mathbb{N}}$ is a localizing sequence.

## Definition: Local property {#def:locally lean="ProbabilityTheory.Locally, ProbabilityTheory.Locally.localSeq" uses="def:localizingSequence, def:stoppedProcess"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $P$ be a class of stochastic processes (or equivalently a predicate on stochastic processes).
We say that a stochastic process $X : T \to \Omega \to E$ is locally in $P$ (or satisfies $P$ locally) if there exists a localizing sequence $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, the process $X^{\tau_n}\mathbb{I}_{\tau_n > 0}$ is in $P$ (in which $X^{\tau_n}$ denotes the stopped process).
We denote the class of processes that are locally in $P$ by $P_{\mathrm{loc}}$.

## Lemma: implies_locally {#lem:implies_locally lean="ProbabilityTheory.Locally.of_prop" uses="def:locally"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For any class of processes $P$, we have $P \subseteq P_{\mathrm{loc}}$.

### Proof {uses="lem:localizingSequence_const_top"}

Take $\tau_n = \infty$ for all $n$.

## Lemma: locally_mono {#lem:locally_mono lean="ProbabilityTheory.Locally.mono" uses="def:locally"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

If $P \subseteq Q$ then $P_{\mathrm{loc}} \subseteq Q_{\mathrm{loc}}$.

### Proof

Let $X \in P_{\mathrm{loc}}$.
Then there exists a localizing sequence $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, $X^{\tau_n}\mathbb{I}_{\tau_n > 0} \in P$.
Since $P \subseteq Q$, for all $n \in \mathbb{N}$, $X^{\tau_n}\mathbb{I}_{\tau_n > 0} \in Q$.
Thus $X \in Q_{\mathrm{loc}}$.

## Definition: stable {#def:stable lean="ProbabilityTheory.IsStable" uses="def:locally"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A class of stochastic processes $P$ is stable if whenever $X$ is in $P$, then for any stopping time $\tau$, the process $X^{\tau}\mathbb{I}_{\tau > 0}$ is also in $P$.

## Lemma: isStable_locally {#lem:isStable_locally lean="ProbabilityTheory.IsStable.locally" uses="def:locally, def:stable"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

If $P$ is a stable class of processes, then $P_{\mathrm{loc}}$ is also stable.

## Lemma: locally_inter {#lem:locally_inter lean="ProbabilityTheory.IsStable.and" uses="def:locally, def:stable"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

If $P, Q$ are stable classes of processes then $(P\cap Q)_{\mathrm{loc}} = P_{\mathrm{loc}}\cap Q_{\mathrm{loc}}$.

### Proof {uses="lem:localizingSequence_min"}

The forward direction is trivial so we only provide proof for the reverse.

Suppose that $X \in P_{\mathrm{loc}}\cap Q_{\mathrm{loc}}$. Then, there exists localizing sequences $(\tau_n)_{n \in \mathbb{N}}$ and $(\sigma_n)_{n \in \mathbb{N}}$ such that $X^{\tau_n} \mathbb{I}_{\tau_n > 0}\in P$ and $X^{\sigma_n} \mathbb{I}_{\sigma_n > 0} \in Q$. Consequently, by the stability of $P$,

$$
X^{\sigma_n \wedge \tau_n} \mathbb{I}_{\sigma_n \wedge \tau_n > 0} = (X^{\tau_n} \mathbb{I}_{\tau_n > 0})^{\sigma_n \wedge \tau_n} \mathbb{I}_{\sigma_n \wedge \tau_n > 0} \in P.
$$

Similarly, by the stability of $Q$, $X^{\sigma_n \wedge \tau_n} \mathbb{I}_{\sigma_n \wedge \tau_n > 0} \in Q$. Thus, as $\sigma_n \wedge \tau_n$ is a localizing sequence by [localizingSequence_min](#lem:localizingSequence_min) and $X^{\sigma_n \wedge \tau_n} \mathbb{I}_{\sigma_n \wedge \tau_n > 0} \in P \cap Q$ for all $n$, it follows that $X \in (P \cap Q)_{\mathrm{loc}}$

## Lemma: locally_of_isPreLocalizingSequence {#lem:locally_of_isPreLocalizingSequence lean="ProbabilityTheory.IsStable.locally_of_isPreLocalizingSequence" uses="def:locally, def:localizingSequence, def:stable, lem:rightContinuous_basic, def:preLocalizingSequence"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $P$ be a stable class of processes and let $(\tau_n)_{n \in \mathbb{N}}$ be a pre-localizing sequence such that for all $n \in \mathbb{N}$, $X^{\tau_n}\mathbb{I}_{\tau_n > 0}$ is in $P$.
If the filtration is right-continuous, then $X$ is locally in $P$.

### Proof {uses="lem:isLocalizingSequence_of_isPreLocalizingSequence"}

Using the localizing sequence defined by [isLocalizingSequence_of_isPreLocalizingSequence](#lem:isLocalizingSequence_of_isPreLocalizingSequence) suffices.

## Lemma: locally_locally {#lem:locally_locally lean="ProbabilityTheory.IsStable.locally_locally_iff" uses="def:locally, def:stable"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Suppose that the filtration is right-continuous.
For any stable class of processes $P$, we have $(P_{\mathrm{loc}})_{\mathrm{loc}} = P_{\mathrm{loc}}$.

### Proof {uses="lem:locally_of_isPreLocalizingSequence, lem:isStable_locally, lem:isPreLocalizingSequence_of_isLocalizingSequence"}

$(P_{\mathrm{loc}})_{\mathrm{loc}} \supseteq P_{\mathrm{loc}}$ by [isStable_locally](#lem:isStable_locally) so we only prove the reverse inclusion.

Let $X$ be a process in $(P_{\mathrm{loc}})_{\mathrm{loc}}$.
By definition there exists a localizing sequence $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, $X^{\tau_n}\mathbb{I}_{\tau_n > 0}$ is in $P_{\mathrm{loc}}$.
By definition of $P_{\mathrm{loc}}$, for each $n$ there exists a localizing sequence $(\sigma_{n,k})_{k \in \mathbb{N}}$ such that for all $k \in \mathbb{N}$, $(X^{\tau_n}\mathbb{I}_{\tau_n > 0})^{\sigma_{n,k}}\mathbb{I}_{\sigma_{n,k} > 0}$ is in $P$.

By [locally_of_isPreLocalizingSequence](#lem:locally_of_isPreLocalizingSequence), it suffices to show that there exists a pre-localizing sequence $(\tau'_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, $X^{\tau'_n}\mathbb{I}_{\tau'_n > 0}$ is in $P$.
Thus, using the localizing sequences $\tau'_n = \tau_n \wedge \sigma_{n, k_n}$ defined by [isPreLocalizingSequence_of_isLocalizingSequence](#lem:isPreLocalizingSequence_of_isLocalizingSequence),
it remains to argue that by stability of $P$, $X^{\tau'_n}\mathbb{I}_{\tau'_n > 0}$ is in $P$ for all $n$.
Indeed, this follows as $X^{\tau'_n}\mathbb{I}_{\tau'_n > 0} = ((X^{\tau_n}\mathbb{I}_{\tau_n > 0})^{\sigma_{n,k_n}}\mathbb{I}_{\sigma_{n,k_n} > 0})^{\tau'_n}\mathbb{I}_{\tau'_n > 0}$ where $(X^{\tau_n}\mathbb{I}_{\tau_n > 0})^{\sigma_{n,k_n}}\mathbb{I}_{\sigma_{n,k_n} > 0}$ is in $P$ by construction and $P$ is stable.

## Lemma: Local implication from global implication {#lem:local_induction lean="ProbabilityTheory.IsStable.locally_induction" uses="def:locally, def:stable"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Suppose that the filtration is right-continuous.
Let $P, Q$ be two classes of stochastic processes such that $P \subseteq Q_{\mathrm{loc}}$ and $Q$ is stable.
Let $X$ be a stochastic process that satisfies $P$ locally.
Then $X$ satisfies $Q$ locally.
In short, if $P$ implies $Q$ locally, then $P$ locally implies $Q$ locally.

### Proof {uses="lem:locally_locally, lem:locally_mono"}

Since $X \in P_{\mathrm{loc}}$, then $X \in (Q_{\mathrm{loc}})_{\mathrm{loc}}$ by assumption and [locally_mono](#lem:locally_mono).
By Lemma [locally_locally](#lem:locally_locally), $(Q_{\mathrm{loc}})_{\mathrm{loc}} = Q_{\mathrm{loc}}$.
Thus $X \in Q_{\mathrm{loc}}$.

**Locally Cadlag**

We in this section assume $\mathcal{F}$ satisfies the usual conditions (i.e. complete and right-continuous).

## Lemma: locally_of_ae {#lem:locally_of_ae lean="ProbabilityTheory.locally_of_ae" uses="def:locally"}

If $P$ be a predicate on paths such that the constant path $0$ satisfies $P$ and $X$ is a stochastic process satisfying $P$ a.s. then, $X$ satisfies $P$ locally.

### Proof {uses="lem:isLocalizingSequence_ae"}

Follows directly by using the localizing sequence defined in [isLocalizingSequence_ae](#lem:isLocalizingSequence_ae).

## Lemma: locally_rightContinuous {#lem:locally_rightContinuous lean="ProbabilityTheory.Locally.rightContinuous" uses="def:locally, def:RightContinuous"}

A stochastic process $X$ is locally right continuous if and only if it is right continuous almost surely.

### Proof {uses="lem:locally_of_ae"}

If $X$ is a.s. right continuous, then it is locally right continuous by [locally_of_ae](#lem:locally_of_ae).

  On the other hand, assuming $X$ is locally right continuous, there exists a localizing sequence
  $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$ and $\omega \in \Omega$, $(X^{\tau_n}\mathbb{I}_{\tau_n > 0})(\omega)$ is right continuous.
  Thus, for almost surely every $\omega$ and any $t \in T$ there exists $N \in \mathbb{N}$ such that $\tau_N(\omega) > t + 1$ (not that the ordering of a.s. and for all is important). Hence, as
  $X_s(\omega) = (X^{\tau_N}\mathbb{I}_{\tau_N > 0})_s(\omega)$ on a neighborhood of $t$, we have that $X(\omega)$ is right continuous at $t$.
  Consequently, as $t$ was arbitrary, $X$ is a.s. right continuous.

## Lemma: locally_leftLimit {#lem:locally_leftLimit lean="ProbabilityTheory.Locally.left_limit" uses="def:locally"}

A stochastic process $X$ has left limits locally if and only if it has left limits almost surely.

### Proof {uses="lem:locally_of_ae"}

Same proof as in [locally_rightContinuous](#lem:locally_rightContinuous).

## Lemma: locally_isCadlag {#lem:locally_isCadlag lean="ProbabilityTheory.Locally.isCadlag" uses="def:locally, def:IsCadlag"}

A stochastic process $X$ is locally cadlag if and only if it is cadlag almost surely.

### Proof {uses="lem:locally_of_ae, lem:locally_rightContinuous, lem:locally_leftLimit"}

The forward direction follows from Lemmas [locally_rightContinuous](#lem:locally_rightContinuous) and [locally_leftLimit](#lem:locally_leftLimit)
  while the reverse direction follows from [locally_of_ae](#lem:locally_of_ae).

## Lemma: isStable_rightContinuous {#lem:isStable_rightContinuous lean="ProbabilityTheory.isStable_rightContinuous" uses="def:stable, def:RightContinuous"}

The class of right continuous processes is stable.

### Proof

Trivial.

## Lemma: isStable_left_limit {#lem:isStable_left_limit lean="ProbabilityTheory.isStable_left_limit" uses="def:stable"}

The class of processes with left limits is stable.

### Proof

Trivial.

## Lemma: isStable_isCadlag {#lem:isStable_isCadlag lean="ProbabilityTheory.isStable_isCadlag" uses="def:stable, def:IsCadlag"}

The class of cadlag processes is stable.

### Proof {uses="lem:isStable_rightContinuous, lem:isStable_left_limit"}

Follows from Lemmas [isStable_rightContinuous](#lem:isStable_rightContinuous) and [isStable_left_limit](#lem:isStable_left_limit).

## Lemma: isStable_isStronglyProgressive {#lem:isStable_isStronglyProgressive lean="ProbabilityTheory.isStable_isStronglyProgressive" uses="def:stable"}

The class of progressively measurable processes is stable.

**Local martingales**

## Definition: Local martingale {#def:IsLocalMartingale lean="ProbabilityTheory.IsLocalMartingale" uses="def:Martingale, def:locally, def:IsCadlag, def:stoppedProcess, def:localizingSequence"}

We say a stochastic process $(M_t)_{t \in T}$ is a local martingale if it is locally a cadlag martingale in the sense of
  [Local property](#def:locally). That is, there exists a localizing sequence $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, the process $M^{\tau_n}\mathbb{I}_{\tau_n > 0}$ is a cadlag martingale.

## Definition: IsLocalSubmartingale {#def:IsLocalSubmartingale lean="ProbabilityTheory.IsLocalSubmartingale" uses="def:Submartingale, def:locally, def:IsCadlag, def:stoppedProcess, def:localizingSequence"}

A stochastic process is a local submartingale if it is locally a cadlag submartingale in the sense of [Local property](#def:locally).
That is, there exists a localizing sequence $(\tau_n)_{n \in \mathbb{N}}$ such that for all $n \in \mathbb{N}$, the process $M^{\tau_n}\mathbb{I}_{\tau_n > 0}$ is a cadlag submartingale.

## Lemma: Martingale.IsLocalMartingale {#lem:Martingale.IsLocalMartingale lean="ProbabilityTheory.Martingale.IsLocalMartingale" uses="def:IsLocalMartingale, def:IsCadlag, def:Martingale"}

Every cadlag martingale is a local martingale.

### Proof {uses="lem:implies_locally"}

This follows from Lemma [implies_locally](#lem:implies_locally).

## Lemma: stable_IsMartingale {#lem:stable_IsMartingale lean="ProbabilityTheory.isStable_martingale" uses="def:Martingale, def:stable, def:IsCadlag"}

The class of cadlag martingales is stable. That is, if $M$ is a cadlag martingale and $\tau$ is a stopping time, then the stopped process cadlag $M^{\tau}\mathbb{I}_{\tau > 0}$ is also a martingale.

### Proof {uses="lem:optionalSampling"}

Clearly, the stopped process $M^{\tau}\mathbb{I}_{\tau > 0}$ is cadlag and it remains to show that it is a martingale.

  Fixing $s \le t \in T$, as $\{\tau > 0\} \in \mathcal{F}_0 \subseteq \mathcal{F}_s$, we have
  
$$
P[M^{\tau}_t \mathbb{I}_{\tau > 0} \mid \mathcal{F}_s] = \mathbb{I}_{\tau > 0}P[M_{\tau \wedge t} \mid \mathcal{F}_{s}].
$$

  Thus, as $\tau \wedge t$ is a bounded stopping time, we have by the optional stopping theorem
  ([Optional sampling (continuous time)](#lem:optionalSampling)) that $P[M_{\tau \wedge t} \mid \mathcal{F}_{s}] = M_{(\tau \wedge t) \wedge s} = M_{\tau \wedge s}$
  and so, $P[M^{\tau}_t \mathbb{I}_{\tau > 0} \mid \mathcal{F}_s] = M^{\tau}_s \mathbb{I}_{\tau > 0}$ as required.

## Lemma: stable_IsSubmartingale {#lem:stable_IsSubmartingale lean="ProbabilityTheory.isStable_submartingale" uses="def:Submartingale, def:stable, def:IsCadlag"}

The class of cadlag submartingales is stable. That is, if $M$ is a cadlag submartingale and $\tau$ is a stopping time, then the stopped process $M^{\tau}\mathbb{I}_{\tau > 0}$ is also a cadlag submartingale.

### Proof {uses="lem:optionalSamplingSubmartingale"}

## Theorem: IsLocalMartingale.eq_zero_of_finiteVariation {#thm:IsLocalMartingale.eq_zero_of_finiteVariation uses="def:IsLocalMartingale"}

Let $M$ be a continuous local martingale with $M_0 = 0$. If $M$ is also a finite variation process, then $M_t = 0$ for all $t$.

**Doob-Meyer class**

## Definition: Integrable supremum {#def:HasIntegrableSup lean="ProbabilityTheory.HasIntegrableSup"}

We say that a stochastic process is integrable if the map $(t,\omega) \mapsto X_t(\omega)$ is strongly measurable and for all $t$, $X_t$ is integrable.
A process has an integrable supremum if $(\sup_{s \le t} \Vert X_s \Vert)_t$ is integrable.

## Definition: Locally integrable supremum {#def:locallyIntegrableSup lean="ProbabilityTheory.HasLocallyIntegrableSup" uses="def:locally, def:HasIntegrableSup"}

A process has locally integrable supremum if it is locally a process with integrable supremum.

## Definition: Doob-Meyer class, class D {#def:classD lean="ProbabilityTheory.ClassD" uses="def:IsStoppingTime"}

A stochastic process $(X_t)$ is of class D (or in the Doob-Meyer class) if it is progressively measurable and the set $\{X_\tau \mid \tau \text{ is a finite stopping time}\}$ is uniformly integrable.

## Definition: Class DL {#def:classDL lean="ProbabilityTheory.ClassDL" uses="def:IsStoppingTime"}

A stochastic process $(X_t)$ is of class DL if it is progressively measurable and for all $t \ge 0$, the set $\{X_\tau \mid \tau \text{ is a stopping time with } \tau \le t\}$ is uniformly integrable.

## Lemma: classDLOfClassD {#lem:classDLOfClassD lean="ProbabilityTheory.ClassD.classDL" uses="def:classD, def:classDL"}

A stochastic process of class D is of class DL.

### Proof {uses="def:classD, def:classDL, lem:uniformIntegrableComp"}

This follows from the definitions and [uniformIntegrableComp](#lem:uniformIntegrableComp).

## Lemma: ClassD.uniformIntegrable {#lem:ClassD.uniformIntegrable lean="ProbabilityTheory.ClassD.uniformIntegrable'" uses="def:classD"}

A stochastic process of class D is uniformly integrable.

### Proof {uses="def:classD, lem:uniformIntegrableComp"}

Use the Class D property with the constant stopping times $\tau_n = n$ for all $n$ and apply [uniformIntegrableComp](#lem:uniformIntegrableComp).

## Lemma: classDL_iff_norm {#lem:classDL_iff_norm lean="ProbabilityTheory.classDL_iff_norm" uses="def:classDL"}

A progressively measurable process is of class DL iff its norm is of class DL.

### Proof {uses="def:classDL, lem:uniformIntegrableIffNorm"}

## Lemma: classD_of_uniformIntegrable_bounded_stoppingTime {#lem:classD_of_uniformIntegrable_bounded_stoppingTime lean="ProbabilityTheory.classD_of_uniformIntegrable_bounded_stoppingTime" uses="def:classD"}

If a stochastic process is progressively measurable and the set

$$
\begin{align*}
  \{X_\tau \mid \tau \text{ is a stopping time and } \exists t, \forall \omega, \tau(\omega) \le t\}
\end{align*}
$$

is uniformly integrable, then the process is of class D.

### Proof {uses="def:classD, lem:uniformIntegrableComp"}

## Lemma: classD_iff_norm {#lem:classD_iff_norm lean="ProbabilityTheory.classD_iff_norm" uses="def:classD"}

A progressively measurable process is of class D iff its norm is of class D.

### Proof {uses="def:classD, lem:uniformIntegrableIffNorm, lem:classD_of_uniformIntegrable_bounded_stoppingTime"}

## Lemma: Submartingale.classDL {#lem:Submartingale.classDL lean="MeasureTheory.Submartingale.classDL" uses="def:Submartingale, def:classDL, def:RightContinuous"}

Every nonnegative right-continuous submartingale is of class DL.

### Proof {uses="lem:optionalSamplingSubmartingale, lem:uniformIntegrableDominated, lem:condExpUI"}

Let $t \in T$ and $\tau \le t$ be a stopping time. By [optionalSamplingSubmartingale](#lem:optionalSamplingSubmartingale) and nonnegativity we get that $0 \le X_\tau \le P[X_t \mid X_\tau]$. As $X$ is a submartingale, $X_t$ is integrable, thus $\{X_t\}$ is uniformly integrable, and we can conclude from [uniformIntegrableDominated](#lem:uniformIntegrableDominated) and [condExpUI](#lem:condExpUI).

## Lemma: Submartingale.classD_iff_uniformIntegrable {#lem:Submartingale.classD_iff_uniformIntegrable lean="MeasureTheory.Submartingale.classD_iff_uniformIntegrable" uses="def:Submartingale, def:classD, def:RightContinuous"}

A nonnegative right-continuous submartingale is of class D if and only if it is uniformly integrable.

### Proof {uses="lem:optionalSamplingSubmartingale, lem:uniformIntegrable_of_tendsto_ae, lem:uniformIntegrableComp, lem:ClassD.uniformIntegrable"}

Assume that $X$ is uniformly integrable. Just like what we did in the proof of [Submartingale.classDL](#lem:Submartingale.classDL), we use [optionalSamplingSubmartingale](#lem:optionalSamplingSubmartingale) and [condExpUI](#lem:condExpUI) to deduce that $\{X_\tau|\exists t\in T, \tau\le t\}$ is uniformly integrable. Moreover, for any finite stopping time $\tau$, We have that $X_\tau = \lim_{n \to +\infty} X_{\tau \land n}$. Thanks to [uniformIntegrable_of_tendsto_ae](#lem:uniformIntegrable_of_tendsto_ae), we deduce that $X$ is of class D.

Conversely, if $X$ is of class D, then it is uniformly integrable by [ClassD.uniformIntegrable](#lem:ClassD.uniformIntegrable).

## Lemma: Martingale.classDL {#lem:Martingale.classDL lean="MeasureTheory.Martingale.classDL" uses="def:Martingale, def:classDL, def:IsCadlag"}

Every càdlàg martingale is of class DL.

### Proof {uses="lem:Submartingale.classDL, lem:Martingale.submartingale_convex_comp, lem:uniformIntegrableIffNorm"}

Let $X$ be càdlàg martingale. By [Martingale.submartingale_convex_comp](#lem:Martingale.submartingale_convex_comp), $(|X_t|)_{t \in T}$ is a nonnegative càdlàg submartingale, and the result follows from [Submartingale.classDL](#lem:Submartingale.classDL) along with [uniformIntegrableIffNorm](#lem:uniformIntegrableIffNorm).

## Lemma: Martingale.classD_iff_uniformIntegrable {#lem:Martingale.classD_iff_uniformIntegrable lean="MeasureTheory.Martingale.classD_iff_uniformIntegrable" uses="def:Martingale, def:classD, def:RightContinuous"}

A right-continuous martingale is of class D if and only if it is uniformly integrable.

### Proof {uses="lem:Submartingale.classD_iff_uniformIntegrable, lem:uniformIntegrableIffNorm, lem:classD_iff_norm, cor:Martingale.submartingale_norm"}

Applying [classD_iff_norm](#lem:classD_iff_norm) and [uniformIntegrableIffNorm](#lem:uniformIntegrableIffNorm), it suffices to show the result for the norm of the martingale.
That norm is a nonnegative right-continuous submartingale by [Martingale.submartingale_norm](#cor:Martingale.submartingale_norm) so this follows from [Submartingale.classD_iff_uniformIntegrable](#lem:Submartingale.classD_iff_uniformIntegrable).

## Lemma: isStable_stronglyMeasurable_uncurry {#lem:isStable_stronglyMeasurable_uncurry lean="ProbabilityTheory.isStable_stronglyMeasurable_uncurry" uses="def:stable"}

The class of processes for which the induced map $(t,\omega)\mapsto X_t(\omega)$ is strongly measurable is stable.

### Proof

The stopped process at $\tau$ is obtained by precomposition with $(t, \omega) \mapsto (\min (\tau(\omega), t), \omega)$.
Precomposing a strongly measurable function with a measurable function gives a strongly measurable function.
On a second-countable space, the minimum of two functions is measurable, and by assumption $\tau$ is measurable.
The result follows from this.

## Lemma: isStable_hasIntegrableSup {#lem:isStable_hasIntegrableSup lean="ProbabilityTheory.isStable_hasIntegrableSup" uses="def:stable, def:HasIntegrableSup"}

The class of process with integrable supremum is stable.

### Proof

Let $X$ be a process with integrable supremum and $\tau$ be a stopping time. Let $t \in T$. Then $(X^\tau)^*_t = \sup_{s \le t} \|X_{\tau \land s}\| \le \sup_{s \le t} \|X_s\| = X^*_t$, and as $X^*_t$ is integrable, so is $(X^\tau)^*_t$. Thus $(X^\tau \mathbb{I}_{\tau > 0})^*_t$ is integrable, concluding the proof.

## Lemma: isStable_hasLocallyIntegrableSup {#lem:isStable_hasLocallyIntegrableSup lean="ProbabilityTheory.isStable_hasLocallyIntegrableSup" uses="def:stable, def:locallyIntegrableSup"}

The class of process with locally integrable supremum is stable.

### Proof {uses="lem:isStable_hasIntegrableSup, lem:isStable_locally"}

Apply [isStable_hasIntegrableSup](#lem:isStable_hasIntegrableSup) and [isStable_locally](#lem:isStable_locally).

## Lemma: isStable_classD {#lem:isStable_classD lean="ProbabilityTheory.isStable_classD" uses="def:stable, def:classD"}

The class D is stable.

### Proof {uses="lem:uniformIntegrableComp, lem:uniformIntegrableDominated, lem:isStable_isStronglyProgressive"}

Let $X$ be a process of class D and $\tau$ be a stopping time. For any finite stopping time $\sigma$, we have that $X_\sigma^\tau = X_{\sigma \land \tau}$. Because $\sigma \land \tau$ is finite and $X$ is of class D, we deduce from [uniformIntegrableComp](#lem:uniformIntegrableComp) that $\{X_{\sigma \land \tau} \mid \sigma \text{ is a finite stopping time}\}$ is uniformly integrable, and thus that $\{X^\tau_\sigma \mid \sigma \text{ is a finite stopping time}\}$ is uniformly integrable. Using [uniformIntegrableDominated](#lem:uniformIntegrableDominated), we obtain that $\{X^\tau_\sigma \mathbb{I}_{\tau > 0} \mid \sigma \text{ is a finite stopping time}\}$ is uniformly integrable, which concludes the proof.

## Lemma: isStable_classDL {#lem:isStable_classDL lean="ProbabilityTheory.isStable_classDL" uses="def:stable, def:classDL"}

The class DL is stable.

### Proof {uses="lem:uniformIntegrableComp, lem:uniformIntegrableDominated, lem:isStable_isStronglyProgressive"}

Let $X$ be a process of class DL, $\tau$ be a stopping time. Let $t \in T$. For any stopping time $\sigma \le t$, we have that $X_\sigma^\tau = X_{\sigma \land \tau}$. Because $\sigma \land \tau$ is bounded by $t$ and $X$ is of class DL, we deduce from [uniformIntegrableComp](#lem:uniformIntegrableComp) that $\{X_{\sigma \land \tau} \mid \sigma \text{ is a stopping time with } \sigma \le t\}$ is uniformly integrable, and thus that $\{X^\tau_\sigma \mid \sigma \text{ is a stopping time with } \sigma \le t\}$ is uniformly integrable. Using [uniformIntegrableDominated](#lem:uniformIntegrableDominated), we obtain that $\{X^\tau_\sigma \mathbb{I}_{\tau > 0} \mid \sigma \text{ is a stopping time with } \sigma \le t\}$ is uniformly integrable, which concludes the proof.

## Lemma: Integrable.classDL {#lem:Integrable.classDL lean="MeasureTheory.Integrable.classDL" uses="def:classDL, def:HasIntegrableSup"}

Let $X$ be a progressively measurable stochastic process with integrable supremum ([Integrable supremum](#def:HasIntegrableSup)). Then $X$ is of class DL.

### Proof {uses="lem:uniformIntegrableDominatedSingleton"}

Let $t \in T$. For every stopping time $\tau$ with $\tau \le t$, we have $\|X_\tau\| \le X^*_t$.
Measurability of $X_\tau$ follows from progressive measurability of $X$.
Because by hypothesis $X^*_t$ is integrable, we deduce from [uniformIntegrableDominatedSingleton](#lem:uniformIntegrableDominatedSingleton) that $\{X_\tau \mid \tau \text{ is a stopping time with } \tau \le t\}$ is uniformly integrable.
This proves that $X$ is of class DL.

## Lemma: IsStronglyProgressive.hasStronglyMeasurableSup {#lem:IsStronglyProgressive.hasStronglyMeasurableSup lean="MeasureTheory.IsStronglyProgressive.hasStronglyMeasurableSupProcess" uses="def:IsStronglyProgressive"}

If the filtration satisfies the usual conditions, a progressively measurable process has a supremum that is jointly strongly measurable.

### Proof {uses="lem:isStoppingTime_leastGT"}

## Lemma: HasLocallyIntegrableSup.locally_classDL {#lem:HasLocallyIntegrableSup.locally_classDL lean="ProbabilityTheory.HasLocallyIntegrableSup.locally_classDL" uses="def:locallyIntegrableSup, def:locally, def:classDL, def:rightContinuous"}

Let $X$ be a progressively measurable stochastic process with locally integrable supremum. Then $X$ is locally of class DL.

### Proof {uses="lem:Integrable.classDL, lem:locally_mono, lem:isStable_isStronglyProgressive"}

Combine [Integrable.classDL](#lem:Integrable.classDL) and [locally_mono](#lem:locally_mono). Use [isStable_isStronglyProgressive](#lem:isStable_isStronglyProgressive) to get progressive measurability of the stopped processes.

## Lemma: ClassDL.locally_classD {#lem:ClassDL.locally_classD lean="ProbabilityTheory.ClassDL.locally_classD" uses="def:classDL, def:locally, def:classD"}

If $X$ is of class DL then it is locally of class D.

### Proof {uses="lem:uniformIntegrableComp, lem:uniformIntegrableDominated"}

Take $\tau_n := n$. Then

$$
\begin{align*}
  \{X^{\tau_n}_\sigma \mid \sigma \text{ is a finite stopping time}\} & = \{X_{\sigma \land n} \mid \sigma \text{ is a finite stopping time}\} \\
  & \subseteq \{X_\sigma \mid \sigma \text{ is a stopping time with } \sigma \le n\}.
\end{align*}
$$

Because $X$ is of class DL, that last set is uniformly integrable, thus

$$
\{X^{\tau_n}_\sigma \mid \sigma \text{ is a finite stopping time}\}
$$

is uniformly integrable thanks to [uniformIntegrableComp](#lem:uniformIntegrableComp). [uniformIntegrableDominated](#lem:uniformIntegrableDominated) allows to conclude that

$$
\{X^{\tau_n}_\sigma \mathbb{I}_{\tau_n > 0} \mid \sigma \text{ is a finite stopping time}\}
$$

is uniformly integrable, thus $X^{\tau_n} \mathbb{I}_{\tau_n > 0}$ is of class D. Obviously $\tau_n \rightarrow +\infty$ as $n$ goes to infinity, so $X$ is locally of class D.

## Lemma: locally_classD_of_locally_classDL {#lem:locally_classD_of_locally_classDL lean="ProbabilityTheory.locally_classD_of_locally_classDL" uses="def:rightContinuous, def:locally, def:classD, def:classDL"}

If the filtration is right-continuous and $X$ is locally of class DL then it is locally of class D.

### Proof {uses="lem:local_induction, lem:ClassDL.locally_classD, lem:isStable_classD"}

Apply [Local implication from global implication](#lem:local_induction) using [ClassDL.locally_classD](#lem:ClassDL.locally_classD) and [isStable_classD](#lem:isStable_classD).

## Lemma: isBounded_image_of_isCadlag_of_isCompact {#lem:isBounded_image_of_isCadlag_of_isCompact lean="isBounded_image_of_isCadlag_of_isCompact" uses="def:IsCadlag"}

Assume $T$ is a linear order endowed with a topology making it first countable and $E$ is a pseudo-metric space. If $X$ is a càdlàg process then it maps compact sets of $T$ to bounded sets.

### Proof

Let $K \subseteq T$ be a compact set and $\omega \in \Omega$. Assume that $X(\omega)(K)$ is not bounded. Then there exists a sequence $(t_n)$ in $K$ such that for all $n \in N$, $d(X_{t_n}(\omega), x) \ge n$, for some arbitrary $x \in E$. Because $K$ is compact, there is a subsequence $(t_{\phi(n)})$ that converges. Then one can extract a subsequence $(t_{\phi(\psi(n))})$ which either converges from below or from above. In both cases the sequence $(X_{t_{\phi(\psi(n))}})$ will converge, contradicting the hypotheses.

TODO: refine the hypotheses with those of Début theorem.

## Lemma: isLocalizingSequence_leastGE {#lem:isLocalizingSequence_leastGE lean="ProbabilityTheory.isLocalizingSequence_leastGE" uses="def:leastGE, def:localizingSequence, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact, and that the filtration is right-continuous.
If $X$ is a real-valued càdlàg and adapted process, then the sequence $\tau_n := \inf \{t | X_t \ge n\}$ is a localizing sequence.

### Proof {uses="lem:isBounded_image_of_isCadlag_of_isCompact, cor:isStoppingTime_leastGE_of_rightContinuous"}

By [isStoppingTime_leastGE_of_rightContinuous](#cor:isStoppingTime_leastGE_of_rightContinuous), each $\tau_n$ is a stopping time. Moreover, for all $n \in \mathbb{N}$, $X_t \ge n+1 \implies X_t \ge n$, thus $\tau_n \le \tau_{n+1}$. Finally, for every $\omega \in \Omega$ and $t_0 \in T$ there exists $N \in \mathbb{N}$ such that for all $s \le t_0$, $X_s \le N$ thanks to [isBounded_image_of_isCadlag_of_isCompact](#lem:isBounded_image_of_isCadlag_of_isCompact). Thus for all $n \ge N$, $\tau_n(\omega) \ge t_0$, proving that $\tau_n$ tends to infinity as n goes to infinity.

## Lemma: sup_stoppedProcess_le {#lem:sup_stoppedProcess_le lean="ProbabilityTheory.sup_stoppedProcess_leastGE_le" uses="def:stoppedProcess"}

For $Y$ a stochastic process, let $Y^*_t = \sup_{s \le t} \Vert Y_s \Vert$.
Let $X$ be a stochastic process and let $\tau = \inf \{t \mid \Vert X_t \Vert \ge n\}$ for some $n \in \mathbb{R}$.
Then

$$
\begin{align*}
  (X^{\tau})^*_t
  \le n + \mathbb{1}_{\tau \le t} \Vert X_{\tau} \Vert
  \: .
\end{align*}
$$

### Proof

If $\tau > t$, then for all $s \le t$, $\|X_s\| \le n$, and thus $(X^\tau)^*_t = \sup_{s \le t} \|X_{\tau \land s}\| \le n = n + \mathbb{1}_{\tau \le t} \|X_{\tau}\|$. Otherwise $(X^\tau)^*_t = \sup_{s \le \tau} \|X_s\|$. For $s < \tau$, $\|X_s\| \le n$, and $\|X_\tau\| \le \|X_\tau\|$ so $\sup_{s \le \tau} \|X_s\| \le n \lor \|X_\tau\| \le n + \|X_\tau\| = n + \mathbb{I}_{\tau \le t} \|X_\tau\|$.

## Lemma: ClassDL.hasLocallyIntegrableSup {#lem:ClassDL.hasLocallyIntegrableSup lean="ProbabilityTheory.ClassDL.hasLocallyIntegrableSup" uses="def:classD, def:locallyIntegrableSup, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact, and that the filtration is right-continuous.
If $X$ is a càdlàg process of class DL, then it has locally integrable supremum.

### Proof {uses="lem:isLocalizingSequence_leastGE, lem:sup_stoppedProcess_le, lem:IsStronglyProgressive.hasStronglyMeasurableSup"}

Set $\tau_n := \inf \{t | X_t \ge n\}$. This is a localizing sequence by [isLocalizingSequence_leastGE](#lem:isLocalizingSequence_leastGE). For every $t \in T$, we have by [sup_stoppedProcess_le](#lem:sup_stoppedProcess_le) that $(X^{\tau_n})^*_t \le n + \mathbb{I}_{\tau_n \le t} \|X_{\tau_n}\| = n + \mathbb{I}_{\tau_n \le t} \|X_{\tau_n \land t}\|$. Because X is of class DL, $X_{\tau_n \land t}$ is integrable, so $(X^{\tau_n})^*_t$ is integrable too, so $(X^{\tau_n} \mathbb{I}_{\tau_n > 0})^*_t$ is integrable. Thus $X$ has locally integrable supremum.

## Lemma: hasLocallyIntegrableSup_of_locally_classDL {#lem:hasLocallyIntegrableSup_of_locally_classDL lean="ProbabilityTheory.hasLocallyIntegrableSup_of_locally_classDL" uses="def:classDL, def:locallyIntegrableSup, def:locally, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact.
Assume that the filtration is right-continuous.
If a process is càdlàg and locally of class DL, then it has locally integrable supremum.

### Proof {uses="lem:local_induction, lem:ClassDL.hasLocallyIntegrableSup, lem:isStable_hasIntegrableSup"}

Apply [Local implication from global implication](#lem:local_induction) using [ClassDL.hasLocallyIntegrableSup](#lem:ClassDL.hasLocallyIntegrableSup) and [isStable_hasIntegrableSup](#lem:isStable_hasIntegrableSup).

## Lemma: locally_classDL_iff_locallyIntegrableSup {#lem:locally_classDL_iff_locallyIntegrableSup lean="ProbabilityTheory.locally_classDL_iff_hasLocallyIntegrableSup" uses="def:classDL, def:locallyIntegrableSup, def:locally, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact, and that the filtration is right-continuous.
If $X$ is a càdlàg process, then it is locally of class DL if and only if it has locally integrable supremum.

### Proof {uses="lem:hasLocallyIntegrableSup_of_locally_classDL, lem:HasLocallyIntegrableSup.locally_classDL"}

The two directions are proved in Lemmas [hasLocallyIntegrableSup_of_locally_classDL](#lem:hasLocallyIntegrableSup_of_locally_classDL) and [HasLocallyIntegrableSup.locally_classDL](#lem:HasLocallyIntegrableSup.locally_classDL).

## Lemma: locally_classD_iff_locally_classDL {#lem:locally_classD_iff_locally_classDL lean="ProbabilityTheory.locally_classD_iff_locally_classDL" uses="def:classD, def:classDL, def:locally, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact, and that the filtration is right-continuous.
A càdlàg process is locally of class D if and only if it is locally of class DL.

### Proof {uses="lem:locally_classD_of_locally_classDL, lem:classDLOfClassD, lem:locally_mono"}

The forward direction follows from [classDLOfClassD](#lem:classDLOfClassD) along with [locally_mono](#lem:locally_mono).
The reverse direction is [locally_classD_of_locally_classDL](#lem:locally_classD_of_locally_classDL).

## Lemma: locally_classD_iff_locallyIntegrableSup {#lem:locally_classD_iff_locallyIntegrableSup lean="ProbabilityTheory.locally_classD_iff_hasLocallyIntegrableSup" uses="def:classD, def:locallyIntegrableSup, def:locally, def:IsCadlag, def:rightContinuous"}

Assume $T$ has a bottom element and that its closed intervals are compact, and that the filtration is right-continuous.
A càdlàg process is locally of class D if and only if it has locally integrable supremum.

### Proof {uses="lem:locally_classD_iff_locally_classDL, lem:locally_classDL_iff_locallyIntegrableSup"}

This follows from Lemmas [locally_classD_iff_locally_classDL](#lem:locally_classD_iff_locally_classDL) and [locally_classDL_iff_locallyIntegrableSup](#lem:locally_classDL_iff_locallyIntegrableSup).

## Lemma: Submartingale.locallyIntegrableSup {#lem:Submartingale.locallyIntegrableSup uses="def:Submartingale, def:locallyIntegrableSup, def:IsCadlag, def:rightContinuous"}

Every cadlag submartingale for a right-continuous filtration has locally integrable supremum.

### Proof {uses="lem:sup_stoppedProcess_le, lem:Submartingale.integrable_stoppedValue, cor:isStoppingTime_leastGE_of_rightContinuous"}

Define the stopping times $\sigma_n = \inf\{t \mid \Vert X_t \Vert \ge n\}$ and set $\tau_n = \sigma_n \wedge n$.
$\sigma_n$ is a stopping time by [isStoppingTime_leastGE_of_rightContinuous](#cor:isStoppingTime_leastGE_of_rightContinuous) and so $\tau_n$ is also a stopping time.
The times $(\tau_n)_{n \in \mathbb{N}}$ form a localizing sequence.
By [sup_stoppedProcess_le](#lem:sup_stoppedProcess_le), we have that

$$
\begin{align*}
  (X^{\tau_n})^*_t
  & \le n + \mathbb{1}_{\tau_n \le t} \Vert X_{\tau_n} \Vert \\
  & \le n + \Vert X_{\tau_n} \Vert
  \: .
\end{align*}
$$

It remains to show that $X_{\tau_n}$ is integrable for each $n$.
This follows by [Submartingale.integrable_stoppedValue](#lem:Submartingale.integrable_stoppedValue) as $\tau_n$ is a bounded stopping time.

## Lemma: Submartingale.locally_classD {#lem:Submartingale.locally_classD lean="MeasureTheory.Submartingale.locally_classD" uses="def:Submartingale, def:classD, def:locally, def:IsCadlag"}

Every cadlag submartingale is locally of class D.

### Proof {uses="lem:Submartingale.classDL, lem:locally_classD_iff_locally_classDL"}

By [locally_classD_iff_locally_classDL](#lem:locally_classD_iff_locally_classDL), it suffices to show that every cadlag submartingale is locally of class DL.
This can be proved with [Submartingale.classDL](#lem:Submartingale.classDL).

## Lemma: IsLocalSubmartingale.locally_classD {#lem:IsLocalSubmartingale.locally_classD lean="ProbabilityTheory.IsLocalSubmartingale.locally_classD" uses="def:IsLocalSubmartingale, def:classD, def:locally"}

Every local submartingale is locally of class D.

### Proof {uses="lem:local_induction, lem:stable_IsSubmartingale, lem:Submartingale.locally_classD, lem:isStable_classD"}

By [Local implication from global implication](#lem:local_induction), it suffices to show that if $X$ is a submartingale then it is locally of class D.
This is done in [Submartingale.locally_classD](#lem:Submartingale.locally_classD).

## Lemma: IsLocalMartingale.locally_classD {#lem:IsLocalMartingale.locally_classD uses="def:IsLocalMartingale, def:classD, def:locally"}

Every local martingale is locally of class D.

## Lemma: IsLocalMartingale.martingale_iff_classDL {#lem:IsLocalMartingale.martingale_iff_classDL uses="def:IsLocalMartingale, def:classDL, def:Martingale, def:IsCadlag"}

A local martingale is a cadlag martingale if and only if it is of class DL.

## Lemma: IsLocalSubmartingale.submartingale_iff_classDL_of_nonnegative {#lem:IsLocalSubmartingale.submartingale_iff_classDL_of_nonnegative uses="def:IsLocalSubmartingale, def:classDL, def:Submartingale, def:IsCadlag"}

A nonnegative local submartingale is a cadlag submartingale if and only if it is of class DL.

