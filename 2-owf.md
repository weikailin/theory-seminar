---
layout: page
title: 2. One-Way Functions
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
> \Pr [k \gets \Gen(1^n) : \Dec_k(\Enc_k(m)) = m]] = 1.
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
> takes an additional *advice* string of poly length $d(i)$ for each input length $i$.

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

This is implied by $NP \not\subseteq BPP$, which is
a long-open complexity problem.
Majority of $x$ are easy (even we set prob $\ge 1 - 1/poly$), open if it is useful for encryption.

Note: nuPPT can store any poly, so there may be more than poly are hard.

#### **Attempt:**
> A function $f : \bits \to \bits$ is one-way if both of the following hold:
> 1. Easy to compute. There is a PPT $C$ that computes $f (x)$ on all inputs $x \in \bits$.
> 2. Hard to Invert. For all nuPPT adversary $\cA$, for all $n\in\N$ and $x \in \bit^n$, 
> 
>    $$
>    \Pr[\cA(1^n, f (x)) \in f^{-1}( f (x))] \leq 2^{-n}.
>    $$

Impossible: too strong, $\cA$ is NU and could have many $(x, f(x))$ pairs. 
Note: $\cA$ takes $1^n$ as the security parameter in case $|f(x)| \ll n$.

Randomize $x$:

#### **Attempt:**

> 2\. Hard to Invert. For any nuPPT adversary $\cA$, for all $n\in\N$, 
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

Note: when the probability is $\ge 1-\eps(n)$, we often call it "overwhelming".

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
>    \Pr[x \gets \bit^n; y \gets f(x) : f(\cA(1^n, y)) = y] \leq 1 - 1/q(n).
>    $$

Note: here the prob. $1-1/q$ is *the same* for all adv $\cA$, 
but in the strong OWF, the prob. $\eps$ is different and *depends* on $\cA$.

Primes and Factoring
--------------------

Define $f_\mul: \N^2 \to \N$ by

$$
f_\mul(x,y) = \begin{cases}
1  & \text{if } x = 1 \text{ or } y = 1 \text{(eliminating trivial invert)}\\
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
PNT states that primes are dense.

#### **Theorem:** (Chebychev, 1848)

{: .theorem}
> For all $x>1$, $\pi(x) \gt \frac{x}{2 \log x}$.

Note: the above is easier to prove, but the famous *Prime Number Theorem* is $\pi(x) \sim x / \ln x$ when $x \to \infty$.
The above $\log$ is base 2.

#### **Theorem:**

{: .theorem}
> If the factoring assumption is true, then $f_\mul$ is a weak OWF.

{: .proof} 
> $f_\mul$ is easy to compute. Hard to invert?
> 
> Assume for contradiction (AC), for all poly $q$, exists nuPPT $A$, s.t. for infinitely many $n\in \N$,
> 
> $$
> \Pr[(x,y)\gets \bit^n; z = xy : f_\mul(A(1^{2n}, z)) = z] \gt 1- \frac{1}{q(n)}.
> $$
> 
> Note: the negation of weak OWF.
> 
> Then, we construct an adversary $B$ breaks factoring.
> 
> {: .defn-title}
>> Algorithm $B(1^{2n}, z)$:
>> 
>> 1. Sample $(x,y) \gets \bit^n$
>> 2. If both $x,y$ prime, let $\bar z \gets z$; otherwise, let $\bar z \gets f_\mul(x,y)$.
>> 3. Run $(\bar x, \bar y) \gets A(1^{2n}, \bar z)$
>> 4. Output $(\bar x, \bar y)$ if both $x,y$ are prime and $z = \bar x \bar y$.
> 
> We intentionally make the input to $A$ uniform in $\bit^{2n}$.
> 
> By Chebychev, both $x,y$ prime w.p. $\gt 1/ (2 \log 2^n)^{2} = 1/(4n^2)$.
> Hence, $B$ fails to pass $z$ to $A$ w.p. at most $1 - 1/(4n^2)$.
> 
> By eq (AC), $A$ fails to invert $\bar z$ w.p. at most $1/q(n)$. Choose $q(n) := 8n^2$ and $A$ correspondingly.
> 
> By union bound, the failure probability of $B$ is at most 
> 
> $$
> \Pr[z\neq \bar z \cup A \text{ fails}] 
> \le \Pr[z\neq \bar z] + \Pr[A \text{ fails}] 
> \le 1 - 1/(4n^2)+1/8n^2 = 1 - 1/8n^2,
> $$ 
> 
> and thus $B$ breaks factoring w.p. at least $1/8n^2$, greater than negl, contradicting Factoring Assumption.

