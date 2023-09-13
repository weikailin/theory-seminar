---
layout: page
title: 3. Pseudo-Randomness
nav_order: 3
nav_exclude: true
---

Indistinguishability and Pseudo-Randomness
=================

Recall the perfectly secure encryption, OTP. 
That is, we bitwise-XOR our message with a uniform random string.
OTP is inefficient because the long random string must be shared between Alice and Bob in advance.

Suppose that we have a (mathematical, deterministic) function 
that can extends a short truely random string to a long "random-looking" string.
We can use the seemingly random to encrypt messages as in OTP, yet it is efficient.

Is that possible?
How to formally define "random-looking"?

Let $g$ be the above function with short input $x$ and long output $g(x)$.
We want Alice and Bob share the same $g(x)$ to decrypt correctly, so $g$ must be deterministic. 
Mathematically, we have def for the distance between two probability distributions.
However, for any $|g(x)| \gt |x|$, the input / output distributions are far.
The point is "random-looking".

We will introduce computational indistinguishability, and then define pseudorandom generator (PRG) and pseudorandom function (PRF).

Computational Indistinguishability
------------------------

Key Idea:
If we have no way to show the difference, then we are satisfied. We call it indistinguishability.

Example: Turing test, when a machine and a human is indistinguishable in another human's prompts, we call it AI.
[Avi Wigderson]

Observation: they are *not* the same, not even close in any sense; 
however, the distinguisher "another human" can not tell the difference due to a limited power.

Concept: we say a distribution is pseudorandom if there is no efficient algorithm can distinguish it
from a (truely) uniform distribution.

We will formalize the concept asymptotically.

#### **Definition:** Ensembles of Probability Distributions

{: .defn}
> A sequence $\set{X_n}_{n\in\N}$ is called an *ensemble* if for each $n \in \N$, 
> $X_n$ is a probability distribution over $\bits$.
> (We often write $\cX = \set{X_n}_n$ when the context is clear.)

E.g., supposing $D_n$ is a distribution over $n$-bit strings for all $n\in\N$, $\set{D_n}_{n\in\N}$ is an ensemble.

#### **Definition:** Computational Indistinguishability

{: .defn}
> Let $\cX = \set{X_n}_n$ and $\cY = \set{Y_n}_n$ be ensembles 
> where $X_n, Y_n$ are distributions over $\bit^{\ell(n)}$ for some polynomial $\ell(·)$. 
> We say that $\cX$ and $\cY$ are *computationally indistinguishable*
> (denoted by $\cX \approx \cY$) 
> if for all NUPPT $D$ (called the “distinguisher”), there exists a negligible function $\eps$
> such that $\forall n \in \N$,
> 
> $$
> \Big| \Pr[t \gets X_n, D(t) = 1] − \Pr[t \gets Y_n, D(t) = 1] \Big| \lt \eps(n).
> $$


