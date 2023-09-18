---
layout: page
title: 3. Pseudo-Randomness
nav_order: 3
nav_exclude: false
---

$
\newcommand{\wkxxx}{[WK: xxx]}
$

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

We will introduce computational indistinguishability, and then define pseudo-random generator (PRG) and pseudo-random function (PRF).

Computational Indistinguishability
------------------------

Key Idea:
If we have no way to show the difference, then we are satisfied. We call it indistinguishability.

Example: Turing test, when a machine and a human is indistinguishable in *every* human's prompts, we call it AI.
- [Turing 1950, Computing machinery and intelligence](https://link.springer.com/chapter/10.1007/978-1-4020-6710-5_3)
- [Wigderson 2022, Imitation game](https://www.youtube.com/watch?v=JZH1AT1kdK8)

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
> Remove the absolute value in the def of comp. ind. by negating the distinguisher $D$,
> and then standard probability. 

Note: the converse the easier to prove. Hence, prediction and distinguishing is essentially equivalent.

Pseudo-Random Generator 
------------------------

#### **Definition:** Pseudo-random Ensembles.

{: .defn}
> The probability ensemble $\set{X_n}_n$, where $X_n$ is a probability distribution
> over $\bit^{l(n)}$ for some polynomial $l(\cdot)$, is said to be pseudorandom 
> if $\set{X_n}_n \approx \set{U_{l(n)}}_n$,
> where $U_m$ is the uniform distribution over $\bit^m$.

Note:
- this definition says that a pseudorandom distribution must pass 
  **all** efficiently computable tests that the uniform distribution would have passesd.
- it is hard to check or prove if a distribution is pseudorandom 
  (due to the "for all" quantifier from comp. ind.)

#### **Definition:** Pseudo-random Generators.

{: .defn}
> A function $g : \bit^\ast \to \bit^\ast$ is a *Pseudo-random Generator (PRG)* 
> if the following holds.
> 1. (efficiency): $g$ can be computed in PPT.
> 2. (expansion): 
>    $|g(x)| \gt |x|$
> 3. The ensemble $\set{x \gets U_n : g(x)}_n$ is pseudorandom.

We sometimes say that the expansion of PRG $g$ is $t$ 
if $|g(x)| - |x| \ge t$ for all $x$.

Example: if $g: \bit^n \to \bit^{n+1}$ for all $n$ is a PRG, then $g$ is a OWF.
(proof left as exercise, why expansion is necessary?)

#### **Lemma:** Expansion of a PRG

{:.theorem}
> Let $g:\bit^n \to \bit^{n+1}$ to be a PRG. 
> For any polynomial $\ell$, define $g': \bit^n \to \bit^{\ell(n)}$ as follows:
> 
> $$
> g'(s) \to b_1 b_2 ... b_{\ell(n)},
> $$
> 
> where 
> $X_0 \gets s, x_{i+1} \| b_{i+1} \gets g(x_i)$. Then $g'$ is a PRG.

{:.proof-title}
> Proof, warmup:
> 
> Suppose that $\ell = 2$, no expansion, but we want to show pseudorandomness.
> Define distributions $H^0_n := g'(s), H^1_n := u_1 \\| g(U_n)[n+1], H^2_n := U_2$ for $n \in \N$.
> Since $g'(s) = g(s)[n+1] \\| g(g(s)[1...n])[n+1]$, by $g(s) \approx U_{n+1}$ and closure,
> we have $\cH^0 \approx \cH^1$.
> By $g(x)$ is pseudorandom and closure, $g(U_n)[n+1] \approx U_1$, which implies $\cH^1 \approx \cH^2$.
> By (the corollary of) hybrid lemma, we have $\cH^0 \approx \cH^2$.

{:.proof}
> It is slightly tricky when $\ell$ depends on $n$.
> 



<!-- > 
> Assume for contra, there is a NUPPT distinguisher $D$ and poly $p$ s.t. for inf many $n$,
> $D$ distinguishes ensembles $\cH^0, \cH^2$ w.p. $\ge 1/p(n)$.
> Then, by hybrid lemma, there ex -->