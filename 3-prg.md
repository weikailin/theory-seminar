---
layout: page
title: 3. Pseudo-Randomness
nav_order: 3
nav_exclude: true
---

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
however, the distinguisher "another human" can not tell the difference due to limited power.

