---
layout: page
title: Introduction
nav_order: 1
nav_exclude: true
---

$$
\newcommand{\Enc}{\mathsf{Enc}}
\newcommand{\Dec}{\mathsf{Dec}}
\newcommand{\Gen}{\mathsf{Gen}}
\newcommand{\cM}{\mathcal{M}}
\newcommand{\cK}{\mathcal{K}}
$$

Introduction
============

About me
--------------------------------------------
 - PhD: Cornell, postdoc: Northeastern
 - Undergrad major: chemistry
 - Worked in the industry as SE

About this course
--------------------------------------------
 - Goal: provable security, 1) define the desired security, 2) construct and prove a system
 - Rigorous and theoretic approach, comfortable with mathematical proofs
 - Prerequisites: Discrete Mathematics, Probability, Theory of Computation

Logistics
--------------------------------------------
 - Website (weikailin.github.io/cs6222-fa23), my email (wklin-course)
 - Office hours (Tue 9:30, Rice Hall 505)
 - Course works: 4 HW, final proj, final exam, quizzes
 - HW policies:

   The goal: critical def, rigorous proof, to solve future challenges
   
   1. in-class, reference, office hours
   2. other in-class students (ack)
   3. other pub (cite)
   4. ready-made solutions like other people, AI, solutions in prev courses (avoid)

   Eg, wrote your own, then google without edit. Good.
   Another eg, wrote your own, then google and edit. Shall cite or ack.

   Internalize your writeup. No direct copying. Must be explainable orally.

   See website for details.

A toy example: match-making
--------------------------------------------
Alice and Bob want to find out if they are meant for
each other. Each of them have two choices: either they love the
other person or they do not. Now, they wish to perform some
interaction that allows them to determine whether there is a
match (i.e., if they both love each other) or not—and nothing
more. For instance, if Bob loves Alice, but Alice does not love
him back, Bob does not want to reveal to Alice that he loves
her.

Note that the desired function is simply an AND gate that takes an input from Alice and an input from Bob.
Also, if we have a trusted third party Charlie, Charlie solve the problem.
The question is, can Alice and Bob compute AND without trusting any others?

#### The protocol
Assume that Alice and Bob have access to five
cards, three identical hearts(♥) and two identical clubs(♣). 
Also assume they have a round dish.

1. Put 1 heart face down on the top of dish.
2. Both A/B: encode Yes by heart-club, No by club-heart.
3. Both A/B: face down their cards on left/right of dish.
4. A secretly rotate the cards with dish
5. B secretly rotate the cards with dish
6. Open all cards, A-B are matched if and only if 3 hearts in a row.

#### Analysis
We need to show both correctness and privacy. 
The correctness is easy. The privacy can be argued by enumeration: 
all 3 cases {No-No, Yes-No, No-Yes} yield the same sequence (H,C,H,C,H) that is cyclic identical.

#### Discuss
Alternatively we can use 2 hearts and 3 clubs to compute AND.
To compute OR, we can encode Yes/No oppositely.
To compute XOR, we can use 2 hearts and 2 clubs.
Unfortunately, these protocols do not compose when we want to compose gates.


Course outline
--------------------------------------------
We will cover:
 - Essential primitives: OWF, PRG, PRF, encryption (SK, PK), authentication (MAC, sig)
   - Are they different / related? Sure, they serve different purposes. How to study them systematically?
   - Construction of the essentials (basic number theory and assumptions)
 - Modern crypto (cool stuff): ZKP, 2PC, MPC, FHE, my research (ORAM, DEPIR, RAM-FHE)

Classical cryptography: hidden writting
--------------------------------------------
Historically, human considered the scenario of *encryption* in communication.
 - Alice ~~~ $$m$$ ~~~> Bob
Eavesdropper Eve, an adversary, may be listening on the channel. 

Alice/Bob want to hide the message from Eve. To do so, they share two algorithms $$\Enc, \Dec$$ secretly and before the communication.
 - Alice ~~~ $$ct$$ ~~~>Bob
 - $$ct \gets \Enc(m)$$, ciphertext, where $$m$$ is the plaintext
 - Bob recovers plaintext by $$\Dec(ct)$$
 - $$y \gets A(x)$$ denotes algo $$A$$ computes on input $$x$$ and gets output $$y$$.

Notice: it is important that which info is *public* (known to all A/B/E) and which is *private*. What if Eve knows $$\Enc$$ or $$\Dec$$?

### Kerchoff's priciple