Note: the above reduction assumes efficient primality testing. That is not necessary, left as exercise.

Note: the pattern is common in crypto.
Reduction *from* Assumption (factoring) *to* Construction (OWF) is bread and butter in this course.

## From Weak OWF to Strong OWF

The existence of OWF is long-open.
We will show that strong and weak OWFs are existentially equivalent.
Clearly, any strong OWF satisfies weak. The challenge is from weak to strong.

We begin with a warmup.

#### **Claim:**

{: .theorem}
> If $\set{f_n: \bit^n \to \bit^l}_{n\in\N}$ is a strong OWF, 
> then $g(x_1,x_2) := (f(x_1), f(x_2))$ is also a strong OWF.

{: .proof}
> Assume for contradiction (AC), there exist poly $p(n)$ and a nuPPT adv $A$ such that 
> for infinitely many $n\in\N$, 
> 
> $$
> \Pr[x_1,x_2 \gets \bit^n; y = g(x_1,x_2) : g(A(1^{2n}, y)) = y] \gt 1/p(n).
> $$
> 
> We construct nuPPT $B$ that inverts $f$.
> 
>> Algorithm $B(1^n, y)$:
>> 1. $x_2 \gets \bit^n$ and $y_2 = f(x_2)$.
>> 2. Run $x'_1, x'_2 \gets A(1^{2n}, (y,y_2))$.
>> 3. Output $x'_1$ if $f(x'_1) = y$.
> 
> For uniform $z\gets \bit^n$, the above $(y,y_2)$ is the same distribution 
> as obtaining the output $g(x_1,x_2)$ by sampling $(x_1,x_2)\gets \bit^{2n}$.
> 
> Also, when $A$ inverts $(y,y_2)$, we have that $B$ inverts $z$ successfully.
> By (AC), $A$ inverts w.p. $\gt 1/p$, greater than any negligible function, 
> and it contradicts that $f$ is a strong OWF.

Note: this is a typical template to prove security by reduction. 
The quantifiers of (AC) is often the same (to negate negligible).

Observation: the definition of weak states that *exist* poly $q(n)$ *for all* nuPPT;
that is, even weak, there is a good fraction, $1/q$, of instances that are hard for all.

Idea: we repeat the weak $f$ for poly many instances and ask the Adv to invert all,
so that Adv fails with high prob.

#### **Theorem:**

{: .theorem}
> For any weak OWF $f_n: \bit^n \to \bit^l$, there exists a poly $m(n)$ such that 
> 
> $$
> g(x_1, ..., x_m) := (f(x_1), ..., f(x_m))
> $$
> 
> from $g: \bit^{mn} \to \bit^{ml}$ is a strong OWF.

Note: by def, there exists a poly $q(n)$ s.t. no adv can invert $f$ w.p. $1-1/q(n)$.

#### **Proof:**

Assume for contradiction (AC), there exists a nuPPT adv $A$ and poly $p(n)$ 
s.t. for inf many $n\in\N$, $A$ inverts $g$ w.p. $\ge 1/p$, i.e.,

$$
\Pr[\set{x_i\gets\bit^n, y_i \gets f(x_i)}_{i\in[m]}, y \gets (y_1...y_m) : g(A(1^n, y)) = y] \ge 1/p(n).
$$

We want to construct a nuPPT $B$ to invert $y=f(x)$ for uniform $x \gets \bit^n$ by running $A$.
So, the idea is to transform $y$ into an output of $g$, that is $(y_1,..., y_m)$.
How? $(y,y, ..., y)$? $(y,y_2, ..., y_m)$? 

We construct $B_0$ as below to run $A$.

