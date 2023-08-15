---
layout: home
title: CS 6222 Introduction to Cryptography
nav_exclude: true
permalink: /:path/
seo:
  type: Course
  name: Introduction to Cryptography
---

Welcome to CS 6222, Introduction to Cryptography!
----------------------------------------

Cryptographic primitives are applied almost everywhere on the network, for instance, encryption and authentication. In this course, we will start from the theoretic foundations that ensures our belief in cryptography, and then we will visit some essential protocols as well as recent advances in cryptography. A major theme of this course is "provable security, " that is, to define the desired security and then to rigorously prove the security is achieved. Hence, students are expected to be familiar with algorithms and mathematical proofs.

Please send me an email if you have questions.

Classroom
---------

**Days and Times:** Monday/Wednesday 2:00-3:15 pm

**Location:** Mechanical Engr Bldg 341

Instructor Contact Information
------------------------------

**Name:** Wei-Kai Lin

**Email:** see [https://engineering.virginia.edu/faculty/wei-kai-lin]

Office Hours
------------

**Days and Times:** Tuesdays, 9:30-11:30am (or make an appointment using email)

**Location:** Rice Hall 505

Administration
--------------

We will use the [Canvas](https://canvas.its.virginia.edu) website to manage homework, exam, and grades. Please also use the discuss page on Canvas if you have course related questions.

There will be 4 homeworks (16% each), 1 final project (20%), and 1 final exam (16%). There will be occasional in-class quizzes that give bonus points (10%).

### Homework Policy

The submissions shall be PDF and typeset in Tex/Latex (template will be provided).

Every student shall submit homework individually. You are free to discuss with other students in this class, but in that case, you shall add an "Acknowledgement" paragraph explicitly. Similarly, you are allowed to make use of published material as long as you cite it properly with a "References" section. In any case, it is a violation if you copy text directly, or if you are unable to explain your solution orally to me.

Each student have 4 "late days" for homework in this semester.

There may be additional rules for some homework questions.

### Final Project

The final project is to read research papers in the area of cryptography, to write a 2-page summary, and then to present the topic in class. In addition to summary, you are encouraged to ask novel questions or to propose novel solutions.

The project can be done individually or by a group of two. The two students in the group get the same grade, so find your partner wisely. Each group is required to submit the authors and the research topic in an 1-page proposal (20%) at mid-semester. The summary (40%) is due at the end of the semester, and the last two lectures will be the presentation (40%).

See below for potential research topics.

### Academic Integrity

Everyone is required to follow the [Honor Codes of UVA](https://honor.virginia.edu/academic-fraud). Notice that using materials from generative AI (like ChatGPT) without citation is [plagiarism](https://honor.virginia.edu/plagiarism-supplement).

Course Outline
--------------

We will follow the course of Rafael Pass in the first half, and then move on to more applications. The square-brackets refer to the material of the lecture, where the material is listed below. This schedule is tentative, and I will add more references as we move on.

1.  Introduction and scope. Logistics. Preliminaries.  
    Match-making. Security definition. \[Ps 1.1-1.2\]  
    \* Aug 23  
    
2.  Shannon's definition. One-time pads. Limitation of information theoretic approach. \[Ps 1.3-1.4\]
3.  Efficient computations and efficient adversaries. One-way functions (OWF). \[Ps 2.1-2.2\]
4.  Prime Number Theorem. Factoring problem. Weak OWF from factoring. \[Ps 2.3\]  
    \* Sep 4  
    
5.  Strong OWF from weak OWF (hardness amplification). \[Ps 2.4\]
6.  Basic number theory, Discrete logarithm, candidate OWFs, one-way permutations. \[Ps 2.6 2.8 2.10\]
7.  Pseudo-Random Generators (PRG), indistinguishability, Pseudo-Random Functions (PRF)
8.  CPA security. Private-key encryption.
9.  Hard-core predicates. PRG from hard-core bits.
10.  Public-key encryption. Trapdoor permutations.
11.  Zero-Knowledge proofs.  
    \* Oct  
    
12.  Collision resistant hash functions. Birthday attack.
13.  Message Authentication Codes (MAC).  
    
14.  Signature. Identification.
15.  Oblivious algorithms. Oblivious RAM.
16.  Garbled circuits.  
    \* Nov  
    
17.  Oblivious transfer (OT). Secure two-party computation.  
    
18.  Secret-sharing. Secure multi-party computation.  
    
19.  Fully Homomorphic Encryption (FHE).
20.  Private Information Retrieval (PIR).

Course Material
---------------

\[Ps\]  
A Course in Cryptography. Rafael Pass and abhi shelat.  
[http://www.cs.cornell.edu/courses/cs4830/2010fa/lecnotes.pdf](http://www.cs.cornell.edu/courses/cs4830/2010fa/lecnotes.pdf)

\[KL\]  
Introduction to Modern Cryptography. Jonathan Katz and Yehuda Lindell.  
[https://www.cs.umd.edu/~jkatz/imc.html](https://www.cs.umd.edu/~jkatz/imc.html) (online access in UVA library)

\[Goldreich\]  
The Foundations of Cryptography. Oded Goldreich.  
[https://www.wisdom.weizmann.ac.il/~oded/foc-book.html](https://www.wisdom.weizmann.ac.il/~oded/foc-book.html) (online access in UVA library)
