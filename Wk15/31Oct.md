---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 31 October, Monday (Lecture 20)
author: Taught by Prof. Bapi Raju
---

# Reinforcement Learning (contd.)
## Reward-Based Action Learning
Consider the example of a rat navigating a maze. Each neuron in the first layer is associated with a certain region in the maze, and it fires if the rat is in this region – the pattern of firing neurons therefore carries the position information.

The next layer, called the $Q$-layer, evaluates the function $Q(s,a)$, where $s$ is the current state and $a$ is some action to be taken.

The function $Q$ is updated according to the learning rule
$$\Delta Q(s,a) \leftarrow \eta [r - (Q(s,a) - \gamma Q(s',a'))],$$
called the SARSA rule. This achieves equilibrium when $Q(s,a) - Q(s',a') = r$.