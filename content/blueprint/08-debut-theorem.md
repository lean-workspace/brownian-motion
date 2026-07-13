---
title: 'Debut Theorem'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Choquet's capacitability theorem**

This section is devoted to the proof of Choquet's capacitability theorem, which is a key ingredient in the proof of the debut theorem. The presentation follows [@bichteler2002stochastic] for the definition of analytic sets (that definition changes a lot between sources) and for the general proof steps, and [@he2019semimartingale] and the PlanetMath website for many of the proofs of individual lemmas.
Although the definition of analytic sets in [@he2019semimartingale] is different, the proofs follow the same general steps and the same ideas, and that book is much more detailed than [@bichteler2002stochastic].

**Pavings and Compact systems**

A paving is simply a set of sets.

## Definition: image2_prod {#def:image2_prod}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

The product of two pavings $S$ and $T$ is the set of sets of the form $s \times t$ where $s \in S$ and $t \in T$. We denote that product by $S \times T$.

## Definition: supClosure {#def:supClosure lean="supClosure"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For a paving $S$, we denote by $S^{\cup f}$ the set of finite unions of sets in $S$.

## Definition: infClosure {#def:infClosure lean="infClosure"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

For a paving $S$, we denote by $S^{\cap f}$ the set of finite intersections of sets in $S$.

## Definition: countableSupClosure {#def:countableSupClosure lean="countableSupClosure"}

We denote by $S_\sigma$ the set of countable unions of sets in $S$.

## Definition: countableInfClosure {#def:countableInfClosure lean="countableInfClosure"}

We denote by $S_\delta$ the set of countable intersections of sets in $S$.

## Lemma: InfClosed.mem_countableInfClosure_iff {#lem:InfClosed.mem_countableInfClosure_iff lean="InfClosed.mem_countableInfClosure_iff" uses="def:countableInfClosure"}

If a paving $S$ is closed under pairwise intersection, then a set $s$ is in $S_\delta$ if and only if there exists a monotone decreasing family of sets $(A_n)_{n\in\mathbb{N}}$ in $S$ such that $s = \bigcap_{n\in\mathbb{N}} A_n$.

### Proof

The ``monotone decreasing'' condition is the only non-trivial part of the statement: without it it would just be the definition of $S_\delta$.
If $s \in S_\delta$ there exists a family $(B_n)$ that satisfies the condition but may not be monotone. We can then define $A_n = \bigcap_{k \le n} B_k$, and the family $(A_n)$ is monotone decreasing and satisfies $\bigcap_{n\in\mathbb{N}} A_n = \bigcap_{n\in\mathbb{N}} B_n = s$.

## Lemma: SupClosed.mem_countableSupClosure_iff {#lem:SupClosed.mem_countableSupClosure_iff lean="SupClosed.mem_countableSupClosure_iff" uses="def:countableSupClosure"}

If a paving $S$ is closed under pairwise union, then a set $s$ is in $S_\sigma$ if and only if there exists a monotone increasing family of sets $(A_n)_{n\in\mathbb{N}}$ in $S$ such that $s = \bigcup_{n\in\mathbb{N}} A_n$.

### Proof

