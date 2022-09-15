---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 15 September, Thursday (Lecture 12)
author: Taught by Prof. Bapi Raju
---

# Hay et al. (2011) (contd.)
The broad spike in the dendritic voltage Hay et al.'s data is called the *calcium spike* and is due to the activation of calcium channels. The locations at which calcium is highly concentrated along the dendrite called *calcium hotspots*.

These spikes cause fluctuations in somatic This phenomenon is called BPAP (backpropagating action potential). This causes a back-and-forth called the *ping-pong effect*.

Thus, dendrites are more than just passive filters. Compartmental models help to model the active character of dendrites, as they are more morphologically realistic and can include several spatially distributed ion channels.  
However, it is difficult to tweak the spatial distribution of channels dynamically.

# Hodgkin-Huxley Revisited
We have seen that the Hodgkin-Huxley model is a four-dimensional system (controlled by four equations). Can we reduce its complexity while retaining its modelling power?

The model can be modified to the FHM model, which is described by two equations. This model is based on two ideas:

* Separation of slow and fast timescales in gating variables
* Exploiting correlations

We have seen that the Hodgkin-Huxley equations are
$$\begin{split}
C\frac{dU}{dt} = &- g_\text{K} \cdot n^4 \cdot (U - U_\text{K}) \\
&- g_\text{Na} \cdot m^3 \cdot h \cdot  (U - U_\text{Na}) \\
&- g_l \cdot (U - U_l) + I(t). \end{split}$$
$$\begin{split}
\frac{dn}{dt} &= -\frac{[n- n_0(u)]}{\tau_n(u)} \\
\frac{dm}{dt} &= -\frac{[m- m_0(u)]}{\tau_m(u)} \\
\frac{dh}{dt} &= -\frac{[h- h_0(u)]}{\tau_h(u)}
\end{split}$$

Of these gating variables, $m$ is said to have "fast" dynamics (compared to $n$ and $h$), in the sense that it rapidly approaches its steady-state value. Because of this property, we can replace $m$ with $m_0$, without losing much accuracy. This reduces one degree of freedom of the model.

Further, $n$ and $h$ have similar dynamics. The profiles of their steady states are mirror-images, and the dependence on time of $\tau_n$ and $\tau_h$ are also similar. These properties allow us to constrain their values as
$$1 - h(t) = an(t) = w(t),$$
for some constant $a$. This reduces another degree of freedom.

Thus, the only dynamic variables in the system are $u(t)$ and $w(t)$. This makes the equation
$$\begin{split}
C\frac{dU}{dt} = &- g_\text{K} \cdot \left(\frac{w}{a}\right)^4 \cdot (U - U_\text{K}) \\
&- g_\text{Na} \cdot m_0^3(u) \cdot (1-w) \cdot  (U - U_\text{Na}) \\
&- g_l \cdot (U - U_l) + I(t). \end{split}$$
$$\frac{dw}{dt} = -\frac{[w-w_0(u)]}{\tau_\text{eff}}$$

This pair of equations has the form
$$C\frac{du}{dt} = f(u(t), w(t)) + I(t)$$
$$\frac{dw}{dt} = g(u(t), w(t))$$

The fact that this system is two-dimensional lets us carry out phase-plane analysis.

## Separation of Timescales (detour)
Consider two general coupled DEs
$$\begin{split}
\tau_1\frac{dx}{dt} &= -x + c(t) \\
\tau_2\frac{dc}{dt} &= -c + f(x) + I(t)
\end{split}$$
where $\tau_1 << \tau_2$. The second term in the right-hand sides of these equations are called *drive terms*.

The time constant $\tau_1$ guides how fast $x$ is able to "track" $c$ (and correspondingly for $\tau_2$).

Suppose $f(x) = 0$ in the above equation. Then $x$ is driven by $c$, and $c$ is governed by $I$. We know that in the steady state, $x \to c \to I$, and the rates of approach of $x$ and $c$ to this state are determined by $\tau_1$ and $\tau_2$. In such a system, $c$ is a *low-pass filtered version* of $I$; it is the bottleneck that makes $x$ take time to catch up to $I$.

For a general $f(x)$, we have that $x$ and $c$ are tracking each other, and $c$ is also tracking $I$. Here, $c$ catches up with $I$ slowly, but $x$ tracks $c$ very closely since $\tau_1$ is fast.

In summary, we can separate timescales by setting $x$ to $c$ whenever $\tau_1$ is small.