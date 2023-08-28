---
layout: page
title: One-Way Functions
nav_order: 2
nav_exclude: false
---

$
\newcommand{\Enc}{\mathsf{Enc}}
\newcommand{\Dec}{\mathsf{Dec}}
\newcommand{\Gen}{\mathsf{Gen}}
\newcommand{\cM}{\mathcal{M}}
\newcommand{\cK}{\mathcal{K}}
\newcommand{\cA}{\mathcal{A}}
\newcommand{\N}{\mathbb{N}}
\newcommand{\eps}{\epsilon}
\newcommand{\card}[1]{\vert{#1}\vert}
\newcommand{\set}[1]{\\{#1\\}}
\newcommand{\bit}{\set{0,1}}
\newcommand{\bits}{\bit^\*}
\newcommand{\mul}{\mathrm{mul}}
$

One-Way Functions
=================

Motivation:
Given the impossibility of efficient but perfectly secure encryption, we want to relax our security definition.
Intuitively, we want to

1. encrypt long plaintext many times using a single short key, and
2. perform "fast" encryption and decryption given the legitimate key, and
3. ensure that the recovering of plaintext is "hard" without the key.

One-time pads achieves 2 and 3 but not 1. However, OTP achieves 3 only bcs the key space is as large as message.
Since we want 1, the key space is relatively small.
Very vague, we want a encryption that is easy to compute (to achieve 1) but hard to find any $k,m$ that $\Enc_k(m) = c$.
(This is vague bcs we can still try any $k'$ to decrypt $c$.)

This suggests that we require functions that are 

> "easy" to compute but "hard" to invert.

That is called "one-wayness" in this lecture.
We next define easy and hard computation in terms of efficiency and probability.

Efficient Computation and Efficient Adversaries
------------------

We want to provide "efficient computation" to the honest users.

#### **Definition:** Deterministic Algorithm

{: .defn}
> An algo $\cA$ is a deterministic Turing Machine with input and output as bit strings, $\bit^*$.

Note: TM is by definition *uniform*, that is, its description size is constant for all unbounded long inputs.

#### **Definition:** Polynomial Running-Time

{: .defn}
> $\cA$ runs in time $T(n)$ if $\forall x \in \bits$, 
> $\cA(x)$ halts within $T(|x|)$ steps. 
> $\cA$ runs in *polynomial time* if there exists a constant $c$ such that $\cA$ runs
> in time $T(n) = n^c$.

#### **Definition:** Efficient Computation

{: .defn}
> We say an algo is *efficient* if it runs in polynomial time.

Justification of poly time:

- Indep of computation models (TM, circuit, ...)
- Closed under compositions of algos
- From human experience: poly-time become cubic, but super-poly remain hard

As discussed in perfect secrecy, we need randomized algo to construct encryption (and more generally crypto).

#### **Definition:** Randomized (or Probabilistic) Algorithm

{: .defn}
> A *randomized* algorithm $\cA$, also called a probabilistic polynomial-time Turing Machine
> and abbreviated as PPT, is a deterministic algorithm equipped with an extra random tape. 
> Each bit of the random tape is uniformly and independently chosen.
> 
> We denote the computation by $y \gets \cA(x ; r)$ but sometimes omit $r$.
> Note that the running-time is bounded by a poly for all $(x,r)$.

As an example, we define efficient and correct encryption.

#### **Definition:** Efficient Private-key Encryption.

{: .defn}
> $(\Gen, \Enc, \Dec)$ is called an *efficient private-key encryption scheme* if:
> 1. $k \gets \Gen(1^n)$ is PPT s.t. for every $n \in \N$, it samples $k$.
> 2. $c \gets \Enc_k(m)$ is PPT s.t. $k, m \in \bit^n$, outputs $c$.
> 3. $m \gets \Dec_k(c)$ is PPT s.t. $c, k$, outputs $m \in \bit^n \cup\bot$.
> 4. Correctness: $\forall n \in \N$, $m \in \bit^n$,
> 
> $$
> \Pr [k \gets Gen(1^n) : \Dec_k(\Enc_k(m)) = m]] = 1.
> $$

Note: the notation $1^n$ means the string of $n$ copies 1's, it is called the *security parameter*.
The purpose is to instantiate the "security" of the scheme, e.g., $n$-bit key.
We write unary $1^n$ (but not $n$ as binary) because "poly-time" is defined by the input length.

### Adversaries: Non-Uniform

Next we want to model adversaries with a stronger capability than honest.

#### **Definition:** Non-Uniform PPT

{: .defn}
> A *non-uniform* PPT machine (abbreviated nuPPT) $\cA$ is a sequence
> of algos $\cA = \set{\cA_1, \cA_2, \dots}$ s.t.:
> - $\cA_i$ computes on inputs of length $i$, and
> - exists a polynomial $d$ s.t. the description size $|A_i| \lt d(i)$ 
>   and the time $\cA_i$ is also less than $d(i)$. 
> We write $\cA(x)$ to denote the computation $\cA_{|x|}(x)$.
> 
> Alternatively, an nuPPT algo can be defined as a *uniform* PPT $\cA$ that
> takes an additional *advice* string for each input length $i$.

Purpose: 
non-uniform gives adv extra power and models many real scenario, 
e.g., Eve may have a list of known (plain, cipher) pairs.

Discuss: the advice may not be computable in poly time 
(if poly-time, then no need to take advice as input). NU is closed under reduction.

Definition of One-Way Functions
------------------

We try to define OWF using efficient computation and efficient adversary.

The first may come from NP-hardness.

#### **Attempt:** (Worst-Case)
> A function $f : \bits \to \bits$ is one-way if both of the following hold:
> 1. Easy to compute. There is a PPT $C$ that computes $f (x)$ on all inputs $x \in \bits$.
> 2. Hard to Invert. No nuPPT adversary $\cA$, for all $n\in\N$ and $x \in \bit^n$, 
> 
>    $$
>    \Pr[\cA(1^n, f (x)) \in f^{-1}( f (x))] = 1.
>    $$

Equivalent to the long-open complexity problem: $NP \notin BPP$ and thus $NP \neq P$.
Majority of $x$ are easy (even we set prob > 1/2), open if it is useful for encryption.

Note: nuPPT can store any poly, so more than poly are hard.

#### **Attempt:**
> A function $f : \bits \to \bits$ is one-way if both of the following hold:
> 1. Easy to compute. There is a PPT $C$ that computes $f (x)$ on all inputs $x \in \bits$.
> 2. Hard to Invert. For all nuPPT adversary $\cA$, for all $n\in\N$ and $x \in \bit^n$, 
> 
>    $$
>    \Pr[\cA(1^n, f (x)) \in f^{-1}( f (x))] \leq 2^{-n}.
>    $$

Impossible: too strong, $\cA$ is nu and could have many $(x, f(x))$ pairs. 
Note: $\cA$ takes $1^n$ as the security parameter in case $|f(x)| \ll n$.

Randomize $x$:

#### **Attempt:**

> 2\. Hard to Invert. For any nuPPT adversary $\cA$, for all $n\in\N$, and $x \in \bit^n$, 
> 
>    $$
>    \Pr[x \gets \bit^n; y \gets f(x) : f(\cA(1^n, y)) = y] \leq 2^{-n}.
>    $$

Still too strong: $\cA$ can take poly time to slash some of the possible $x$.

We may relax by $poly(n) / 2^n$ or $2^{-0.1 n}$ on the RHS, but they still too strong to find a candidate.
We formalize "very small" as follows.

#### **Definition:** Negligible Function

{: .defn}
> Func $\eps(n)$ is *negligible* if for every $c$, there exists some $n_0$ s.t.
> $\forall n > n_0, \eps(n) \le 1/n^c$.

Note: $\eps$ is smaller than any inverse poly for sufficiently large $n$.

#### **Definition:** (Strong) One-Way Function

{: .defn}
> A function $f : \bits \to \bits$ is *one-way* if both of the following hold:
> 1. Easy to compute. There is a PPT $C$ that computes $f (x)$ on all inputs $x \in \bits$.
> 2. Hard to Invert. For any nuPPT adversary $\cA$, there exists a negligible function $\eps$ 
>    that for any $n\in\N$,
> 
>    $$
>    \Pr[x \gets \bit^n; y \gets f(x) : f(\cA(1^n, y)) = y] \leq \eps(n).
>    $$

Note: each $\cA$ has a different $\eps$. The definition is asymptotic.

The above definition is standard in literature, but it is still hard to construct:
any adversary can only invert a tiny fraction.
Many natural candidates, such as factoring, does not meet this.
We relax it:

#### **Definition:** Weak One-Way Function

{: .defn}
> A function $f : \bits \to \bits$ is *weak one-way* if (... same as strong OWF.)
> 
> 2\. Hard to Invert. There exists a polynomial $q: \N \to \N$ such that for any nuPPT adversary $\cA$, 
>    for sufficiently large $n\in \N$,
> 
>    $$
>    \Pr[x \gets \bit^n; y \gets f(x) : f(\cA(1^n, y)) = y] \leq 1 - q(n).
>    $$


Primes and Factoring
--------------------

Define $f_\mul: \N^2 \to \N$ by

$$
f_\mul(x,y) = \begin{cases}
1  & \text{if } x = 1 \text{ or } y = 1 \text{( to eliminate trivial inversion)}\\
x \cdot y & \text{o.w.}
\end{cases}
$$

Easy to compute. For many $(x,y)$ are "easy" to invert: w.p. at least 3/4 when $xy$ even.
It is not strong OWF.

#### **Assumption:** Factoring

{: .defn}
> For any adv $\cA$, there exists a negligible function $\eps$ s.t.
> 
> $$
> \Pr[(p,q) \gets \Pi_n^2; N \gets pq : \cA(N) \in \set{p,q}] \lt \eps(n),
> $$
> 
> where $\Pi_n := \set{p \lt 2^n : p \text{ prime}}$ is the set of primes less than $2^n$.

### The Prime Number Theorem

Define $\pi(x)$ as the number of primes $\le x$.

#### **Theorem:** (Chebychev, 1848)

{: .theorem}
> For all $x>1$, $\pi(x) \gt \frac{x}{2 \log x}$.

Note: the above is easier to prove, but the famous *Prime Number Theorem* is $\pi(x) \approx x / \ln x$ when $x \to \infty$.
The above $\log$ is base 2 since 2 is the smallest prime.

#### **Theorem:**

{: .theorem}
> If the factoring assumption is true, then $f_\mul$ is a weak OWF.

{: .proof} 
> $f_\mul$ is easy to compute. Hard to invert?
> 
> Assume for contradiction (AC), for all poly $q$, exists nuPPT $A$, s.t. for infinitely many $n\in \N$,
> 
> $$
> \Pr[(x,y)\gets \bit^n; z = xy : A(1^{2n}, z) \in \set{x,y}] \gt 1- \frac{1}{q(n)}.
> $$
> 
> Note: the negation of weak OWF.
> 
> Then, we construct an adversary $B$ breaks factoring.
> 
> {: .defn-title}
>> Algorithm $B(z)$:
>> 
>> 1. Sample $(x,y) \gets \bit^n$
>> 2. If both $x,y$ prime, let $\bar z \gets z$; otherwise, let $\bar z \gets f_\mul(x,y)$.
>> 3. Run $\bar x \gets A(1^{2n}, \bar z)$
>> 4. Output $\bar x$ if both $x,y$ are prime.
> 
> We intentionally make the input to $A$ uniform in $\bit^{2n}$.
> 
> By Chebychev, both $x,y$ prime w.p. $\gt 1/ (2 \log 2^n)^{2} = 1/(4n^2)$.
> Hence, $B$ fails to pass $z$ to $A$ w.p. at most $1 - 1/(4n^2)$.
> 
> By eq (AC), $A$ fails to invert $\bar z$ w.p. at most $1/q(n)$. Choose $q(n) = 1/8n^2$ and $A$ correspondingly.
> 
> By union bound, the failure probability of $B$ is at most $1 - 1/(4n^2)+1/8n^2$, 
> and thus $B$ breaks factoring w.p. at least $1/8n^2$, greater than negl, contradicting Factoring Assumption.

Note: the above reduction assumes efficient primality testing. That is not necessary, left as exercise.

Note: the pattern is common in crypto.
Reduction *from* Assumption (factoring) *to* Construction (OWF) is bread and butter in this course.


Reduction from weak to strong OWF

Idea: repeat independently weak poly many times.

Let $f$ be weak OWF s.t. no adv can invert w.p. $1-1/q$ where $q$ is a function of $n$.



Weak OWF?

Basic number theory, DL assumption

OWP

Universal OWF