Similar to the proof of [InfClosed.mem_countableInfClosure_iff](#lem:InfClosed.mem_countableInfClosure_iff).

## Definition: IsCompactSystem {#def:IsCompactSystem lean="IsCompactSystem"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

A set of sets $K$ is a compact system if for every countable family $(C_n)_{n \in \mathbb{N}}$ of sets in $K$ such that $\bigcap_{n \in\mathbb{N}} C_n = \emptyset$, there exists a finite subset $S$ of $\mathbb{N}$ such that $\bigcap_{n \in S} C_n = \emptyset$.

## Lemma: isCompactSystem_isCompact_isClosed {#lem:isCompactSystem_isCompact_isClosed lean="isCompactSystem_isCompact_isClosed" uses="def:IsCompactSystem"}

The family of compact closed sets of a topological space is a compact system.

### Proof {uses="def:IsCompactSystem"}

## Lemma: isCompactSystem_isCompact {#lem:isCompactSystem_isCompact lean="isCompactSystem_isCompact" uses="def:IsCompactSystem"}

The family of compact sets of a T2 topological space is a compact system.

### Proof {uses="lem:isCompactSystem_isCompact_isClosed"}

The T2 assumption ensures that compact sets are closed, so the family of compact sets is the family of compact closed sets, which is a compact system by [isCompactSystem_isCompact_isClosed](#lem:isCompactSystem_isCompact_isClosed).

## Lemma: IsCompactSystem.mono {#lem:IsCompactSystem.mono lean="IsCompactSystem.mono" uses="def:IsCompactSystem"}

If $S \subseteq T$ and $T$ is a compact system, then $S$ is a compact system.

### Proof {uses="def:IsCompactSystem"}

Any sequence of sets in $S$ is a sequence of sets in $T$, so if the intersection of the sequence is empty, then there is a finite subset of the sequence whose intersection is empty by the compact system property of $T$.

## Lemma: isCompactSystem_Icc {#lem:isCompactSystem_Icc lean="isCompactSystem_Icc" uses="def:IsCompactSystem"}

The family of closed compact intervals of $\mathbb{R}$ is a compact system.

### Proof {uses="lem:isCompactSystem_isCompact, lem:IsCompactSystem.mono"}

The family of closed compact intervals of $\mathbb{R}$ is a family of compact sets, so it is a compact system by [isCompactSystem_isCompact](#lem:isCompactSystem_isCompact) and [IsCompactSystem.mono](#lem:IsCompactSystem.mono).

## Lemma: IsCompactSystem.pi {#lem:IsCompactSystem.pi uses="def:IsCompactSystem"}

The product of a countable family of compact systems is a compact system.

## Lemma: IsCompactSystem.sigma {#lem:IsCompactSystem.sigma lean="IsCompactSystem.sigma" uses="def:IsCompactSystem"}

The sum of a countable family of compact systems is a compact system.

## Lemma: IsCompactSystem.image2_prod {#lem:IsCompactSystem.image2_prod lean="IsCompactSystem.image2_prod" uses="def:IsCompactSystem"}

The product of two compact systems $S \times T$ is a compact system.

## Lemma: IsCompactSystem.supClosure {#lem:IsCompactSystem.supClosure lean="IsCompactSystem.supClosure" uses="def:IsCompactSystem, def:supClosure"}

If $S$ is a compact system, then $S^{\cup f}$ is a compact system.

## Lemma: IsCompactSystem.countableInfClosure {#lem:IsCompactSystem.countableInfClosure uses="def:IsCompactSystem, def:countableInfClosure"}

If $S$ is a compact system, then $S_\delta$ is a compact system.

## Lemma: IsCompactSystem.infClosure {#lem:IsCompactSystem.infClosure lean="IsCompactSystem.infClosure" uses="def:IsCompactSystem, def:infClosure"}

If $S$ is a compact system, then $S^{\cap f}$ is a compact system.

### Proof {uses="lem:IsCompactSystem.mono, lem:IsCompactSystem.countableInfClosure"}

$S_\delta$ is a compact system by [IsCompactSystem.countableInfClosure](#lem:IsCompactSystem.countableInfClosure), and $S^{\cap f} \subseteq S_\delta$, so we can apply [IsCompactSystem.mono](#lem:IsCompactSystem.mono).

## Theorem: fst_iInter_of_supClosure_image2_prod_of_antitone {#thm:fst_iInter_of_supClosure_image2_prod_of_antitone lean="MeasureTheory.fst_iInter_of_supClosure_image2_prod_of_antitone" uses="def:IsCompactSystem, def:supClosure, def:image2_prod"}

Let $S$ be a paving of $\mathcal{X}$ and $T$ be a compact system of $\mathcal{K}$.
Let $(B_n)_{n \in \mathbb{N}}$ be a monotone decreasing sequence of sets in $(S \times T)^{\cup f}$.
Let $\pi_{\mathcal{X}} : \mathcal{X} \times \mathcal{K} \to \mathcal{X}$ be the projection on $\mathcal{X}$.
Then

$$
\begin{align*}
  \pi_{\mathcal{X}}\left(\bigcap_{n\in\mathbb{N}} B_n\right) = \bigcap_{n\in\mathbb{N}} \pi_{\mathcal{X}}(B_n).
\end{align*}
$$

### Proof {uses="lem:IsCompactSystem.supClosure"}

**Analytic sets**

## Definition: Analytic set {#def:IsPavingAnalytic lean="MeasureTheory.IsPavingAnalytic, MeasureTheory.IsPavingAnalyticFor" uses="def:IsCompactSystem, def:countableSupClosure, def:countableInfClosure, def:image2_prod"}

Let $F$ be a paving of a type $\mathcal{X}$.
A set $s$ of $\mathcal{X}$ is said to be $F$-analytic if there exists a nonempty type $\mathcal{K}$ and a compact system $K$ of $\mathcal{K}$ with $\emptyset \in K$ such that $s$ is the projection on $\mathcal{X}$ of a set in $(F \times K)_{\sigma \delta}$.

We denote the set of $F$-analytic sets by $\mathcal{A}(F)$.

Lean note: we can't quantify over universes, so we have to restrict $\mathcal{K}$ to `Type`. We have an auxiliary definition `IsPavingAnalyticFor` that specifies which $\mathcal{K}$ is used.

## Lemma: isPavingAnalytic_of_prop {#lem:isPavingAnalytic_of_prop lean="MeasureTheory.isPavingAnalytic_of_mem" uses="def:IsPavingAnalytic"}

Every set in $F$ is $F$-analytic: $F \subseteq \mathcal{A}(F)$.

## Lemma: IsPavingAnalytic.mono {#lem:IsPavingAnalytic.mono lean="MeasureTheory.IsPavingAnalytic.mono" uses="def:IsPavingAnalytic"}

If $F \subseteq G$ and $s$ is $F$-analytic, then $s$ is $G$-analytic: $\mathcal{A}(F) \subseteq \mathcal{A}(G)$.

## Lemma: IsPavingAnalytic.exists_mem_countableSupClosure_superset {#lem:IsPavingAnalytic.exists_mem_countableSupClosure_superset lean="MeasureTheory.IsPavingAnalyticFor.exists_mem_countableSupClosure_superset" uses="def:IsPavingAnalytic"}

If $s$ is $F$-analytic, then there exists a set $t$ in $F_\sigma$ such that $s \subseteq t$.

## Lemma: IsPavingAnalytic.iUnion {#lem:IsPavingAnalytic.iUnion lean="MeasureTheory.IsPavingAnalytic.iUnion, MeasureTheory.IsPavingAnalytic.union" uses="def:IsPavingAnalytic"}

A countable union of $F$-analytic sets is $F$-analytic.

### Proof {uses="lem:IsCompactSystem.pi"}

## Lemma: IsPavingAnalytic.iInter {#lem:IsPavingAnalytic.iInter lean="MeasureTheory.IsPavingAnalytic.iInter, MeasureTheory.IsPavingAnalytic.inter" uses="def:IsPavingAnalytic"}

A countable intersection of $F$-analytic sets is $F$-analytic.

### Proof {uses="lem:IsCompactSystem.sigma"}

## Lemma: IsPavingAnalytic.fst {#lem:IsPavingAnalytic.fst lean="MeasureTheory.IsPavingAnalytic.fst" uses="def:IsPavingAnalytic, def:IsCompactSystem"}

Let $F$ be a set of sets of $\mathcal{X}$ and $K$ be a compact system of $\mathcal{K}$, with $\emptyset \in K$.
If a set $s$ of $\mathcal{X} \times \mathcal{K}$ is $F \times K$-analytic, then its projection on $\mathcal{X}$ is $F$-analytic.

### Proof {uses="lem:IsCompactSystem.image2_prod"}

## Lemma: IsPavingAnalytic.prod_left {#lem:IsPavingAnalytic.prod_left lean="MeasureTheory.IsPavingAnalytic.prod_left" uses="def:IsPavingAnalytic"}

If $t \in T$ and $s$ is $F$-analytic, then $t \times s$ is $(T \times F)$-analytic: $T \times \mathcal{A}(F) \subseteq \mathcal{A}(T \times F)$.

## Lemma: IsPavingAnalytic.prod {#lem:IsPavingAnalytic.prod lean="MeasureTheory.IsPavingAnalytic.prod" uses="def:IsPavingAnalytic"}

If $s$ is $F$-analytic and $t$ is $G$-analytic, then $s \times t$ is $(F \times G)$-analytic: $\mathcal{A}(F) \times \mathcal{A}(G) \subseteq \mathcal{A}(F \times G)$.

### Proof {uses="lem:IsPavingAnalytic.prod_left, lem:IsPavingAnalytic.exists_mem_countableSupClosure_superset"}

## Lemma: isPavingAnalytic_isPavingAnalytic {#lem:isPavingAnalytic_isPavingAnalytic lean="MeasureTheory.isPavingAnalytic_isPavingAnalytic" uses="def:IsPavingAnalytic"}

$\mathcal{A}(\mathcal{A}(F)) = \mathcal{A}(F)$.

### Proof {uses="lem:IsPavingAnalytic.iInter, lem:IsPavingAnalytic.iUnion, lem:IsPavingAnalytic.prod, lem:IsPavingAnalytic.fst"}

**Analytic sets in measurable spaces**

We denote by $K_{\mathbb{R}}$ the paving of compact sets of $\mathbb{R}$ and let $I_{\mathbb{R}}$ be the paving of closed compact intervals of $\mathbb{R}$.
For a measurable space $\mathcal{X}$, we denote by $M_{\mathcal{X}}$ the paving of measurable sets of $\mathcal{X}$.

## Lemma: isPavingAnalytic_of_measurableSet_generateFrom {#lem:isPavingAnalytic_of_measurableSet_generateFrom lean="MeasureTheory.isPavingAnalytic_of_measurableSet_generateFrom" uses="def:IsPavingAnalytic"}

Let $F$ be a paving with $\emptyset \in F$ and let $\sigma(F)$ be the $\sigma$-algebra generated by $F$.
Suppose that for every $t \in F$, $t^c$ is $F$-analytic.
Then every set in $\sigma(F)$ is $F$-analytic: $\sigma(F) \subseteq \mathcal{A}(F)$.

### Proof {uses="lem:isPavingAnalytic_of_prop, lem:IsPavingAnalytic.iUnion, lem:IsPavingAnalytic.iInter"}

## Lemma: MeasurableSet.isPavingAnalytic_Icc_real {#lem:MeasurableSet.isPavingAnalytic_Icc_real lean="MeasurableSet.isPavingAnalytic_Icc_real" uses="def:IsPavingAnalytic"}

A measurable set of $\mathbb{R}$ is $I_{\mathbb{R}}$-analytic.
That is, $M_{\mathbb{R}} \subseteq \mathcal{A}(I_{\mathbb{R}})$.

### Proof {uses="lem:isPavingAnalytic_of_measurableSet_generateFrom, lem:IsPavingAnalytic.iUnion, lem:isPavingAnalytic_of_prop"}

## Lemma: IsPavingAnalytic_measurableSet_iff_isPavingAnalytic_Icc {#lem:IsPavingAnalytic_measurableSet_iff_isPavingAnalytic_Icc lean="MeasureTheory.IsPavingAnalytic_measurableSet_iff_isPavingAnalytic_Icc" uses="def:IsPavingAnalytic"}

A set of $\mathbb{R}$ is $M_{\mathbb{R}}$-analytic if and only if it is $I_{\mathbb{R}}$-analytic.

### Proof {uses="lem:isPavingAnalytic_isPavingAnalytic, lem:MeasurableSet.isPavingAnalytic_Icc_real"}

## Lemma: MeasurableSet.isPavingAnalytic_image2_prod {#lem:MeasurableSet.isPavingAnalytic_image2_prod lean="MeasurableSet.isPavingAnalytic_image2_prod" uses="def:IsPavingAnalytic"}

Let $\mathcal{X}$ be a measurable space and $s$ be a measurable set of $\mathcal{X} \times \mathbb{R}$.
Then $s$ is $(M_{\mathcal{X}} \times I_{\mathbb{R}})$-analytic.

### Proof {uses="lem:isPavingAnalytic_of_measurableSet_generateFrom, lem:IsPavingAnalytic.iUnion, lem:isPavingAnalytic_of_prop"}

## Lemma: isPavingAnalytic_fst_of_image2_prod_measurableSet_Icc {#lem:isPavingAnalytic_fst_of_image2_prod_measurableSet_Icc lean="MeasureTheory.isPavingAnalytic_fst_of_image2_prod_measurableSet_Icc" uses="def:IsPavingAnalytic"}

Let $\mathcal{X}$ be a measurable space and $s$ be a set of $\mathcal{X} \times \mathbb{R}$ which is $(M_{\mathcal{X}} \times I_{\mathbb{R}})$-analytic.
Then the projection $\pi_{\mathcal{X}}(s)$ is $M_{\mathcal{X}}$-analytic.

### Proof {uses="lem:IsPavingAnalytic.fst, lem:isCompactSystem_Icc"}

## Lemma: MeasurableSet.isPavingAnalytic_fst {#lem:MeasurableSet.isPavingAnalytic_fst lean="MeasurableSet.isPavingAnalytic_fst" uses="def:IsPavingAnalytic"}

Let $\mathcal{X}$ be a measurable space and $s$ be a measurable set of $\mathcal{X} \times \mathbb{R}$.
Then the projection of $s$ on $\mathcal{X}$ is $M_{\mathcal{X}}$-analytic.

### Proof {uses="lem:MeasurableSet.isPavingAnalytic_image2_prod, lem:isPavingAnalytic_fst_of_image2_prod_measurableSet_Icc"}

## Definition: IsMeasurableAnalytic {#def:IsMeasurableAnalytic lean="MeasureTheory.IsMeasurableAnalytic, MeasureTheory.IsMeasurableAnalyticFor"}

We say that a set $s$ of a measurable space $\mathcal{X}$ is measurably analytic for a measurable space $\mathcal{K}$ if it is the projection of a measurable set of $\mathcal{X} \times \mathcal{K}$.

We say that $s$ is measurably analytic if it is measurably analytic for $\mathbb{R}$.

## Lemma: IsMeasurableAnalyticFor.isMeasurableAnalytic {#lem:IsMeasurableAnalyticFor.isMeasurableAnalytic lean="MeasureTheory.IsMeasurableAnalyticFor.isMeasurableAnalytic" uses="def:IsMeasurableAnalytic"}

Let $\mathcal{K}$ be a standard Borel space.
If a set $s$ of $\mathcal{X}$ is measurably analytic for $\mathcal{K}$, then it is measurably analytic.

### Proof

There is a measurable embedding of $\mathcal{K}$ into $\mathbb{R}$.

## Lemma: IsMeasurableAnalytic.isPavingAnalytic {#lem:IsMeasurableAnalytic.isPavingAnalytic lean="MeasureTheory.IsMeasurableAnalytic.isPavingAnalytic" uses="def:IsMeasurableAnalytic, def:IsPavingAnalytic"}

If a set $s$ of $\mathcal{X}$ is measurably analytic, then it is $M_{\mathcal{X}}$-analytic.

### Proof {uses="lem:MeasurableSet.isPavingAnalytic_fst"}

**Capacities and capacitable sets**

## Definition: Capacity {#def:Capacity lean="MeasureTheory.Capacity"}

Let $F$ be a set of sets of a type $\mathcal{X}$.
An $F$-capacity is a function $I$ from the sets of $\mathcal{X}$ to $\mathbb{R}_{+,\infty}$ such that

1. $I$ is monotone for set inclusion: for $s \subseteq t$, $I(s) \le I(t)$,
1. if $(s_n)_{n\in\mathbb{N}}$ is an increasing sequence of sets of $\mathcal{X}$, then $I(s_n)$ tends to $I(\bigcup_{n\in\mathbb{N}} s_n)$ at infinity,
1. if $(s_n)_{n\in\mathbb{N}}$ is a decreasing sequence of sets in $F$, then $I(s_n)$ tends to $I(\bigcap_{n\in\mathbb{N}} s_n)$ at infinity.

## Lemma: Capacity.comp_fst_aux {#lem:Capacity.comp_fst_aux lean="MeasureTheory.Capacity.comp_fst" uses="def:Capacity, def:IsCompactSystem"}

Let $F$ be a set of sets of $\mathcal{X}$ and let $I$ be an $F$-capacity.
Suppose that $\emptyset \in F$ and $F$ is closed under pairwise unions.
Let $K$ be a compact system of $\mathcal{K}$.
Let $\pi_{\mathcal{X}} : \mathcal{X} \times \mathcal{K} \to \mathcal{X}$ be the projection on the first coordinate.
Then the function $I_{\mathcal{X}}(u) = I(\pi_{\mathcal{X}}(u))$ is a capacity for $(F \times K)^{\cup f}$.

### Proof {uses="thm:fst_iInter_of_supClosure_image2_prod_of_antitone"}

## Definition: Capacity.comp_fst {#def:Capacity.comp_fst lean="MeasureTheory.Capacity.comp_fst" uses="def:Capacity, def:IsCompactSystem"}

Let $F$ be a set of sets of $\mathcal{X}$ and let $I$ be an $F$-capacity.
Suppose that $\emptyset \in F$ and $F$ is closed under pairwise unions.
Let $K$ be a compact system of $\mathcal{K}$.
Let $\pi_{\mathcal{X}} : \mathcal{X} \times \mathcal{K} \to \mathcal{X}$ be the projection on the first coordinate.
Then we define a capacity for $(F \times K)^{\cup f}$ by $I_{\mathcal{X}}(u) = I(\pi_{\mathcal{X}}(u))$ (it is indeed a capacity by [Capacity.comp_fst_aux](#lem:Capacity.comp_fst_aux)).

## Definition: IsCapacitable {#def:IsCapacitable lean="MeasureTheory.IsCapacitable" uses="def:Capacity"}

Let $F$ be a set of sets of $\mathcal{X}$ and let $I$ be an $F$-capacity.
A set $s$ of $\mathcal{X}$ is said to be $I$-capacitable if for all $a < I(s)$, there exists a set $t \in F_\delta$ such that $t \subseteq s$ and $a \le I(t)$.

## Lemma: isCapacitable_of_prop {#lem:isCapacitable_of_prop lean="MeasureTheory.isCapacitable_of_mem" uses="def:IsCapacitable"}

For $I$ an $F$-capacity, every set in $F$ is $I$-capacitable.

## Lemma: isCapacitable_mem_countableInfClosure_countableSupClosure {#lem:isCapacitable_mem_countableInfClosure_countableSupClosure lean="MeasureTheory.isCapacitable_mem_countableInfClosure_countableSupClosure" uses="def:IsCapacitable, def:Capacity, def:countableInfClosure, def:countableSupClosure"}

Suppose that $F$ contains the empty set and is closed under pairwise intersections and unions, and let $I$ be an $F$-capacity.
Then every set of $F_{\sigma \delta}$ is $I$-capacitable.

### Proof {uses="lem:SupClosed.mem_countableSupClosure_iff"}

## Lemma: mem_countableInfClosure_fst {#lem:mem_countableInfClosure_fst lean="MeasureTheory.mem_countableInfClosure_fst" uses="def:countableInfClosure, def:image2_prod, def:IsCompactSystem"}

Suppose that $F$ contains the empty set and is closed under pairwise intersections and unions, and let $I$ be an $F$-capacity.
Let $K$ be a compact system which is also closed under pairwise intersections.
Let $s \in ((F \times K)^{\cup f})_\delta$.
Then $\pi_{\mathcal{X}}(s) \in F_\delta$.

### Proof {uses="thm:fst_iInter_of_supClosure_image2_prod_of_antitone, lem:InfClosed.mem_countableInfClosure_iff"}

## Lemma: IsCapacitable.fst {#lem:IsCapacitable.fst lean="MeasureTheory.IsCapacitable.fst" uses="def:IsCapacitable, def:Capacity, def:Capacity.comp_fst, def:IsCompactSystem"}

Let $F$ be a set of sets of $\mathcal{X}$ and let $I$ be an $F$-capacity.
Suppose that $F$ contains the empty set and is closed under pairwise intersections and unions.
Let $K$ be a compact system of $\mathcal{K}$ which is also closed under pairwise intersections.
If a set $s$ of $\mathcal{X} \times \mathcal{K}$ is capacitable with respect to the capacity $I_{\mathcal{X}}$ of [Capacity.comp_fst](#def:Capacity.comp_fst), then its projection on $\mathcal{X}$ is capacitable with respect to $I$.

### Proof {uses="lem:mem_countableInfClosure_fst"}

## Theorem: Choquet's capacitability theorem {#thm:IsPavingAnalytic.isCapacitable lean="MeasureTheory.IsPavingAnalytic.isCapacitable" uses="def:IsPavingAnalytic, def:IsCapacitable"}

Let $F$ be a set of sets of $\mathcal{X}$ and let $I$ be an $F$-capacity.
Suppose that $F$ contains the empty set and is closed under pairwise intersections and unions.
Then every $F$-analytic set is $I$-capacitable.

### Proof {uses="lem:isCapacitable_mem_countableInfClosure_countableSupClosure, lem:IsCompactSystem.infClosure, lem:IsCapacitable.fst"}

**Capacities and measures**

## Definition: Measure.capacity {#def:Measure.capacity lean="MeasureTheory.Measure.capacity" uses="def:Capacity"}

Every finite measure defines a capacity by $I(s) = \mu(s)$ (where $\mu(s)$ is the value of the outer measure defined by $\mu$, but in Lean that's how $\mu(s)$ is defined already).

## Lemma: isCapacitable_measure_iff {#lem:isCapacitable_measure_iff lean="MeasureTheory.isCapacitable_measure_iff" uses="def:IsCapacitable, def:Measure.capacity"}

A set is capacitable with respect to the capacity defined by a finite measure if and only if it is null-measurable for this measure.

## Lemma: IsPavingAnalytic.nullMeasurableSet {#lem:IsPavingAnalytic.nullMeasurableSet lean="MeasureTheory.IsPavingAnalytic.nullMeasurableSet" uses="def:IsPavingAnalytic"}

An $M_{\mathcal{X}}$-analytic set of a measurable space $\mathcal{X}$ is universally measurable: it is null-measurable for every finite measure on $\mathcal{X}$.

### Proof {uses="thm:IsPavingAnalytic.isCapacitable, def:Measure.capacity, lem:isCapacitable_measure_iff"}

## Lemma: IsMeasurableAnalytic.nullMeasurableSet {#lem:IsMeasurableAnalytic.nullMeasurableSet lean="MeasureTheory.IsMeasurableAnalytic.nullMeasurableSet" uses="def:IsMeasurableAnalytic"}

A measurably analytic set of a measurable space $\mathcal{X}$ is universally measurable: it is null-measurable for every finite measure on $\mathcal{X}$.

### Proof {uses="lem:IsMeasurableAnalytic.isPavingAnalytic, lem:IsPavingAnalytic.nullMeasurableSet"}

## Theorem: Measurable projection {#thm:MeasurableSet.nullMeasurableSet_fst lean="MeasurableSet.nullMeasurableSet_fst" uses="def:IsMeasurableAnalytic"}

Let $\mathcal{X}$ and $\mathcal{Y}$ be measurable spaces, with $\mathcal{Y}$ standard Borel.
Then the projection of a measurable set of $\mathcal{X} \times \mathcal{Y}$ on $\mathcal{X}$ is universally measurable.

### Proof {uses="lem:IsMeasurableAnalyticFor.isMeasurableAnalytic, lem:IsMeasurableAnalytic.nullMeasurableSet"}

**Monotone class theorem**

## Definition: Monotone class {#def:monotone_class lean="MeasureTheory.MonotoneClass"}

Let $\mathcal{M}$ be a collection of subsets of a set $X$. We say that $\mathcal{M}$ is a monotone class if it is closed under countable monotone unions and countable monotone intersections, i.e.:

1. if \( A_1, A_2, \ldots \in M \) and \( A_1 \subseteq A_2 \subseteq \cdots \), then \( \bigcup_{i=1}^\infty A_i \in M \),
1. if \( B_1, B_2, \ldots \in M \) and \( B_1 \supseteq B_2 \supseteq \cdots \), then \( \bigcap_{i=1}^\infty B_i \in M \).

Given a collection $\mathcal{F}$ of subsets of $X$, we call the smallest monotone class containing $\mathcal{F}$ the monotone class generated by $\mathcal{F}$.

## Theorem: Monotone class theorem {#thm:monotone_class lean="MeasureTheory.MonotoneClass.generateFrom_eq" uses="def:monotone_class"}

Let \(G\) be an algebra of subsets of a set \(X\). Then the monotone class generated by \(G\) coincides with the $\sigma$-algebra generated by \(G\).

**Debut Theorem**

## Definition: Progressively measurable set {#def:progr_meas_set lean="MeasureTheory.ProgMeasurableSet" uses="def:IsStronglyProgressive"}

A subset of $[0, \infty) \times \Omega$ is progressively measurable if its indicator is a progressively measurable process.

## Definition: Debut of a set {#def:debut_set lean="MeasureTheory.debut"}

Let $E \subseteq{} [0, \infty) \times \Omega $, define $D_E = \inf\left\lbrace t \geq 0\ :\ (t, \omega) \in E\right\rbrace$, the debut of $E$.

## Theorem: debut_of_progr_meas_is_stop_time {#thm:debut_of_progr_meas_is_stop_time lean="MeasureTheory.isStoppingTime_debut" uses="def:progr_meas_set, def:debut_set, def:IsStoppingTime, def:hasUsualConditions"}

If $E$ is a progressively measurable set and the filtration satisfies the usual conditions, then $D_E$ is a stopping time.

### Proof {uses="thm:MeasurableSet.nullMeasurableSet_fst"}

**Hitting times**

## Theorem: hitting_is_stopping_time {#thm:hitting_is_stopping_time lean="MeasureTheory.isStoppingTime_hittingAfter'" uses="def:IsStoppingTime, def:hittingAfter, def:IsStronglyProgressive, def:hasUsualConditions"}

If $X : T \to \Omega \to E$ is a progressively measurable process with respect to a filtration satisfying the usual conditions and $B$ is a Borel-measurable subset of $E$, then the hitting time of $X$ in $B$ is a stopping time.

### Proof {uses="thm:debut_of_progr_meas_is_stop_time"}

Since $B$ is a Borel subset of $\mathcal{S}$ and $X$ is progressively measurable, then $\mathbf{1}_B(X_t)$ is also progressively measurable.
The hitting time is then the debut of the set $E = \{(s,\omega) : \mathbf{1}_B(X_s(\omega)) = 1\}$, and therefore is a stopping time by [debut_of_progr_meas_is_stop_time](#thm:debut_of_progr_meas_is_stop_time).

## Definition: leastGE {#def:leastGE lean="MeasureTheory.leastGE"}

_Upstream marks this `\mathlibok`: realized in mathlib itself._

Let $T$ be a conditionally complete linear order with a bottom element and let $R$ be a preorder.
For a process $X : T \to Ω \to R$ and $a \in R$, define the random time

$$
\begin{align*}
  \tau_{X \ge a} = \inf\{t \in T \mid X_t \ge a\} \: ,
\end{align*}
$$

in which the infimum is infinite if the set is empty.

## Lemma: isStoppingTime_leastGE {#lem:isStoppingTime_leastGE lean="MeasureTheory.isStoppingTime_leastGE" uses="def:IsStoppingTime, def:leastGE"}

Let $T$ be a conditionally complete linear order with a bottom element, which is a Polish space for its order topology, on which we put the Borel $\sigma$-algebra.
Let $R$ be a preorder with a metrizable topology for which sets of the form $\{x \in R \mid x \ge a\}$ are closed, with its Borel $\sigma$-algebra.
If $X : T \to Ω \to R$ is a progressively measurable process with respect to a filtration satisfying the usual conditions, then for any $a \in R$, the random time $\tau_{X \ge a}$ is a stopping time.

### Proof {uses="thm:hitting_is_stopping_time"}

This is a direct application of [hitting_is_stopping_time](#thm:hitting_is_stopping_time) with the set $B = [a, +\infty)$.

## Corollary: isStoppingTime_leastGE_of_rightContinuous {#cor:isStoppingTime_leastGE_of_rightContinuous uses="def:IsStoppingTime, def:leastGE, def:rightContinuous, def:adapted, def:RightContinuous"}

If $X : ι \to Ω \to ℝ$ is a right-continuous and adapted process with respect to a filtration satisfying the usual conditions, then for any $a \in \mathbb{R}$, the random time $\tau_{X \ge a}$ is a stopping time.

### Proof {uses="lem:isStoppingTime_leastGE, lem:Adapted.isStronglyProgressive_of_rightContinuous"}

This follows from [isStoppingTime_leastGE](#lem:isStoppingTime_leastGE) since $X$ is progressively measurable by [Adapted.isStronglyProgressive_of_rightContinuous](#lem:Adapted.isStronglyProgressive_of_rightContinuous).

## Definition: leastGT {#def:leastGT lean="MeasureTheory.leastGT"}

Let $T$ be a conditionally complete linear order with a bottom element and let $R$ be a preorder.
For a process $X : T \to Ω \to R$ and $a \in R$, define the random time

$$
\begin{align*}
  \tau_{X > a} = \inf\{t \in T \mid X_t > a\} \: ,
\end{align*}
$$

in which the infimum is infinite if the set is empty.

## Lemma: isStoppingTime_leastGT {#lem:isStoppingTime_leastGT lean="MeasureTheory.isStoppingTime_leastGT" uses="def:IsStoppingTime, def:leastGT"}

Let $T$ be a conditionally complete linear order with a bottom element, which is a Polish space for its order topology, on which we put the Borel $\sigma$-algebra.
Let $R$ be a preorder with a metrizable topology for which sets of the form $\{x \in R \mid x \ge a\}$ are closed, with its Borel $\sigma$-algebra.
If $X : T \to Ω \to R$ is a progressively measurable process with respect to a filtration satisfying the usual conditions, then for any $a \in R$, the random time $\tau_{X > a}$ is a stopping time.

### Proof {uses="thm:hitting_is_stopping_time"}

This is a direct application of [hitting_is_stopping_time](#thm:hitting_is_stopping_time) with the set $B = (a, +\infty)$.

## Lemma: leastGT_lt_iff {#lem:leastGT_lt_iff lean="MeasureTheory.leastGT_lt_iff" uses="def:leastGT"}

For $t \in T$, $\tau_{X > a} < t$ if and only if there exists $s < t$ such that $X_s > a$.

### Proof {uses="def:leastGT"}