> The enemy knows the system.
>
> ~ Claude Shannon. Communication Theory of Secrecy Systems. The Bell System Technical Journal, 1949. [https://ieeexplore.ieee.org/document/6769090]

Reason: the algorithms are eventually leaked to Eve. We shall be conservative.

Consequence: let algos public, but keep a short secret key $$k$$.

Generalize: sample key $$k \gets \Gen$$

Note: $$(\Gen, \Enc, \Dec)$$ can not be all deterministic. What if only $$\Gen$$ is randomized?

### Classical encryption
Rotation, substitution, enigma, .... They are mostly broken now. DES? AES?

[Breaking German Army Ciphers](https://cryptocellar.org/bgac/)

Modern cryptography: provable security
--------------------------------------------
A principle driven *science* (instead of an art).
Modern cryptography relies on the following paradigms:

 - Providing mathematical definitions of security.
 - Providing precise mathematical assumptions (e.g. “factoring is hard”, where hard is formally defined).
 - Providing proofs of security, i.e., proving that, if some particular scheme can be broken, then it contradicts the assumption.

Definition of secure encryption
--------------------------------------------
We want to accurately model the A-B communication.

### Attempt 1
> The adversary cannot learn (all or part of) the key from the ciphertext.

It can leak the plaintext.

### Attempt 2
> The adversary cannot learn the plaintext from the ciphertext.

Leaking some function of the plaintext can be fatal.

### Attempt 3
> The adversary cannot learn *any function of, or any part of* the plaintext from the ciphertext.

The adversary may already learned something even not looking at ct.

### Intuitive Definition
> Given some *a priori* information, the adversary cannot learn any additional information about the plaintext by observing the ciphertext.

### Formal definition

Let $$\cK$$ be the space of keys, and let $$\cM$$ be the space of all messages.
We want to model the *information* as probability distributions.

#### **Definition:** Shannon Secrecy.
> $$(\Gen,\Enc,\Dec)$$ is said to be a *private-key encryption scheme* over the messages space $$\cM$$ and the keyspace $$\cK$$ 
> if the following syntax holds.
> 
> 1. $$\Gen$$ is a randomized algorithm that returns a key $$k \in \cK$$. We denote by $$k \gets \Gen$$ the process of generating $$k$$.
> 2. $$\Enc$$ is a potentially randomized algorithm that on input a key $$k\in\cK$$ and a message $$m \in \cM$$, outputs a ciphertext $$c$$.
>    We denote by $$c \gets \Enc_k(m)$$ the computation of $$\Enc$$ on $$k$$ and $$m$$.
> 3. $$\Dec$$ is a deterministic algorithm that on input input a key $$k$$ and a ciphertext $$c$$ outputs a message $$m \in \cM$$.
>    We denote by $$m' \gets \Dec_k(c)$$ the computation of $$\Dec$$.
> 4. (Correctness.) For all $$m \in \cM$$,  
>    $$\Pr[k \gets \Gen : \Dec_k(\Enc_k(m)) = m] = 1$$.  
>    (the probability is taken over the randomness of $$\Gen, \Enc$$.)
>
> The private-key encryption scheme $$(\cM,\cK,\Gen,\Enc,\Dec)$$ is *Shannon-secret with respect to the distribution $$D$$* over $$\cM$$ 
> if for all $$m' \in \cM$$ and for all $$c$$,  
> $$\Pr[k \gets \Gen; m \gets D : \qquad\qquad m = m' \ | \  \Enc_k(m) = c] \quad = \quad \Pr[m \gets D : m = m']$$.
>
> An encryption scheme is said to be *Shannon secret* if it is Shannon secret with respect to all distributions $$D$$ over $$\cM$$.

The RHS is the distribution of messages without $$c$$. The LHS is the distribution *conditioned on observing $$c$$*.
Is the definition good if we skip the quantifier for "all distribution $$D$$"?

An alternative intuition is that the distribution of ciphertexts for any two messages are identical.

#### **Definition:** Perfect Secrecy.
> The private-key encryption scheme $$(\cM,\cK,\Gen,\Enc,\Dec)$$ is *perfectly secret* 
> if for all $$m_1, m_2 \in \cM$$, and for all $$c$$,  
> $$ \Pr[k \gets \Gen : \Enc_k(m_1) = c] \quad = \quad \Pr[k \gets \Gen : \Enc_k(m_2) = c].$$









TEST

long math

$$\Pr[k \gets \Gen; m \gets D : m = m' \ | \  \Enc_k(m) = c] \quad = \quad \Pr[m \gets D : m = m']  \quad = \quad \Pr[m \gets D : m = m'] \quad = \quad \Pr[m \gets D : m = m']$$.

