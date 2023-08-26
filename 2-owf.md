---
layout: page
title: One-Way Functions
nav_order: 2
nav_exclude: true
---

$
\newcommand{\Enc}{\mathsf{Enc}}
\newcommand{\Dec}{\mathsf{Dec}}
\newcommand{\Gen}{\mathsf{Gen}}
\newcommand{\cM}{\mathcal{M}}
\newcommand{\cK}{\mathcal{K}}
\newcommand{\cA}{\mathcal{K}}
\newcommand{\card}[1]{\vert{#1}\vert}
$

One-Way Functions
=================

Motivation:
Given the impossibility of efficient but perfectly secure encryption, we want to relax our security definition.
Intuitively, we want to

0. encrypt long plaintext many times using a single short key, and
1. perform "fast" encryption and decryption given the legitimate key, and
2. ensure that the recovering of plaintext is "hard" without the key.

One-time pads achieves 1 and 2 but not 0.
This suggests that we require functions that are 

> "easy" to compute but "hard" to invert.

We next define easy and hard computation in terms of efficiency and probability.

Efficient Computation and Efficient Adversaries
------------------

We want to provide "efficient computation" to the honest users.

#### **Definition:** Deterministic Algorithm

{: .defn}
> An algo $\cA$ is a deterministic Turing Machine with input and output as bit strings ($\{0,1\}^*$).

Note: TM is by definition *uniform*, that is, its description size is constant for all unbounded long inputs.

#### **Definition:** Polynomial Running-Time

{: .defn}
> $\cA$ runs in time $T(n)$ if $\forall x \in \{0, 1\}^*$, 
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

> A *randomized* algorithm $\cA$, also called a probabilistic polynomial-time Turing Machine
> and abbreviated as PPT, is a deterministic algorithm equipped with an extra random tape. 
> Each bit of the random tape is uniformly and independently chosen.
> 
> We denote the computation by $y \gets \cA(x ; r)$ but sometimes omit $r$.
> Note that the running-time is bounded by a poly for all $(x,r)$.





We want to model adversaries with a stronger capability than honest.



Randomized algo, running time, easy is poly-time, adversary is non-uniform ppt

Attempt: worst-case OWF

OWF and factoring assumption, PNT

Weak OWF?

Basic number theory, DL assumption

OWP

Universal OWF


