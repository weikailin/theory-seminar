---
layout: page
title: 3. Pseudo-Randomness
nav_order: 3
nav_exclude: false
---

$$
\newcommand{\wkxxx}{}
$$

Indistinguishability and Pseudo-Randomness
==========================================

Recall the perfectly secure encryption, OTP. 
That is, we bitwise-XOR our message with a uniform random string.

$$
m \oplus k, ~ |m| = |k|.
$$

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
The point is "random-looking" at best.

$$
m \oplus g(s), ~ |m| = |g(s)|, \text{ but } |s| \ll |m|.
$$

We will introduce computational indistinguishability, and then define pseudorandom generator (PRG) and pseudorandom function (PRF).

Computational Indistinguishability
------------------------

Key Idea:
If we have no way to show the difference, then we are satisfied. We call it indistinguishability.

Example: Turing test, when a machine and a human is indistinguishable in *every* human's prompts, we call it AI.
- [Turing 50, Computing machinery and intelligence](https://link.springer.com/chapter/10.1007/978-1-4020-6710-5_3)
- [Wigderson 22, Imitation game](https://www.youtube.com/watch?v=JZH1AT1kdK8)

Observation: they are *not* the same, not even close in any sense; 
however, the distinguisher "another human" can not tell the difference due to a limited power.

Concept: we say a distribution is pseudorandom if for *every* efficient algorithm,
it can not be distinguished from a (truely) uniform distribution.

We will formalize the concept asymptotically.

#### **Definition:** Ensembles of Probability Distributions

{: .defn}
> A sequence $\set{X_n}_{n\in\N}$ is called an *ensemble* if for each $n \in \N$, 
> $X_n$ is a probability distribution over $\bits$.
> (We often write $\cX = \set{X_n}_n$ when the context is clear.)

E.g., supposing $X_n$ is a distribution over $n$-bit strings for all $n\in\N$, $\set{X_n}_{n\in\N}$ is an ensemble.

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

Note: 
- "=1" is a convention in literature
- "absolute" is not necessary due to "for all D"

This definition requires the two distributions to pass *all efficient* statistical tests,
which include the following.
- Roughly as many 0 as 1.
- Roughly as many 01 as 10.
- Each sequence of bits occurs with roughly the same probability.
- Given any prefix, guessing the next bit correctly happens with roughly the same probability.

#### **Lemma:** Closure Under Efficient Operations

{: .theorem}
> If the pair of ensembles $\set{X_n}_n \approx \set{Y_n}_n$, 
> then for any NUPPT $M$, $\set{M(X_n)}_n \approx \set{M(Y_n)}_n$.

{: .proof}
> (By standard reduction) 

Examples:

1. $M$ ignores its input. Clearly, $M(X_n) \equiv M(Y_n)$ for all $n$.
2. $M$ is identity, i.e., its output is exactly the input. $\set{M(X_n) = X_n}_n \approx \set{M(Y_n)=Y_n}_n$.
3. $M$ outputs the first half of the input, i.e., $M(x) := x[1, ..., |x|/2]$.

#### **Lemma:** Hybrid Lemma

{: .theorem}
> Let $X^{(1)}, X^{(2)}, ..., X^{(m)}$ be a sequence of probability distributions. 
> Assume that the machine $D$ distinguishes $X^{(1)}$ and $X^{(m)}$ with probability $p$. 
> Then there exists some $i \in \set{1, ..., m − 1}$ s.t. 
> $D$ distinguishes $X^{(1)}$ and $X^{(m)}$ with probability $p/m$.

{: .proof}
> (By triangular ineq) 

Notice that this lemma applies to distributions, *not ensembles*.
Fortunately, it implies the following.

#### **Corollary:**

{: .theorem}
> For any ensembles $\cX, \cY, \cZ$, if $\cX \approx \cY$ and $\cY \approx \cZ$,
> then it follows that $\cX \approx \cZ$.

{: .proof}
> (left as exercise)

**Notice**{: .label}
If the number of hybrid distributions (between two ensembles) depends on 
the size $n$ (of the distributions in the ensembles), the above corollary is tricky.
Consider two ensembles $\cX = \set{X_n}_n, \cY=\set{Y_n}_n$, and suppose that
the machine $D$ distinguishes $\cX, \cY$ w.p. $p(n)$ (that depends on $n$),
and then suppose that the sequence $(X_n = X_n^{(1)}, ... , X_n^{(m(n))} = Y_n)$
consists of $m(n)$ distributions such that $m$ depends on $n$.
Then, we *can not* define $m(n)$ ensembles between $\cX$ and $\cY$ due to the dependence 
(i.e., the length of the sequence depends on $n$).
This is indeed the case when we have many hybrids, e.g., going from $(n+1)$-bit PRG to $2n$-bit PRG.
There are two ways to treat this case, the formal one and the more popular one.
In the formal way, we assume for contra that exists $D$ and $p(n)$ s.t. 
for inf many $n\in\N$, $D$ distinguishes $(X_n, Y_n)$ w.p. at least $p(n)$;
we then construct a reduction $B$ such that *guesses* an index $j \in [m(n)-1]$ 
and hoping that $j = i$, where $i$ is the index given by hybrid lemma, 
so that $B$ runs $D$ to distinguish and solve the challenge specified by the $j$-th hybrid.
The popular way is less rigorous but more intuitive:
we just claim that the two distributions $X_n^{(j)}, X_n^{(j+1)}$ are "indistinguishable"
for each $j, n$, and thus $X_n, Y_n$ are "indistinguishable";
this is informal because fixing any $j$ means that $n$ is also fixed and $X_n, Y_n$ are two distributions (not ensembles), 
but indistinguishability is defined asymptotically on ensembles.

Example:
Let $\cX, \cY, \cZ, \cZ'$ be ensembles.
Suppose that $(\cX, \cZ) \approx (\cX, \cZ')$ and $(\cY, \cZ) \approx (\cY, \cZ')$.
Does $(\cX, \cY, \cZ) \approx (\cX, \cY, \cZ')$?

#### **Lemma:** Prediction Lemma

{: .theorem}
> Let $\set{X^0_n}_n$ and $\set{X^1_n}_n$ be two ensembles where $X^0_n, X^1_n$ are 
> probability distributions over $\bit^{\ell(n)}$ for some polynomial $\ell(\cdot)$, 
> and let $D$ be a NUPPT machine that distinguishes between $\set{X^0_n}_n$ and $\set{X^1_n}_n$
> with probability $\ge p(·)$ for infinitely many $n \in \N$.
> Then there exists a NUPPT $A$ such that
> 
> $$
> \Pr[b \gets \bit, t \gets X^b_n : A(t) = b] \ge \frac{1}{2} + \frac{p(n)}{2}
> $$
> 
> for infinitely many $n \in \N$.

{: .proof}
> Remove the absolute value in the def of CI by negating the distinguisher $D$,
> and then standard probability. 

Note: the converse the easier to prove. Hence, prediction and distinguishing is essentially equivalent.


