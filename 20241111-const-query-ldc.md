---
layout: page
title: 5. Locally decodable codes with constant query complexity
nav_order: 5
nav_exclude: false
---

### Time
4:30-6pm, Monday, Nov 11, 2024

### Location
Rice 109

### Speaker
Jinye He

### Title:
Locally decodable codes with constant query complexity


### Abstract:
Locally Decodable Codes (LDCs) are a special type of error-correcting codes. Error-correcting codes are used to ensure the reliable transmission and storage of data, as information may become corrupted either during transmission or over time. Classical error-correcting codes are inefficient when we are only interested in a specific part or a particular bit of the message. LDCs solve this problem efficiently. By querying a few bits of a corrupted codeword, they can decode any bit of the message with a good probability.

Based on the relation between the message length $$k$$ and the query complexity $$r$$, there are three categories of LDCs. Among these, LDCs with low qnuery complexity—specifically, those with constant query complexity—are closely related to Private Information Retrieval (PIR). In this talk, we will primarily focus on this type of LDCs. An important parameter for this type of LDCs is the codeword length, and we hope to find best trade-off between query complexity and codeword length. For LDCs with more than 2 queries, there is still a significant gap between the upper and lower bounds of codeword length.

In this talk, we will start with an typical LDC--Reed-Muller Code, and then introduce the Matching Vector Code, which provides the best trade-off between query complexity and codeword length. Based on Matching Vector Code, we can construct the current most efficient r-server PIR. Finally, we will discuss a new result on the lower bound of LDC. A new perspective relating LDC to CSP (Constraint Satisfaction Problems), improves the lower bound results for 3-query LDCs.


### Bio:
Jinye He is a first year PhD student in Computer Science at the University of Virginia, advised by Professor Wei-Kai Lin. She is interested in cryptography and related topics in theoretical computer science.
