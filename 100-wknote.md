---
layout: page
title: Wei-Kai's Notes
# nav_order: 0
nav_exclude: true
toc: true
---

This page maintains some of my personal and random thought's for this course.


### [Ps, Definition 26.1] Worst-case One-way Function.
The "hard to invert" property says that there is no adversary A such that 

$$
\forall x \Pr[A(f(x)) \in f^{-1}(f(x))] = 1
$$

The given equation $=1$ was not good since the next paragraph says that 

> assuming $NP \notin BPP$, one-way functions
> according to the above definition must exist. In fact, these two
> assumptions are equivalent (show this!).

However, to make the equivalence, the probability should be 

$$
\Pr[...] \ge 1 - 2^{-n}
$$

where 
$n:=|x|$ is the size of $x$.
Namely, if we want to prove that worst-case OWF imples $NP \notin BPP$, we want to construct a reduction
that uses a $BPP$ oracle to invert the OWF w.p. 1. 
This is open unless we have efficient derandomization, as pointed by Yanyi Liu.

### [Ps, Section 2.4.3, p.40] From weak to strong OWF
The analysis of $\Pr[A'(\vec y) \wedge x_j \notin G_n]$ is loose when we use it in the following union bound.
There factor is $m^2$, the first $m$ is from the random choice of index in $A_0$, 
and the second is from union bound.

We can split the event $A'(\vec y) \wedge \text{ some } x_i \notin G_n$ first, and then take union bound.
They are actually the same summation. This yields only one factor $m$. 

### [Ps, Theorem 12.3, p.12]
The probability

$$
\frac{\Pr_{k,m}[m=m' \cap \Enc_k(m)=c]}{\Pr_{k,m}[\Enc_k(m)=c]}
$$

does not seem to "be re-written as" the next one that exchanges $m$ and $m'$.
Particularly, in the nominator, $m$ is a random variable but $m'$ is fixed,
but in general the substitution shall be applied globally.

