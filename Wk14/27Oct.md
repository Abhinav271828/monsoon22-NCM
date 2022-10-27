---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 27 October, Thursday (Lecture 19)
author: Taught by Prof. Bapi Raju
---

# Reinforcement Learning
Reinforcement learning is a form of learning where the agent must collect its own data, *e.g.*, when the agent learns to play games. Algorithms for reinforcement learning must learn to predict events ahead of time.  
It is based on the idea of conditioning, which was first explained by Pavlov in 1897.

Pavlov first noticed that a dog would salivate at the sight of food. He then rang a bell every time the dog was presented with food; eventually, the dog began to salivate every time the bell was rung, regardless of the appearance of food or not. In the dog's brain, the sound of the bell was associated with the appearance of food.

Dopamine is released in the brain according to RPE, or *reward prediction error* (not reward itself), which is calculated as (actual reward $-$ expected reward). The second term is what the agent learns to predict well over time.  
The *credit assignment problem* is a challenge in a reinforcement learning scenario. How does the agent know what has to be changed (learnt) to improve the reward? For example, in a complex task, like playing tennis, if one serves well, a number of actions need to be taken – which of these is essential and which can be changed?

Dopamine is produced by two areas in the midbrain, the VTA and the SN. We note that before learning (the association between two things, like a sound and food), the dopamine release occurs when the food is obtained, but after the association is learnt, it occurs at the predictive stimulus itself. There is no release once the food is actually received. Furthermore, if there is no food received, a dip in dopamine firing is observed (from the baseline of about 300 Hz).  
Learning occurs in the first and third scenarios.

## Learning
An agent learns a policy $\Pi$, which is a mapping from observations to actions. This is usually modelled as a probability distribution over actions given a state of the environment.

A reward is typically a *scalar feedback signal*. Rewards may be extrinsic (environmental) or intrinsic (*e.g.*, curiosity, learning progress, etc.).

## Challenges
Exploration is the main difference between RL and supervised learning – supervised learning agents do not need to explore to obtain their data.

Furthermore, it involves sequential decision making, and the states and actions form a continuous and/or high-dimensional space. The environment may also be unknown and the rewards sparse.

## Definition
RL is formalised as a Markov decision process or MDP, which has five components $\langle S, \mathcal{A}, P, R, \gamma \rangle$:

* $S$ is a finite set of states
* $\mathcal{A}$ is a finite set of actions
* $P$ is a transition function $S \to S$
* $R$ is a reward function
* $\gamma$ is a discount factor, to model diminishing rewards across time

The goal of the agent is to maximise the return:
$$G_t = r_t + \gamma r_{t+1} + \cdots + \gamma^i r_{t+i} + \cdots$$

The agent learns a policy, which gives probabilities $\pi(a_t \mid s_t)$, from which $a_t$ is drawn.

The agent also has a state value function to model which states are better:
$$V^\pi(s_t) = \mathbb{E}_\pi[r_t + \gamma r_{t+1} + \cdots \mid s_t]$$
The Bellman expectation equation rearranges this to
$$V^\pi(s_t) = \mathbb{E}_\pi[r_t + \gamma V^\pi(s_{t+1}) \mid s_t]$$

Similarly, we have a state-action value function
$$Q^\pi(s_t, a_t) = \mathbb{E}_\pi \mathbb{E}_{s_{t+1}} [r_t + \gamma Q^\pi(s_{t+1}, a_{t+1}) \mid s_t, a_t]$$

$\varepsilon$-greedy is a simple policy improvement method that allows for continual exploration. With probability $(1-\varepsilon)$, we choose the best action according to the current value function, and with probability $\varepsilon$, we randomly choose an action.

$Q$-learning learns about the value of its greedy policy from experiences gathered by a different policy, like $\varepsilon$-greedy. If $a$ represents the current action, which leads to a state $s'$ from which some action $a'$ must be taken, then
$$Q(s,a) \leftarrow Q(s,a) + \alpha(r + \gamma \max_{a'} Q(s',a') - Q(s,a)).$$