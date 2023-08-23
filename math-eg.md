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

**label-purple**{: .label .label-purple }
**label-red**{: .label .label-red }

[Link to section](1-intro.md#a-toy-example-match-making)


#### **Definition:** Shannon Secrecy.

{: .defn}
> The private-key encryption scheme $(\cM,\cK,\Gen,\Enc,\Dec)$ is ....
> 
> $$
> \Pr[k \gets \Gen; m \gets D : \qquad m = m' \ | \  \Enc_k(m) = c] \quad = \quad \Pr[m \gets D : m = m'].
> $$
>
> An encryption scheme is said to be *Shannon secret* if ...


#### **Claim:**

{: .theorem}
> Perfect secrecy implies Shannon secrecy.

{: .proof-title}
> Proof:
> 
> Suppose that $(\cM,\cK,\Gen,\Enc,\Dec)$ is perfectly secret. For any $D$, any $c$, and any $m'$, we have
> 
> $$
> \Pr_{k,m}[m = m' | \Enc_k(m) = c] = \Pr_{k,m}[m = m' \cap \Enc_k(m) = c] / \Pr_{k,m}[\Enc_k(m) = c].
> $$
> 

{: .proof}
> Suppose that $(\cM,\cK,\Gen,\Enc,\Dec)$ is perfectly secret. For any $D$, any $c$, and any $m'$, we have
> 
> $$
> \Pr_{k,m}[m = m' | \Enc_k(m) = c] = \Pr_{k,m}[m = m' \cap \Enc_k(m) = c] / \Pr_{k,m}[\Enc_k(m) = c].
> $$
> 