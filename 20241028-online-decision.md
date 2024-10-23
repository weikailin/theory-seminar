---
layout: page
title: Information-Theoretic Approaches for Efficient Exploration in Online Decision-Making
nav_order: 4
nav_exclude: false
---

### Time
4:30-6pm, Monday, Oct 28, 2024

### Location
Rice 109

### Speaker
Haolin Liu

### Title:
Information-Theoretic Approaches for Efficient Exploration in Online Decision-Making

### Abstract:
In online decision-making, such as reinforcement learning, a learner repeatedly takes actions to interact with an unknown environment and receives reward feedback, with the goal of maximizing cumulative rewards. At each step, the learner only has partial knowledge of the environment based on prior interactions and faces a key dilemma: whether to exploit the best-known action or explore new, potentially better actions. This is referred to as the exploration-exploitation tradeoff, which seeks to balance leveraging current knowledge with acquiring new information.

Several well-established algorithmic principles, such as optimism in the face of uncertainty and Thompson Sampling, are commonly used to address this challenge. However, a natural question arises: do these methods achieve the optimal balance between exploration and exploitation?

In this talk, I will first provide an overview of these two principles and highlight their limitations in cases with complex information structures. Then, I will introduce a new framework called Information-Directed Sampling (IDS), which uses an information-theoretic measure to guide action selection, aiming to achieve an optimal balance between exploring less-understood actions and exploiting existing knowledge to maximize rewards. Finally, I will briefly explain how the idea of IDS leads to a statistical complexity measure for online decision-making.


### Bio:
Haolin Liu is a PhD candidate in Computer Science at the University of Virginia, advised by Professor Chen-Yu Wei. His research focuses on reinforcement learning theory and its application to language models. His works contribute to the theoretical foundations of reinforcement learning in dynamic environments and have been published in NeurIPS and ICLR with spotlight recognition.
