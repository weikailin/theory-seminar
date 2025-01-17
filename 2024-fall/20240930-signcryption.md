---
layout: page
title: 3. Anonymous Multi-receiver Certificateless Hybrid Signcryption for Broadcast Communication
nav_order: 3
nav_exclude: false
parent: 2024 Fall
---

### Title: Anonymous Multi-receiver Certificateless Hybrid Signcryption for Broadcast Communication

### Time
4:30-6pm, Monday, Sep 30, 2024

### Location
Rice 109

### Speaker
Alia Umrani

### Abstract:

Confidentiality, authentication, and anonymity are fundamental security requirements in broadcast communication achievable by Digital Signature (DS), encryption, and Pseudo-Identity (PID) techniques. Signcryption, particularly hybrid signcryption, offers both DS and encryption more efficiently than “sign-then-encrypt”, with lower computational and communication costs. This paper proposes an Anonymous Multi-receiver Certificateless Hybrid Signcryption (AMCLHS) scheme for secure broadcast communication. AMCLHS combines public-key cryptography and symmetric key to achieve confidentiality, authentication, and anonymity. We provide a simple and efficient construction of a multi-recipient Key Encapsulation Mechanism (mKEM) to create a symmetric session key. This key, with the sender’s private key, is used in Data Encapsulation Mechanism (DEM) to signcrypt the message, ensuring confidentiality and authentication. The scheme generates identical ciphertext for multiple recipients while maintaining their anonymity by assigning a PID to each user. Security notions are demonstrated for indistinguishability against chosen-ciphertext attack using the elliptic curve computational diffie-hellman assumption in the random oracle model and existential unforgeability against chosen message attack under the elliptic curve diffie-hellman assumption. The AMCLHS scheme operates in a multireceiver certificateless environment, preventing the key escrow problem. We implement our scheme and statistically compare the performance with existing schemes for multiple receivers. Comparative analysis demonstrates that the proposed scheme achieves optimal communication cost, is computation-ally efficient, and ensures the security properties of confidentiality, authentication, anonymity, non-repudiation, and forward security.


### Bio:
I am a fourth-year PhD candidate in Computer Science at University College Cork, affiliated with the ADVANCE Centre for Training and Research, funded by Science Foundation Ireland (SFI). Currently, I am a Visiting Graduate Researcher (VGR) at the University of Virginia. My research focuses on both theoretical and applied aspects of cryptography, specifically on designing cryptographic protocols for secure broadcast communication. The main emphasis of my work is on establishing secure communication channels that ensure authentication, confidentiality, and non-repudiation for users. Additionally, I am interested in post-quantum cryptography, where I explore credential-based authentication methods, such as password-based schemes, and provide security using post-quantum hard assumptions like Learning with Errors (LWE).
