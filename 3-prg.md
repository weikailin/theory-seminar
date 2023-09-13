---
layout: page
title: 3. Pseudo-Randomness
nav_order: 3
nav_exclude: true
---

$$
\newcommand{\wkxxx}{}
$$

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

Note: "=1" is a convention in literature. 

This definition requires the two distributions to pass *all efficient* statistical tests,
which include the following.
- Roughly as many 0 as 1.
- Roughly as many 01 as 10.
- Each sequence of bits occurs with roughly the same probability.
- Given any prefix, guessing the next bit correctly happens with roughly the same probability.

#### **Lemma:** Closure Under Efficient Operations

{: .defn}
> If the pair of ensembles $\set{X_n}_n \approx \set{Y_n}_n$, 
> then for any NUPPT $M$, $\set{M(X_n)}_n \approx \set{M(Y_n)}_n$.

{: .proof}
> (By standard reduction) 

#### **Lemma:** Hybrid Lemma

{: .defn}
> Let $X^{(1)}, X^{(2)}, ..., X^{(m)}$ be a sequence of probability distributions. 
> Assume that the machine $D$ distinguishes $X^{(1)}$ and $X^{(m)}$ with probability $p$. 
> Then there exists some $i \in \set{1, ..., m − 1}$ s.t. 
> $D$ distinguishes $X^{(1)}$ and $X^{(m)}$ with probability $p/m$.

{: .proof}
> (By triangular ineq) 

By this lemma, if $\cX \approx \cY$ and $\cY \approx \cZ$ for ensembles $\cX, \cY, \cZ$,
then it follows that $\cX \approx \cZ$.

Notice that this lemma applies to distributions (not ensembles).

Looking forward:
Consider two ensembles $\cX = \set{X_n}_n, \cY=\set{Y_n}_n$, and suppose that
the machine $D$ distinguishes $\cX, \cY$ w.p. $p(n)$ (that depends on $n$),
and then suppose that the sequence$X_n = X_n^{(1)}, ... , X_n^{(m(n))} = Y_n$
consists of $m(n)$ distributions such that $m$ is a polynomial of $n$.
Then, we *can not* define $m(n)$ ensembles between $\cX$ and $\cY$ due to the dependence of $m$ on $n$.
This is indeed the case when we have many hybrids, e.g., going from $(n+1)$-bit PRG to $m(n)$-bit PRG.
There are two ways to treat this case, the formal one and the more popular one.
In the formal way, we assume for contra that exists $D$ and $p(n)$ s.t. 
for inf many $n\in\N$, $D$ distinguishes $(X_n, Y_n)$ w.p. at least $p(n)$;
we then construct a reduction $B$ such that *guesses* an index $j \in [m(n)-1]$ 
and hoping that $j = i$, where $i$ is the index given by hybrid lemma, 
so that $B$ runs $D$ to distinguish and solve the challenge specified by the $j$-th hybrid.
The popular way is less rigorous but more intuitive:
we just claim that the two distributions $X_n^{(j)}, X_n^{(j+1)}$ are "indistinguishable"
for each $j, n$ (which is informal since $n$ is no longer asymptotic)
and thus $X_n, Y_n$ are "indistinguishable" (still informal).

