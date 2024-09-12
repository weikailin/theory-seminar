---
layout: page
title: 2. Differentially private exact recovery for stochastic block models
nav_order: 2
nav_exclude: false
---

### Title: Differentially private exact recovery for stochastic block models

### Time
4:30-6pm, Monday, Sep 2, 2024

### Location
Rice 109

### Speaker
Dung Nguyen

### Abstract:
The goal of community detection in graphs is to recover the underlying labels/attributes of nodes (e.g., political affiliation) based on their connectivity. Stochastic block models (SBMs) are widely studied network models for community detection algorithms. In the standard form of an SBM, the $$n$$ vertices (or nodes) of a graph are divided into multiple pre-determined communities (or clusters). Connections between pairs of vertices are generated randomly and independently with pre-defined probabilities, depending on the communities to which the two endpoints belong.

A fundamental problem is the recovery of the community structure of a graph generated from an SBM. There has been significant recent progress in understanding the limits of community detection for SBMs. Sharp information-theoretic bounds for recoverability have been established for many versions of SBMs.

Our focus here is on the recoverability problem in SBMs when the connections of the input network are private. We aim to understand the fundamental trade-offs between intra-community and inter-community connection probabilities $$(p, q)$$, differential privacy (DP) budget $$(\epsilon, \delta)$$, and computational efficiency for exact recovery of community structure.

In this talk, I will focus on one of our proposed techniques called "stability analysis". This technique applies the Stability mechanism to a non-private estimator and leverages the estimator's stability to maintain the high utility of the private output. We first construct a semidefinite program (SDP) estimator that relaxes the maximum likelihood estimator (MLE) for the communities. Then, we prove that the optimal solution of the SDP is highly stable, i.e., it remains unchanged when the input is slightly perturbed, by providing a stable dual certificate for the SDP under edge perturbation.

The stability analysis has successfully derived the conditions for exact recovery in symmetric SBMs (where communities are of equal size) (ICML '22),  which was also the first exact recovery result achieved under DP. Recently, we have designed efficient algorithms and established conditions for exact recovery in three different versions of SBMs: Asymmetric SBM (where communities have non-uniform sizes), General Structure SBM (with outliers), and Censored SBM (with edge features) (ICML '24).

### Bio:
Dung Nguyen is a PhD candidate in Computer Science at the University of Virginia and the UVA Biocomplexity Institute, specializing in privacy-preserving algorithms for network science. His research focuses on solving fundamental graph problems—such as subgraph counting, clustering, and densest subgraph detection—within the framework of differential privacy (DP), with a strong emphasis on ensuring both rigorous utility and privacy guarantees.

He also explores methods to protect sensitive data in domains like public health, examining the impact of privacy on accuracy, usability, and explainability in real-world data analysis. His contributions to privacy-preserving algorithm research have been published in top-tier venues, including ICML, NeurIPS, AISTATS, IJCAI, and Nature Digital Medicine.

Dung is a recipient of the 2024-25 UVA School of Engineering Endowed PhD Fellowship and a winner in the first phase of data.org's Privacy-Enhancing Technologies (PETs) for Public Health Challenge.

Visit his personal website at: [https://dungxnguyen.github.io](https://dungxnguyen.github.io).

