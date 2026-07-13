---
title: 'Modifications with cadlag paths'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Cadlag modifications of martingales**

**Stochastic intervals**

## Definition: Stochastic intervals {#def:stochasticInterval lean="ProbabilityTheory.stochIcc, ProbabilityTheory.stochIco, ProbabilityTheory.stochIoc, ProbabilityTheory.stochIoo, ProbabilityTheory.stochGraph"}

Let $T$ be a time domain and let $\sigma, \tau$ be functions $\Omega \to T \cup \{\infty\}$.
We define

$$
\begin{align*}
  [\![\sigma, \tau]\!]
  &= \{(t, \omega) \in T \times \Omega \mid \sigma(\omega) \le t \le \tau(\omega)\}
  \:, \\
  [\![\sigma, \tau[\![
  &= \{(t, \omega) \in T \times \Omega \mid \sigma(\omega) \le t < \tau(\omega)\}
  \:, \\
  ]\!]\sigma, \tau]\!]
  &= \{(t, \omega) \in T \times \Omega \mid \sigma(\omega) < t \le \tau(\omega)\}
  \:, \\
  ]\!]\sigma, \tau[\![
  &= \{(t, \omega) \in T \times \Omega \mid \sigma(\omega) < t < \tau(\omega)\}
  \:, \\
  [\![\sigma]\!]
  &= \{(t, \omega) \in T \times \Omega \mid \sigma(\omega) = t\} = [\![\sigma, \sigma]\!]
  \:.
\end{align*}
$$

We call those stochastic intervals. Note that these are subsets of $T \times \Omega$, not of $ (T \cup \{\infty\}) \times \Omega$.
$[\![\sigma]\!]$ is called the graph of $\sigma$.

## Lemma: predictable_stochasticInterval {#lem:predictable_stochasticInterval uses="def:IsStoppingTime, def:stochasticInterval, def:predictable"}

If $\sigma$ and $\tau$ are stopping times, then the stochastic interval $]\!]\sigma, \tau]\!]$ is a predictable set.

## Lemma: elementaryPredictableSet_stochasticInterval {#lem:elementaryPredictableSet_stochasticInterval lean="ProbabilityTheory.stochIoc.exists_elementaryPredictableSet" uses="def:stochasticInterval, def:elementaryPredictableSet, def:IsStoppingTime"}

If $\sigma$ and $\tau$ are stopping times on $\mathbb{N}$, with $\tau$ bounded, then the stochastic interval $]\!]\sigma, \tau]\!]$ is an elementary predictable set.

### Proof

Let $n$ be an upper bound for $\tau$.
To see that the stochastic interval is an elementary predictable set, note that it can be written as a finite disjoint union of sets

$$
\begin{align*}
  \{\sigma(\omega) < t \le \tau(\omega)\}
  &= \bigcup_{k=1}^{n} \{k\} \times \{\sigma < k \le \tau\}
  \\ &= \bigcup_{k=1}^{n} (k-1, k] \times \{\sigma \le k-1 < \tau\}
\end{align*}
$$

where $\{\sigma \le k-1 < \tau\} \in \mathcal{F}_{k-1}$.
Therefore this is an elementary predictable set.

**Upcrossings**

## Definition: lowerCrossingTimeAux {#def:lowerCrossingTimeAux lean="MeasureTheory.lowerCrossingTimeAux" uses="def:hittingBtwn"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X : T \to \Omega \to \mathbb{R}$ be a stochastic process, $t \in T$, and $a, b \in \mathbb{R}$.
The auxiliary lower crossing time $\sigma'_{a, s, t}$ is the hitting time of the set $(-\infty, a]$ by the process $X$ between times $s$ and $t$.

## Definition: Upper crossing time {#def:upperCrossingTime lean="MeasureTheory.upperCrossingTime" uses="def:lowerCrossingTimeAux"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X : T \to \Omega \to \mathbb{R}$ be a stochastic process, $t \in T$, and $a, b \in \mathbb{R}$.
The $n$-th upper crossing time $\tau^n_{a, b, t}$ of the interval $[a, b]$ by $X$ before time $t$ is the hitting time of the set $[b, \infty)$ by $X$ after hitting the set $(-\infty, a]$ for the $n-1$-th time.

