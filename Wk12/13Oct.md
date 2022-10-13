---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 13 October, Thursday (Lecture 16)
author: Taught by Prof. Bapi Raju
---

# Population Models (contd.)
The function $F$ acting on $h_n(t)$ in the differential equation
$$\tau \frac{d}{dt} h(t) = -h(t) + RI^\text{ext}(t) + w_{ee}F(h(t))$$
is said to return the *activity* of the population. This is denoted $A_n = F \circ h_n$; in other words,
$$A_n(t) = F(h_n(t)).$$

## Reduction
We would like to reduce the three-equation system we saw earlier, if possible:
$$\begin{split}
\tau \frac{d}{dt}h_1(t) &= -h_1(t) + RI_1^\text{ext}(t) + w_{ee}F(h_1(t)) - w_{ei}F(h_\text{inh}(t)) \\
\tau \frac{d}{dt}h_2(t) &= -h_2(t) + RI_2^\text{ext}(t) + w_{ee}F(h_2(t)) - w_{ei}F(h_\text{inh}(t)) \\
\tau_\text{inh} \frac{d}{dt}h_\text{inh}(t) &= -h_\text{inh}(t) + w_{ie}\left[ F(h_1(t)) + F(h_2(t)) \right]
\end{split}$$

Our first assumption will be that $\tau_\text{inh} = \varepsilon \cdot \tau$, *i.e.*, inhibition is much faster than excitation. Thus we can assume that the inhibition reaches its steady state quickly, and
$$\frac{dh_\text{inh}}{dt} = 0.$$
Thus we get
$$h_\text{inh}(t) = w_{ie}[F(h_1(t)) + F(h_2(t))].$$

We are left with the $A_\text{inh}$ terms in the first two equations. We assume that for the range of interest, $F$ is the identity function itself, and so $A_\text{inh}(t) = h_\text{inh}(t)$.

These two assumptions give us a two-equation system, after substituting:
$$\begin{split}
\tau \frac{d}{dt}h_1(t) &= -h_1(t) + RI_1^\text{ext}(t) + (w_{ee} - w_{ei}w_{ie})F(h_1(t)) - w_{ei}w_{ie}F(h_2(t)) \\
\tau \frac{d}{dt}h_2(t) &= -h_2(t) + RI_2^\text{ext}(t) + (w_{ee} - w_{ei}w_{ie})F(h_2(t)) - w_{ei}w_{ie}F(h_1(t)) \\
\end{split}$$

In effect, the system behaves like two excitatory populations, with self-interaction constants $(w_{ee} - \alpha)$, and interacting with each other with constant $-\alpha$, where $\alpha = w_{ei}w_{ie}$.

## Phase-Plane Analysis & Decision Making
We can now draw the nullclines of $h_1$ and $h_2$ and carry out phase-plane analysis.

This gives us two stable fixpoints (one near 1 on each axis) and one unstable fixpoint (near the midpoint of the other two).

Now, the inputs $I_1$ and $I_2$ represent the strength of the stimuli from two different options between which a decision has to be made. In the phase plane, these values shift the nullclines up and down.

Consider the case where $I_2 < I_1$. This shifts the $h_2$-nullcline down, removing the stable fixpoint to the left of the separatrix; the only fixpoint left has a high value of $h_1$, representing the choice made. Similarly, if both inputs are weak, the only remaining fixpoint becoems unstable and stays close to the separatrix, representing an uncertain decision.

In other words, a biased input leads to a stable fixpoint – the decision reflects the bias.