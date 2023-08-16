---
layout: page
title: Introduction
---

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
 - Construction of the essentials (basic number theory and assumptions)
 - Modern crypto (cool stuff): ZKP, 2PC, MPC, FHE, my research