That is, $\tau^0_{a, b, t} = 0$, and for all $n$, $\tau^{n+1}_{a, b, t}$ is the hitting time of $[b, \infty)$ by $X$ between $\sigma'_{a, \tau^{n}_{a, b, t}, t}$ and $t$.

## Definition: Lower crossing time {#def:lowerCrossingTime lean="MeasureTheory.lowerCrossingTime" uses="def:upperCrossingTime"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X : T \to \Omega \to \mathbb{R}$ be a stochastic process, $t \in T$, and $a, b \in \mathbb{R}$.
The $n$-th lower crossing time $\sigma^n_{a, b, t}$ of the interval $[a, b]$ by $X$ before time $t$ is the hitting time of the set $(-\infty, a]$ by $X$ after hitting the set $[b, \infty)$ for the $n$-th time.

That is, it is the hitting time of $(-\infty, a]$ by $X$ between $\tau^n_{a, b, t}$ and $t$.

## Definition: Upcrossings before time $t$ {#def:upcrossingsBefore lean="MeasureTheory.upcrossingsBefore" uses="def:upperCrossingTime"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X : T \to \Omega \to \mathbb{R}$ be a stochastic process, $t \in T$, and $a, b \in \mathbb{R}$.
The number of upcrossings $U_t[a, b]$ of the interval $[a, b]$ by $X$ before time $t$ is the largest $n$ such that $\tau^n_{a, b, t} < t$, or $\infty$ if there is no such largest $n$.

## Definition: Upcrossings {#def:upcrossings lean="MeasureTheory.upcrossings" uses="def:upcrossingsBefore"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X : T \to \Omega \to \mathbb{R}$ be a stochastic process and $a, b \in \mathbb{R}$.
The number of upcrossings $U[a, b]$ of the interval $[a, b]$ by $X$ is the supremum over $t \in T$ of the number of upcrossings $U_t[a, b]$ of $[a, b]$ by $X$ before time $t$.

## Lemma: tendsto_of_no_upcrossings {#lem:tendsto_of_no_upcrossings lean="tendsto_of_no_upcrossings" uses="def:upcrossings"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $u : \beta \to \alpha$, for $\alpha$ a densely ordered, conditionally complete linear order equipped with the order topology.
Let $S$ be a dense subset of $\alpha$ and $f$ a filter of $\beta$.
If for all $a < b$ in $S$, the number of upcrossings of the interval $[a, b]$ by $u$ along $f$ is finite, then $u$ tends to a limit along $f$.

## Lemma: isStoppingTime_upperCrossingTime {#lem:isStoppingTime_upperCrossingTime uses="def:upperCrossingTime, def:IsStoppingTime, def:adapted"}

For an adapted process $X : \mathbb{N} \to \Omega \to \mathbb{R}$ indexed by the natural numbers, the upper crossing time $\tau^n_{a, b, t}$ is a stopping time.

### Proof {uses="lem:isStoppingTime_hittingBtwn"}

## Lemma: isStoppingTime_lowerCrossingTime {#lem:isStoppingTime_lowerCrossingTime uses="def:lowerCrossingTime, def:IsStoppingTime, def:adapted"}

For an adapted process $X : \mathbb{N} \to \Omega \to \mathbb{R}$ indexed by the natural numbers, the lower crossing time $\sigma^n_{a, b, t}$ is a stopping time.

### Proof {uses="lem:isStoppingTime_hittingBtwn, lem:isStoppingTime_upperCrossingTime"}

## Definition: upcrossingPredictableSet {#def:upcrossingPredictableSet uses="def:upcrossings, def:upperCrossingTime, def:lowerCrossingTime, def:adapted"}

Let $X : \mathbb{N} \to \Omega \to \mathbb{R}$ be an adapted process on the natural numbers.
The upcrossing predictable set of $X$ before time $N$ is the predictable set defined by

$$
\begin{align*}
  A_N = \bigcup_{k=0}^{N-1} ]\!]\sigma^k_{a, b, N}, \tau^{k+1}_{a, b, N}]\!]
  \:.
