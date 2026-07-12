---
title: "Gaussian measures"
type: "blueprint-chapter"
tags:
  - "blueprint"
---

Scaffold chapter, migrated from chapter 3 of the
[upstream blueprint](https://remydegenne.github.io/brownian-motion/blueprint/):
a small slice of the Gaussian theory, from the real Gaussian measure to the
characterization of Gaussian measures on a Banach space by their
characteristic functional. Dependency edges into material not yet migrated
(characteristic functions, chapter 1 upstream) are omitted until those
chapters exist here.

## Definition: Real Gaussian measure {#def:gaussianReal lean="ProbabilityTheory.gaussianReal"}

The real Gaussian measure with mean $\mu \in \mathbb{R}$ and variance
$\sigma^2 > 0$ is the measure on $\mathbb{R}$ with density
$\frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2 \sigma^2}\right)$
with respect to the Lebesgue measure. For $\sigma^2 = 0$ it is the Dirac
measure at $\mu$.

## Lemma: Characteristic function of a real Gaussian {#lem:charFun_gaussianReal lean="ProbabilityTheory.charFun_gaussianReal" uses="def:gaussianReal"}

The characteristic function of the real Gaussian measure with mean $\mu$ and
variance $\sigma^2$ is
$x \mapsto \exp\left(i\, \mu x - \frac{\sigma^2 x^2}{2}\right)$.

## Definition: Gaussian measure {#def:IsGaussian lean="ProbabilityTheory.IsGaussian" uses="def:gaussianReal"}

A measure $\mu$ on a separable Banach space $F$ is Gaussian if for every
continuous linear form $L \in F^*$, the pushforward measure $L_* \mu$ is a
Gaussian measure on $\mathbb{R}$.

## Theorem: Gaussian characterization by the characteristic functional {#thm:isGaussian_iff_charFunDual_eq lean="ProbabilityTheory.isGaussian_iff_charFunDual_eq" uses="def:IsGaussian"}

A finite measure $\mu$ on $F$ is Gaussian if and only if for every
$L \in F^*$ there are $m \in \mathbb{R}$ and $v \ge 0$ such that the
characteristic functional of $\mu$ at $L$ equals
$\exp\left(i\, m - \frac{v}{2}\right)$.
