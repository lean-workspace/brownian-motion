---
title: 'Stochastic processes'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

Let $T$ be an index set and $\Omega$ a measurable space, with measure $\mathbb{P}$.
A stochastic process is a function $X : T \to \Omega \to E$, where $E$ is another measurable space, such that for all $t \in T$, $X_t : \Omega \to E$ is $\mathbb{P}$-a.e. measurable.

## Definition: Law of a stochastic process {#def:processLaw}

The law of a stochastic process $X$ is the measure on the measurable space $E^T$ obtained by pushing forward the measure $\mathbb{P}$ by the map $\omega \mapsto X(\cdot, \omega)$.

**Lean remark**: we don't use a Lean definition for the law, but write the map in full.

## Definition: Modification {#def:modification}

We say that a stochastic process $Y$ is a _modification_ of another stochastic process $X$ if for all $t \in T$, $Y_t =_{\mathbb{P}\text{-a.e.}} X_t$.

**Lean remark**: we don't use a Lean definition for being a modification, but write explicitly the condition $\forall t \in T,\ Y_t =_{\mathbb{P}\text{-a.e.}} X_t$ .

## Definition: Indistinguishable {#def:indistinguishable}

We say that a stochastic processes $Y$ is a _indistinguishable_ from $X$ if $\mathbb{P}$-a.e., for all $t \in T$, $X_t = Y_t$.

A summary of the next few lemmas is this:

- indistinguishable $\implies$ modification $\implies$ same law,
- modification and continuous with $T$ separable $\implies$ indistinguishable.

## Lemma: Indistinguishable.Modification {#lem:Indistinguishable.Modification lean="modification_of_indistinguishable" uses="def:indistinguishable, def:modification"}

If $Y$ is indistinguishable from $X$, then $Y$ is a modification of $X$.

### Proof

Obvious.

## Lemma: map_eq_of_modification {#lem:map_eq_of_modification lean="ProbabilityTheory.map_eq_of_forall_ae_eq" uses="def:modification"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X, Y : T \to \Omega \to E$ be two stochastic processes that are modifications of each other.
Then for all $t_1, \ldots, t_n \in T$, the random vector $(X_{t_1}, \ldots, X_{t_n})$ has the same distribution as the random vector $(Y_{t_1}, \ldots, Y_{t_n})$.
That is, $X$ and $Y$ have same finite-dimensional distributions.

### Proof

By the modification property, almost surely $X_{t_i} = Y_{t_i}$ for all $i \in [n]$.
Thus the function $\omega \mapsto (X_{t_1}(\omega), \ldots, X_{t_n}(\omega))$ is equal to $\omega \mapsto (Y_{t_1}(\omega), \ldots, Y_{t_n}(\omega))$ almost surely, hence the maps of $\mathbb{P}$ by these two functions are equal.

## Lemma: map_eq_iff {#lem:map_eq_iff lean="ProbabilityTheory.map_eq_iff_forall_finset_map_restrict_eq" uses="def:processLaw"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $X, Y : T \to \Omega \to E$ be two stochastic processes.
Then $X$ and $Y$ have same finite-dimensional distributions if and only if they have the same law.

### Proof

TODO: consider the $\pi$-system of cylinder sets.

## Lemma: indistinguishable_of_modification_of_continuous {#lem:indistinguishable_of_modification_of_continuous lean="indistinguishable_of_modification" uses="def:modification, def:indistinguishable"}

Let $T$ and $E$ be topological spaces and suppose that $T$ is separable Hausdorff.
Let $X, Y : T \to \Omega \to E$ be two stochastic processes that are modifications of each other and are almost surely continuous.
Then $X$ and $Y$ are indistinguishable.

### Proof

Since $T$ is separable, it has a countable dense subset $D$.
Since $D$ is countable,

$$
\begin{align*}
  (\forall t \in D, \mathbb{P}\text{-a.e.}, X_t = Y_t)
  \iff (\mathbb{P}\text{-a.e.}, \forall t \in D, X_t = Y_t)
\end{align*}
$$

Hence by the modification property we have that almost surely, for all $t \in D$, $X_t = Y_t$.
Then almost surely $X$ and $Y$ are continuous functions which are equal on a dense subset of $T$: those two functions are equal everywhere.