\end{align*}
$$

## Lemma: predictable_upcrossingPredictableSet {#lem:predictable_upcrossingPredictableSet uses="def:upcrossingPredictableSet, def:predictable"}

The upcrossing predictable set $A_N$ of $X : \mathbb{N} \to \Omega \to \mathbb{R}$ before time $N$ is a predictable set.

### Proof {uses="lem:isStoppingTime_lowerCrossingTime, lem:isStoppingTime_upperCrossingTime, lem:predictable_stochasticInterval"}

By Lemmas [isStoppingTime_lowerCrossingTime](#lem:isStoppingTime_lowerCrossingTime) and [isStoppingTime_upperCrossingTime](#lem:isStoppingTime_upperCrossingTime), $\sigma^k_{a, b, N}$ and $\tau^{k+1}_{a, b, N}$ are stopping times.
Hence by [predictable_stochasticInterval](#lem:predictable_stochasticInterval), the stochastic interval $]\!]\sigma^k_{a, b, N}, \tau^{k+1}_{a, b, N}]\!]$ is a predictable set for each $k$.
Since a finite union of predictable sets is predictable, $A_N$ is predictable.

## Lemma: elementaryPredictableSet_upcrossingPredictableSet {#lem:elementaryPredictableSet_upcrossingPredictableSet uses="def:upcrossingPredictableSet, def:elementaryPredictableSet"}

The upcrossing predictable set $A_N$ of $X : \mathbb{N} \to \Omega \to \mathbb{R}$ before time $N$ is an elementary predictable set.

### Proof {uses="lem:isStoppingTime_lowerCrossingTime, lem:isStoppingTime_upperCrossingTime, lem:elementaryPredictableSet_stochasticInterval"}

By Lemmas [isStoppingTime_lowerCrossingTime](#lem:isStoppingTime_lowerCrossingTime) and [isStoppingTime_upperCrossingTime](#lem:isStoppingTime_upperCrossingTime), $\sigma^k_{a, b, N}$ and $\tau^{k+1}_{a, b, N}$ are stopping times, and are bounded by $N$.
By [elementaryPredictableSet_stochasticInterval](#lem:elementaryPredictableSet_stochasticInterval), the stochastic intervals $]\!]\sigma^k_{a, b, N}, \tau^{k+1}_{a, b, N}]\!]$ are elementary predictable sets for each $k$.
Since a finite union of elementary predictable sets is elementary predictable, $A_N$ is elementary predictable.

## Lemma: upcrossing_simpleProcess_le_nat {#lem:upcrossing_simpleProcess_le_nat uses="def:elemStochIntegral, def:simpleProcess, def:upcrossings, def:upcrossingPredictableSet"}

Let $X : \mathbb{N} \to \Omega \to \mathbb{R}$ be an adapted process on the natural numbers.
Then for all $a < b$ in $\mathbb{R}$ and $t \in \mathbb{N}$, for $A_t$ the upcrossing predictable set of $X$ before time $t$, the number of upcrossings $U_t[a, b]$ of the interval $[a, b]$ before time $t$ satisfies

$$
\begin{align*}
  (b - a) U_t[a, b] \le (\mathbb{1}_{A_t} \bullet X)_t + \max\{a - X_t, 0\}
  \:.
\end{align*}
$$

### Proof {uses="lem:elementaryPredictableSet_upcrossingPredictableSet"}

$$
\begin{align*}
  (\mathbb{1}_{A_t} \bullet X)_t
  &= \sum_{k=0}^t (X_{\tau^{k+1}_{a, b, t} \wedge t} - X_{\sigma^k_{a, b, t} \wedge t})
  \\
  &= \sum_{k=0}^{U_t[a, b]-1} (X_{\tau^{k+1}_{a, b, t} \wedge t} - X_{\sigma^k_{a, b, t} \wedge t})
    + (X_t - X_{\sigma^{U_t[a, b]}_{a, b, t} \wedge t})
  \\
  &\ge (b - a) U_t[a, b] + \min\{X_t - a, 0\}
  \\
  &= (b - a) U_t[a, b] - \max\{a - X_t, 0\}
  \: .
\end{align*}
$$

## Lemma: upcrossing_simpleProcess_le {#lem:upcrossing_simpleProcess_le uses="def:elemStochIntegral, def:simpleProcess, def:upcrossings"}

Let $X : T \to \Omega \to \mathbb{R}$ be an adapted process on a finite time domain $T$.
Then for all $a < b$ in $\mathbb{R}$ and $t \in T$, there exists an elementary predictable set $A$ such that the number of upcrossings $U_t[a, b]$ of the interval $[a, b]$ before time $t$ satisfies

$$
\begin{align*}
  (b - a) U_t[a, b] \le (\mathbb{1}_A \bullet X)_t + \max\{a - X_t, 0\}
  \:.
\end{align*}
$$

### Proof {uses="lem:upcrossing_simpleProcess_le_nat"}

Go from $T$ to a subset of $\mathbb{N}$ and use [upcrossing_simpleProcess_le_nat](#lem:upcrossing_simpleProcess_le_nat)?

**Cadlag modifications**

## Theorem: exists_rightContinuous_modification_of_bounded_elemStochIntegral {#thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral lean="ProbabilityTheory.exists_modification_left_right_limit" uses="def:elemStochIntegral, def:modification"}

Let $X : T \to \Omega \to \mathbb{R}$ be an adapted stochastic process such that $X$ is integrable and for every $t \in T$ the set $\{\mathbb{E}[(\mathbb{1}_A \bullet X)_t] \mid A \text{ elementary predictable}\}$ is bounded.

Then $X$ has a modification $Y$ which has left and right limits everywhere and such that there is a countable set $S \subseteq T$ for which $Y$ is right-continuous on $T \setminus S$.

### Proof {uses="lem:upcrossing_simpleProcess_le, lem:tendsto_of_no_upcrossings"}

Let $D$ be a countable dense subset of $T$ (e.g.\ the rationals in $T$) and let $t \in T$ and let
  $S$ be a finite subset of $D \cap [0, t]$. By [upcrossing_simpleProcess_le](#lem:upcrossing_simpleProcess_le), for all
  $a < b$ in $\mathbb{R}$, the number of upcrossings $U_S[a, b]$ of the interval $[a, b]$ along $S$
  satisfies
  
$$
\begin{align*}
    (b - a) U_S[a, b] \le (\mathbb{1}_A \bullet X)_t + \max\{a - X_t, 0\}
  \end{align*}
$$

  for some elementary predictable set $A$.
  Taking expectations and using the boundedness hypothesis, we obtain
  
$$
\begin{align*}
    (b - a) \mathbb{E}[U_S[a, b]] \le L + \mathbb{E}[\max\{a - X_t, 0\}] \le L + |a| + \mathbb{E}[|X_t|]
  \end{align*}
$$

  where $L$ is a bound for $\{\mathbb{E}[(\mathbb{1}_A \bullet X)_t] \mid A \text{ elementary predictable}\}$.

  Now, let $S_1 \subseteq S_2 \subseteq \cdots$ be an increasing sequence of finite subsets of
  $D \cap [0, t]$ with $\bigcup_n S_n = D \cap [0, t]$.
  The number of upcrossings $U_{S_n}[a, b]$ is increasing in $n$.
  By monotone convergence,
  
$$
\begin{align*}
    (b - a) \mathbb{E}[U_{D \cap [0, t]}[a, b]] = \lim_{n \to \infty} (b - a) \mathbb{E}[U_{S_n}[a, b]]
      \le L + |a| + \mathbb{E}[|X_t|] < \infty.
  \end{align*}
$$

  In particular, $U_{D \cap [0, t]}[a, b] < \infty$ a.s. for each pair $a < b$.
  Since $\mathbb{Q}^2$ is countable, we conclude that almost surely, for all rational $a < b$, the
  number of upcrossings of $[a, b]$ by $X$ along $D \cap [0, t]$ is finite.

  By [tendsto_of_no_upcrossings](#lem:tendsto_of_no_upcrossings), finite upcrossings of all rational intervals implies
  that the left and right limits of $s \mapsto X_s(\omega)$ along $D$ exist at every $t \in T$, for
  almost every $\omega$. Define
  $$\tilde{Y}_t(\omega) = \lim_{\substack{s \downarrow t \\ s \in D}} X_s(\omega)$$
  whenever this limit exists, and $\tilde{Y}_t(\omega) = 0$ otherwise.
  Then $\tilde{Y}$ has left and right limits everywhere (along $T$) almost surely, and is
  right-continuous at every point of $D$.

  We claim that the set
  
$$
\begin{align*}
    S = \{t \in T \mid \tilde{Y}_t \ne X_t \text{ with positive probability}\}
  \end{align*}
$$

  is countable.
  For each $n \in \mathbb{N}$, consider the set
  
$$
\begin{align*}
    S_n = \{t \in T \cap [0, n] \mid \mathbb{P}(|\tilde{Y}_t - X_t| > 1/n) > 1/n\}
    \:.
  \end{align*}
$$

  We have $S = \bigcup_n S_n$, so it suffices to show each $S_n$ is finite.
  If $S_n$ were infinite, it would contain a monotone sequence $t_k$ converging to some limit
  $t^* \in [0, n]$. Adding $\{t_k\}$ to $D$ and repeating the upcrossing argument, we would obtain
  that $X_{t_k}$ converges along $D \cup \{t_k\}$ almost surely. But $\tilde{Y}_{t_k}$ also converges
  (since $\tilde{Y}$ has left/right limits), giving $\tilde{Y}_{t_k} - X_{t_k} \to 0$ in probability,
  contradicting the definition of $S_n$. Therefore each $S_n$ is finite and $S$ is countable.

  Define
  
$$
\begin{align*}
    Y_t = \begin{cases} X_t & \text{if } t \in S \:, \\ \tilde{Y}_t & \text{if } t \notin S \:. \end{cases}
  \end{align*}
$$

  Then $Y_t = X_t$ almost surely for all $t$: for $t \in S$ this is by definition, and for
  $t \notin S$ this follows from $\tilde{Y}_t = X_t$ a.s. Thus $Y$ is a modification of $X$.

  Since $\tilde{Y}$ has left and right limits everywhere almost surely, and $Y$ differs from
  $\tilde{Y}$ only on the countable set $S$, $Y$ also has left and right limits everywhere almost surely.
  Furthermore, $Y$ agrees with $\tilde{Y}$ on $T \setminus S$, so $Y$ is right-continuous on $T \setminus S$.

In the following, we say that a stochastic process $X$ is _right-continuous in probability_ if for all $t \in T$, $\lim_{s \downarrow t} X_s = X_t$ in which the limit is taken in probability.

## Corollary: exists_caldag_modification {#cor:exists_caldag_modification lean="ProbabilityTheory.exists_modification_isCadlag" uses="def:elemStochIntegral, def:modification"}

Let $X : T \to \Omega \to \mathbb{R}$ be an adapted stochastic process which is right-continuous in probability and such that the boundedness condition of [exists_rightContinuous_modification_of_bounded_elemStochIntegral](#thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral) holds.
Then $X$ has a cadlag modification.

### Proof {uses="thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral"}

Let $Y$ be the modification of $X$ given by [exists_rightContinuous_modification_of_bounded_elemStochIntegral](#thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral).
$Y$ has left and right limits everywhere and there is a countable set $S$ such that $Y$ is right-continuous on $T \setminus S$. It remains to show that $Y$ is right-continuous at the points of $S$.
Let $Y_{t+}$ denote the right limit of $Y$ at $t$.
Since $X$ is right-continuous in probability, for all $t \in S$, $Y_t = Y_{t+}$ almost surely.
Therefore, since $S$ is countable, we have that almost surely $Y_t = Y_{t+}$ for all $t \in S$ (and hence for all $t \in T$).
$Y$ is therefore almost surely cadlag.
We can modify $Y$ on the null set to obtain a cadlag modification of $X$.

## Lemma: Submartingale.integral_elemStochIntegral_bounded {#lem:Submartingale.integral_elemStochIntegral_bounded uses="def:elemStochIntegral, def:Submartingale"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale.
Then for every $t \in T$, the set $\{\mathbb{E}[(\mathbb{1}_A \bullet X)_t] \mid A \text{ elementary predictable}\}$ is bounded.

### Proof {uses="lem:submartingale_iff_integral_elemStochIntegral_nonneg, cor:Submartingale.integral_elemStochIntegral_le"}

Since $X$ is a submartingale, for any elementary predictable set $A$, we have ([Submartingale.integral_elemStochIntegral_le](#cor:Submartingale.integral_elemStochIntegral_le))

$$
\begin{align*}
  0 \le \mathbb{E}[(\mathbb{1}_A \bullet X)_t] \le \mathbb{E}[X_t - X_0]
  \:.
\end{align*}
$$

As $X_t$ and $X_0$ are integrable, the set $\{\mathbb{E}[(\mathbb{1}_A \bullet X)_t] \mid A \text{ elementary predictable}\}$ is bounded.

## Lemma: Submartingale.exists_cadlag_modification_of_rightContinuous {#lem:Submartingale.exists_cadlag_modification_of_rightContinuous uses="def:modification, def:Submartingale"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale which is right-continuous in probability.
Then $X$ has a cadlag modification.

### Proof {uses="cor:exists_caldag_modification, lem:Submartingale.integral_elemStochIntegral_bounded"}

We apply [exists_caldag_modification](#cor:exists_caldag_modification), in which the boundedness condition of [exists_rightContinuous_modification_of_bounded_elemStochIntegral](#thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral) holds by [Submartingale.integral_elemStochIntegral_bounded](#lem:Submartingale.integral_elemStochIntegral_bounded).

## Lemma: Submartingale.exists_modifications_limits {#lem:Submartingale.exists_modifications_limits uses="def:modification, def:Submartingale"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale.
Then $X$ has a modification $Y$ such that for all $t \in T$, $Y$ has left and right limits at $t$ and such that there is a countable set $S \subseteq T$ for which $Y$ is right-continuous on $T \setminus S$.

### Proof {uses="thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral, lem:Submartingale.integral_elemStochIntegral_bounded"}

Apply [exists_rightContinuous_modification_of_bounded_elemStochIntegral](#thm:exists_rightContinuous_modification_of_bounded_elemStochIntegral), in which the boundedness condition holds by [Submartingale.integral_elemStochIntegral_bounded](#lem:Submartingale.integral_elemStochIntegral_bounded).

## Lemma: Submartingale.uniformIntegrable_of_antitone_of_ge {#lem:Submartingale.uniformIntegrable_of_antitone_of_ge uses="def:Submartingale"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale and let $t_n$ be a decreasing sequence in $T$ which is bounded below.
Then the family $\{X_{t_n}\}_{n \in \mathbb{N}}$ is uniformly integrable.

## Lemma: Submartingale.le_condExp_of_tendsto {#lem:Submartingale.le_condExp_of_tendsto uses="def:Submartingale"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale and $t \in T$.
Let $t_n$ be a decreasing sequence in $T$ converging to $t$, and such that $X_{t_n}$ tends to a limit $X_{t+}$ almost surely.
Then $X_t \le P[X_{t+} \mid \mathcal{F}_t]$ almost surely.

### Proof {uses="lem:Submartingale.uniformIntegrable_of_antitone_of_ge"}

By the submartingale property, for all $n$ we have that $X_t \le P[X_{t_n} \mid \mathcal{F}_t]$ almost surely.
By [Submartingale.uniformIntegrable_of_antitone_of_ge](#lem:Submartingale.uniformIntegrable_of_antitone_of_ge), the family $\{X_{t_n}\}_{n \in \mathbb{N}}$ is uniformly integrable.

TODO: conclude that $P[X_{t+} \mid \mathcal{F}_t]$ is the limit of $P[X_{t_n} \mid \mathcal{F}_t]$.

## Theorem: Submartingale.exists_cadlag_modification_iff_rightContinuous {#thm:Submartingale.exists_cadlag_modification_iff_rightContinuous uses="def:modification, def:Submartingale, def:rightContinuous"}

Let $X : T \to \Omega \to \mathbb{R}$ be a submartingale with respect to a right-continuous filtration.
Then $X$ has a cadlag modification if and only if $t \mapsto \mathbb{E}[X_t]$ is right-continuous.

### Proof {uses="lem:Submartingale.exists_modifications_limits, lem:Submartingale.le_condExp_of_tendsto, lem:Submartingale.uniformIntegrable_of_antitone_of_ge"}

Let $Y$ be the modification of $X$ given by [Submartingale.exists_modifications_limits](#lem:Submartingale.exists_modifications_limits).
$Y$ has left and right limits everywhere and there is a countable set $S$ such that $Y$ is right-continuous on $T \setminus S$.
It remains to show that for each $t \in S$, $Y$ is right-continuous at $t$ almost surely. We will then be able to modify $Y$ on a null set to obtain a cadlag modification of $X$.
Let $t \in S$ and let $Y_{t+}$ denote the right limit of $Y$ at $t$.

We show that $Y_t = P[Y_{t+} \mid \mathcal{F}_t]$ almost surely, and that $P[Y_{t+} \mid \mathcal{F}_t] = Y_{t+}$ almost surely, which will conclude the proof.
For the second equality it suffices to show that $Y_{t+}$ is $\mathcal{F}_t$-measurable, which follows from the right-continuity of the filtration.

For the first equality, it suffices to show that $P[Y_{t+} \mid \mathcal{F}_t] - Y_t$ is an almost surely nonnegative random variable with zero expectation.
Nonnegative follows from [Submartingale.le_condExp_of_tendsto](#lem:Submartingale.le_condExp_of_tendsto).
The expectation is $P[Y_{t+}] - P[Y_t]$. Let $t_n$ be a decreasing sequence in $T$ converging to $t$.
By right-continuity of $t \mapsto \mathbb{E}[Y_t]$, we have that

$$
\begin{align*}
  P[Y_t] = \lim_{n \to \infty} P[Y_{t_n}]
  \: .
\end{align*}
$$

By uniform integrability ([Submartingale.uniformIntegrable_of_antitone_of_ge](#lem:Submartingale.uniformIntegrable_of_antitone_of_ge)), we have that

$$
\begin{align*}
  P[Y_{t+}] = \lim_{n \to \infty} P[Y_{t_n}]
  \: .
\end{align*}
$$

Therefore $P[Y_{t+}] = P[Y_t]$, which concludes the proof.

## Theorem: Martingale.exists_cadlag_modification {#thm:Martingale.exists_cadlag_modification uses="def:modification, def:Martingale, def:rightContinuous"}

Let $X : T \to \Omega \to \mathbb{R}$ be a martingale with respect to a right-continuous filtration.
Then $X$ has a cadlag modification.

### Proof {uses="thm:Submartingale.exists_cadlag_modification_iff_rightContinuous"}

$X$ is in particular a submartingale, and for all $t \in T$, we have that $\mathbb{E}[X_t] = \mathbb{E}[X_0]$ by the martingale property.
Therefore $t \mapsto \mathbb{E}[X_t]$ is right-continuous, and we can apply [Submartingale.exists_cadlag_modification_iff_rightContinuous](#thm:Submartingale.exists_cadlag_modification_iff_rightContinuous).

**Cadlag modifications of (local) martingales**

TODO: this is partially or entirely redundant, consider removing this section.

## Lemma: exists_cadlag_mod_of_nonneg_submg {#lem:exists_cadlag_mod_of_nonneg_submg uses="def:hasUsualConditions, def:Submartingale"}

Let the filtered probability space satisfy the usual conditions.
  Then every nonnegative submartingale $X$ admits a modification that is still a nonnegative submartingale with cadlag trajectories.

### Proof

See 8.2.3 of Pascucci.

## Lemma: exists_cadlag_mod_of_local_mg {#lem:exists_cadlag_mod_of_local_mg uses="def:hasUsualConditions"}

Let the filtered probability space satisfy the usual conditions.
  Then every local martingale $X$ admits a modification that is still a local martingale with cadlag trajectories.

### Proof {uses="thm:Martingale.exists_cadlag_modification"}

