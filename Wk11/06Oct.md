---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 06 October, Thursday (Lecture 15)
author: Taught by Prof. Bapi Raju
---

# Population Models
Systems modelling populations of neurons more accurately mirror what happens in the cortex. We will make a computational attempt to model the task of (binary) decision-making using cognitive modelling principles.

In a population with external input $I^\text{ext}$, the membrane voltage is affected both by external and internal factors. A simple way to describe this dependence is
$$\tau \frac{d}{dt} h(t) = -h(t) + RI^\text{ext}(t) + w_{ee}F(h(t)).$$

This model, however, is valid only for high noise conditions (why?).

The $w_{ee}$ coefficient is a parameter modelling the population's self-dependence when it is excitatory. The population may also be affected by a different inhibitory population, which is modelled by $w_{ie}, w_{ei}$. Thus, for two excitatory networks and one inibitory network, we have
$$\begin{split}
\tau \frac{d}{dt}h_1(t) &= -h_1(t) + RI_1^\text{ext}(t) + w_{ee}F(h_1(t)) - w_{ei}F(h_\text{inh}(t)) \\
\tau \frac{d}{dt}h_2(t) &= -h_2(t) + RI_2^\text{ext}(t) + w_{ee}F(h_2(t)) - w_{ei}F(h_\text{inh}(t)) \\
\tau_\text{inh} \frac{d}{dt}h_\text{inh}(t) &= -h_\text{inh}(t) + w_{ie}\left[ F(h_1(t)) + F(h_2(t)) \right]
\end{split}$$