---
layout: page
title: test
nav_exclude: true
---

Math tests

$
\newcommand{\Enc}{\mathsf{Enc}}
\newcommand{\Dec}{\mathsf{Dec}}
\newcommand{\Gen}{\mathsf{Gen}}
$

inline $f(x) = 0$

Display

$$
\frac{1}{2}\cdot \sum_{i=0}^n x_i
$$

Long display

$$
\Pr[k \gets \Gen; m \gets D : m = m' \ | \  \Enc_k(m) = c] \quad = \quad \Pr[m \gets D : m = m']  \quad = \quad \Pr[m \gets D : m = m'] \quad = \quad \Pr[m \gets D : m = m'].
$$

quote display
> $$
> \frac{1}{2}\cdot \sum_{i=0}^n x_i
> $$

list display
- it holds that
  $$
  \frac{1}{2}\cdot \sum_{i=0}^n x_i
  $$

align

$$
\begin{align}
3x-1 &= -10 \\
  3x &= -9 \\
   x &= -3
\end{align}
$$

align*

$$
\begin{align*}
3x-1 &= -10 \\
  3x &= -9 \\
\end{align*}
$$

For "Kramdown" renderer:

do we need to escape vertical pipes $| S |$?

unfortunately need to escape vertical pipes $\vert S \vert$ due to over sensitive table in kramdown.

table begins from a block so
putting this on second line $| S |$ escapes it.

[test pdf](../../otherdocs/[SODA18]CacheOblivSort.pdf)


Sep 28
: [Java & Git](#)
  : [1.1](#)

Sep 29
: **Section**{: .label .label-purple }[Intro to Java](#)
  : [Solution](#)

Sep 30
: [Variables & Objects](#)
  : [1.2](#), [2.1](#)

Oct 1
: **Lab**{: .label .label-purple } [Intro to Java](#)

Oct 2
: [Tracing, IntLists, & Recursion](#)
  : [2.1](#)
: **HW 1 due**{: .label .label-red }
