---
layout: page
title: 3. A Direct PRF Construction from Kolmogorov Complexity
nav_order: 3
nav_exclude: false
parent: 2024 Spring
---

### Time
9am, Tuesday, April, 2024

### Location
Rice 414

### Speaker
Yanyi Liu

### Title:
A Direct PRF Construction from Kolmogorov Complexity

### Abstract:
While classic results in the 1980s establish that one-way functions (OWFs) imply the existence of pseudorandom generators (PRGs) which in turn imply pseudorandom functions (PRFs), the constructions (most notably the one from OWFs to PRGs) is complicated and inefficient. $\newcommand{\mktp}{\mathsf{MK}^t\mathsf{P}}$

Consequently, researchers have developed alternative *direct* constructions of PRFs from various different concrete hardness assumptions. 
In this work, we continue this thread of work and demonstrate the first direct constructions of PRFs from average-case hardness of the time-bounded Kolmogorov complexity problem $\mktp[s]$, 
where given a threshold, $s(\cdot)$, and a polynomial time-bound, $t(\cdot)$, $\mktp[s]$ denotes the language consisting of strings $x$ with $t$-bounded Kolmogorov complexity, $K^t(x)$, bounded by $s(|x|)$.

In more detail, we demonstrate a direct PRF construction with quasi-polynomial security from mild average-case of hardness of $\mktp[2^{O(\sqrt{\log n})}]$ w.r.t the uniform distribution. We note that by earlier results, this
assumption is known to be equivalent to the existence of quasi-polynomially secure OWFs; as such, our results yield the first direct (quasi-polynomially secure) PRF constructions from a natural hardness assumption that also is known to be implied by (quasi-polynomially secure) PRFs.

Perhaps surprisingly, we show how to make use of the Nisan-Wigderson PRG construction to get a cryptographic, as opposed to a complexity-theoretic, PRG.

### Bio:
 Yanyi Liu is a PhD student at Cornell Tech, advised by Prof. Rafael Pass and Prof. Elaine Shi. He's interested in cryptography and its interplay with complexity theory.