{: .defn}
> Algorithm $B_0(1^n, y)$:
> 
> 1. $j \gets [m]$
> 2. $x_1, ..., x_m \gets \bit^{n}$
> 3. let $y_i \gets f(x_i)$ for all $i$
> 4. let $y_j \gets y$
> 5. run $x'_1, .., x'_m \gets A(1^{mn}, (y_1,..., y_m))$
> 6. if $f(x'_j) = y$, output $x_j$, otherwise output $\bot$.

Note: $B_0$ inverts $y$ w.p. roughly $1/p$ by (AC), but our goal is to invert w.p. $1-1/q \gg 1/p$.
Hence, repeating $B_0(y)$ is necessary.

{: .defn}
> Algorithm $B(1^n, y)$:
> 
> 1. repeatedly run $B_0(y)$ poly $r_1(n)$ many times using fresh randomness
> 2. output the first non $\bot$ output of $B_0$.

Note: we use the same $y$ as input, and that makes the probability analysis involved 
since the repetition is *dependent*.

By (AC), inverting $g$ is easy, intuitively there are many $(x,y=f(x))$ that can be inverted by $B_0(y)$.
Clearly that holds for $A$, but as mentioned, we need to prove it for $B_0$.

The following claim is the key.

#### **Claim:** (many easy instances)

{: .theorem}
> Suppose that (AC) holds.
> There exists a "large" set $G_n$ of "easy" instances, 
> 
> $$
> G_n := \set{x \in \bit^n : \Pr_{x, y=f(x)}[f(B_0(y)) = y] \geq 1/r_2(n)}
> $$
> 
> for some poly $r_2(n)$, 
> and $|G| \geq (1 - 1/2q)\cdot 2^n$.

If the claim holds, then $B$ can invert by repeating $B_0$:

$$
\newcommand{\tinv}{\text{ inv}}
\newcommand{\tnotinv}{\text{ not}\tinv}
\newcommand{\tall}{\text{all }}
\newcommand{\tsome}{\text{some }}
\begin{align*}
\Pr_{x,y}[B \tnotinv] 
 & = \Pr[B \tnotinv \cap x \in G] + \Pr[B \tnotinv \cap x \notin G] \\
 & \le \Pr[B \tnotinv | x \in G] + \Pr[x \notin G] \\
 & \le (1-1/r_2)^{r_1} + 1/2q \\
 & \le e^{-n} + 1/2q \le 1/q
\end{align*}
$$

We will choose $r_1(n) := n \cdot r_2(n)$ to get $(1-1/r_2)^{r_1} \le e^{-n}$.

Then, $B$ inverts w.p. $\gt 1-1/q$, and it is contradicting that $f$ is weak OWF.
It remains to prove the claim.

{: .proof-title}
> Proof of Claim:
> 
> Intuition: $G_n$ is $B_0$, but essentially $B_0$ is running $A$.
> If $G_0$ is small, then $A$ should not invert w.p. $\ge 1/p$, and thus contra (AC).
> 
> Assume for contra (AC2), 
> $|G_0| \lt (1-1/2q) \cdot 2^n$. 
> We have 
> 
> $$
> \Pr[ A \tinv] = \Pr[A \tinv \cap \tall x_i \in G_n] + \Pr[A \tinv \cap \tsome x_i \notin G_n]
> $$
> 
> Since the "easy" set $G_n$ is small, it is unlikely all $x_i$ are easy.
> Formally, by (AC2)
> 
> $$
> \begin{align*}
> \Pr[A \tinv \cap \tall x_i \in G] \le \Pr[\tall x_i \in G] \le (1-1/2q)^m \le e^{-n}.
> \end{align*}
> $$
> 
> Note: this is where the repetition $m$ kicks in (in the construction of $g$), 
> and we choose $m(n) := n \cdot 2q(n)$ to get the ineq.
> 
> Also, by union bound,
> 
> $$
> \begin{align*}
> \Pr[A \tinv \cap \tsome x_i \notin G]
> \le \sum_i \Pr[A \tinv \cap x_i \notin G]
> \le \sum_i \Pr[A \tinv | x_i \notin G]
> \end{align*}
> $$
> 
> Observe that 
> $\Pr[A \tinv | x_i \notin G]$ is very close to $\Pr[B_0(y) \tinv | x \notin G]$ as that of the claim. 
> The only difference is that $B_0$ plant $y$ in random position.
> Indeed, for any fixed $i \in [m]$,
> 
> $$
> \begin{align*}
> \Pr[x_1,...,x_m\gets\bit^n, y_1\gets f(x_1), ..., y_m\gets f(x_m): A(y_1,...,y_m) \tinv | x_i \notin G]\\
> = \Pr[j\gets[m] \text{ in } B : B_0(y) \tinv | x \notin G \cap j = i]
> \end{align*}
> $$
> 
> and thus
> 
> $$
> \begin{align*}
> &\Pr[B_0 \tinv | x \notin G] \\
> &= \sum_i \Pr[B_0 \tinv \cap j = i | x \notin G] \\
> &= \sum_i \Pr[B_0 \tinv \cap j = i \cap x \notin G] / \Pr[x \notin G] \\
> &= \sum_i \Pr[B_0 \tinv | j = i \cap x \notin G] \cdot \left(\Pr[j = i \cap x \notin G] / \Pr[x \notin G]\right)\\
> &= \sum_i \Pr[A \tinv | x_i \notin G] \Pr[j=i] = (1/m) \sum_i \Pr[A \tinv | x_i \notin G]
> \end{align*}
> $$
> 
> We thus conclude
> 
> $$
> \begin{align*}
> \Pr[A \tinv \cap \tsome x_i \notin G]
> \le m \cdot \Pr[B_0 \tinv | x \notin G]
> \lt m \cdot 1 / r_2.
> \end{align*}
> $$
> 
> and thus
> 
> $$
> \Pr[A \tinv] \lt e^{-n} + m \cdot 1/ r_2.
> $$
> 
> We choose $r_2(n) = 2m \cdot p(n)$ so that $\Pr[A \tinv] \lt 1/p$, contradicting (AC).


Primality Testing
--------------------



#### **Definition:** Group

{: .defn}
> A group $G$ is a set of elements with a binary operator
> $\ast$ that satisfies the following properties:
> 1. Closuer: $\forall a,b \in G, a \ast b \in G$
> 2. Identity: $\exists 1 \in G$ s.t. $\forall a \in G, 1 \ast a = a \ast 1 = a.
> 3. Associativity: $\forall a, b, c \in G, (a\ast b) \ast c = a \ast (b \ast c)$.
> 4. Inverse: $\forall a \in G, \exists b \in G$ s.t. $a \ast b = b \ast a = 1$.

#### **Definition:**

{: .defn}
> Let $Z_n^* := \set{a \in \N : a < n, \gcd(a,n)=1}$ be the multiplicative group modulo $n$.
> Let $\phi(n) := |Z_n^*|$ be the Euler's totient.

Note: $\phi(n) = p_1^{k_1-1}(p_1-1) \cdot p_2^{k_2-1}(p_2-1) ...$
for $n = p_1^{k_1} \cdot p_2^{k_2} ...$ where $p_i$ are distinct primes.

#### **Theorem:** (Euler)

{: .theorem}
> $$
> \forall n \in \N, \forall a \in Z_n^*, a^{\phi(n)} = 1 \mod n
> $$

{: .proof}
> Let $a \in Z_n^\ast$, and let $S := \set{ax : x \in Z_n^\ast}$.
> We have $S = Z_n^*$ (otherwise, we have $x_1 \neq x_2$ but $ax_1 = ax_2$, a contradiction given $a^{-1}$ exists).
> Then, by commutative (first eq),
> 
> $$
> \prod_{x \in Z_n^\ast} = \prod_{b \in S} b = \prod_{x \in Z_n^\ast} ax = a^{\phi(n)} \prod_{x \in Z_n^\ast}.
> $$
> 
> That implies $a^{\phi(n)} = 1$.

#### **Corollary:** (Fermat's Little Theorem)

{: .theorem}
> For all prime $p$,
> 
> $$
> \forall a \in Z_p^*, a^{p-1} = 1 \mod p
> $$

#### **Definition:**

{: .defn}
> For any composite $n \in \N$, we say that $a \in Z_n^\*$ 
> is a *witness* if $a^{n-1} \neq 1 \mod n$.

#### **Lemma:**

{: .theorem}
> For all $n\in \N$, if there exists a witness, then there are at least $\phi(n) / 2$ witnesses.

{: .proof}
> Let $H \subset Z_n^*$ be the subset of none witnesses.
> We have $1 \in H$, and $H$ is a subgroup modular $n$.
> Given that there exists a witness, $H$ is a strict subgroup.
> We can then show that any strict subgroup is at most half size of the supergroup,
> ie, $|H| \le \phi(n) / 2$.

#### **Definition:**

{: .defn}
> For any composite $n \in \N$, write $\phi(n) = 2^r \cdot d$ for some integer $r\in \N$ and odd $d$.
> We say that $a \in Z_n^\*$ 
> is a *strong* witness if 
> 
> $$
> a^d \neq \pm 1 \mod n ~\text{ and }~
> a^{2^i \cdot d} \neq -1 \mod n \text{ for all } i = 1,2,...,r-1
> $$

#### **Lemma:**

{: .theorem}
> If $a$ is a witness, then $a$ is also a strong witness.

{: .proof}
> Assume for contradiction that $a$ is not a strong witness.
> Then the sequence $a^d, a^{2d}, ..., a^{2^r d}$ is either
> - $(\pm 1, 1, 1, ..., 1)$, or
> - $(\star, \star, ..., -1, 1,1, ..., 1)$.
> Hence, $a$ is not a witness, a contradiction.


#### **Lemma:**

{: .theorem}
> If $n$ prime, then there is no strong witness in $Z_n^*$.

{: .proof}
> If $n$ prime, then the only solution to $x^2 = 1 \mod n$ is $\pm 1$ (need proof).
> By Fermat's Little Theorem, for any $a \in Z_n^*$, $a^{2^r d} = 1 \mod n$, and $a^{2^{r-1} d} = \pm 1 \mod n$.
> If $-1$, then it is not a strong witness.
> Otherwise, $1$, we can continue the next square root $r-2$, until $a^d$, which must be $\pm 1$.

It remains to show that every composite has many strong witnesses.
The first step is to exclude perfect powers.
The second step is to show that other composites have many strong witnesses.

#### **Lemma:**

{: .theorem}
> If $n$ is composite such that $n = n_1 \cdot n_2$ for some coprime $n_1,n_2$, 
> then there are at least half strong witness in $Z_n^*$.

{: .proof}
> Let $H$ be the subset of none-strong witnesses. 
> We will show that there exists $\bar H \supset H$ s.t. $\bar H$ is a strict subgroup of $Z_n^*$,
> which is sufficient.
> 
> For each $a \in H$, consider the sequence $a^d, a^{2d}, ..., a^{2^r d}$. 
> Let $j$ be the largest index such that $\exists a \in H, a^{2^j d} = -1 \mod n$ 
> but for all $a\in H$, $a^{2^{j+1}d} = 1 \mod n$.
> Such $j < r$ exists because $(-1)^d = -1 \mod n$.
> Now, define 
> 
> $$
> \bar H:= \set{a : a^{2^{j}d} = \pm 1 \mod n}.
> $$
> 
> Clearly, $H \subseteq \bar H$.
> Also, $\bar H$ is a subgroup.
> It remains to show that $\bar H$ is strict.
> Let $a\in \bar H$ be an element s.t. $a^{2^j d} = -1 \mod n$.
> We have $a^{2^j d} = -1 \mod n_1 = -1 \mod n_2$ by $n=n_1n_2$ and $\gcd(n_1,n_2)=1$.
> Let $b \in Z_n^*$ be an element s.t. $b^{2^j d} = -1 \mod n_1 = +1 \mod n_2$.
> We have $b^{2^j d} \neq \pm 1$ because of CRT, which implies that $b \notin \bar H$.


#### **Theorem:** generators are dense

{: .theorem}
> If $n$ is prime, such a number x (called a primitive root of n) will always exist; 
> see exercise 3.2.1.2–16. In fact, primitive roots are rather numerous. 
> There are φ(n − 1) of them, and this is quite a substantial number, since n/φ(n − 1) = O(log log n).
> 
> (Knuth, TA of CP, vol 2, Sec 4.5.4)


Basic number theory, DL assumption



OWP

Universal OWF


