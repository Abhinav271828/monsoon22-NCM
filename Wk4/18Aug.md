---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 18 August, Thursday (Lecture 6)
author: Taught by Prof. Bapi Raju
---

# Passive Membrane Model (contd.)
Let us consider the behaviour of the passive membrane DE under certain special input conditions. We have already considered the case $I(t) = 0$.

## Step Current
Consider the step function
$$I(t) = \begin{cases}
0 & t < t_0 \\
I_0 & t \geq t_0 \end{cases}$$

At the steady state just before $t = t_0$, we know that $V = 0$, or
$$U_\text{membrane}(t \to t_0) = U_\text{rest}.$$
Similarly, at the steady state after $t = t_0$, we will have $V = RI_0$, or
$$U_\text{membrane}(t \to \infty) = U_\text{rest} + RI_0.$$

We propose that the transition between these two steady states follows the equation
$$U_\text{membrane}(t \geq t_0) = U_\text{rest} + RI_0 \left[1 - e^{-\frac{t}\tau} \right].$$
To prove this, we can differentiate it to get
$$\begin{split}
\frac{d}{dt}U_\text{membrane} &= -RI_0 \cdot e^{-\frac{t}{\tau}} \cdot \left(-\frac1\tau \right) \\
\implies \tau\frac{d}{dt}U_\text{membrane} &= RI_0 \cdot e^{-\frac{t}{\tau}} \\
\implies \tau\frac{d}{dt}U_\text{membrane} &= U_\text{rest} - U_\text{membrane} + RI_0 \\
\implies \tau \frac{dV}{dt} &= -V + RI(t).
\end{split}$$

Thus, the proposed equation is a solution.

## Pulse Current
The pulse input with width $\Delta$ is given by
$$I(t) = \begin{cases}
0 & t < t_0 \text{ or } t > t_0 + \Delta \\
I_0 & t_0 \leq t \leq t0 + \Delta \end{cases}$$
If $\Delta \to 0$, we can express this as
$$I(t) = q_0 \delta(t-t_0),$$
where $q_0$ is the total amount of charge deposited. In general, we know that $I_0 = \frac{q_0}{\Delta}.$

We propose that this is solved by
$$U_\text{membrane}(t) = U_\text{rest} + RI_0 \left[ 1 - e^{\frac{(t-t_0)}{\tau}}\right].$$

Suppose that $\Delta << \tau$. In that case, we can express the exponential using a Taylor-series based approximation
$$e^{-\frac\Delta\tau} \approx 1 - \frac\Delta\tau.$$
This gives us
$$\begin{split}
U_\text{membrane}(t_0 + \Delta) &= U_\text{rest} + RI_0 \left[ 1 - 1 + \frac\Delta\tau \right] \\
&= U_\text{rest} + I_0 \frac\Delta c \\
&= U_\text{rest} + \frac{q_0}{c}. \end{split}$$

Thus, the voltage jumps by $\frac{q_0}c$ through the duration of the pulse. Thereafter, there is no input, so it decays according to our original solution delayed by $t_0$.

## Multiple Pulses
As the DE is linear, we can describe the solution under a sum of pulses as a sum of the solutions for each pulse.  

Now, any arbitrary current can be represented as a sum of infinitesimally small pulses. Thus the summation turns into an integral and we get
$$U_\text{membrane}(t) = U_\text{rest} + \int_\infty^t \frac1c e^{-\frac{(t-t')}\tau} \cdot I(t')dt',$$
since the infinitesimal charge $dq$ deposited at during $t' \leq t \leq t' + dt'$ is $I(t')dt'$.

This solution is specific to the case where the voltage was zero prior to the current. In the general case, this residual voltage also decays exponentially, and so we add this term to the equation to get
$$U_\text{membrane}(t) = U_\text{rest} + \left[U(t_0) - U_\text{rest} \right] e^{\frac{-(t-t_0)}\tau} + \int_{t_0}^t \frac1c e^{\frac{-(t-t_0)}\tau} \cdot I(t') dt'.$$

# Leaky Integrate-and-Fire Model
We have observed that a spike in the input leads to an EPSP (excitatory postsynaptic potential). This is followed by the relative refractory period, the undershoot and the stabilisation. These are not modelled by the passive membrane model.

The leaky integrate-and-fire model, then, augments the passive membrane model and incorporates two equations:
$$\tau \frac{dU_\text{membrane}}{dt} = -(U_\text{membrane}-U_\text{rest}) + RI(t)$$
$$U_\text{membrane}(t) = \theta \implies \text{Fire + Reset}.$$

For example, consider the behaviour of this model under a step current. We can distinguish two cases: $U_\text{rest} + RI_0 < \theta$ or $U_\text{rest} \geq \theta$.

In the first case, the voltage jumps to $U_\text{rest} + RI_0$ and stays there. There is no further change.  
In the second case, the voltage jumps to $\theta$ first (before reaching $U_\text{rest} + RI_0$). At this point (according to the second rule), a spike is emitted and the voltage is reset to some $U_r < U_\text{rest}.$  
At this point, the current is still $I_0$. So the voltage again rises from $U_r$ up to $\theta$, spikes and resets. This repeats as long as the current stays at the constant value of $I_0$.

What is the minimum current required for the voltage to reach $\theta$? We can substitute $\theta$ in the original equation's steady state to get
$$\theta = U_\text{rest} + RI_\text{min},$$
which means that
$$I_\text{min} = \frac{\theta - U_\text{rest}}{R}.$$

The interval between successive spikes reduces as the current increases. The dependence of $f = \frac1T$ on $I_0$ is called the *gain function* of the neuron. We can derive this as follows:
$$\begin{split}
\theta &= U_\text{rest} + RI \left[1 - e^{-\frac{t}{\tau}}\right] \\
\implies \left[1 - e^{-\frac{t}{\tau}}\right] &= \frac{\theta - U_\text{rest}}{R} \\
\implies e^{-\frac{t}{\tau}} &= \frac{\theta - U_\text{rest}}{R} \\
\implies T &= \tau \ln \left[\frac{RI}{RI - \theta + U_\text{rest}} \right] \\
\implies f &= \frac1T = \frac1{\tau \ln \left[\frac{RI}{RI - \theta + U_\text{rest}} \right]}
\end{split}$$

#### Homework (24 Aug)
Plot the f-I curve for the following parameters:
$$\begin{split}
U_\text{rest} &= -70 \text{mV} \\
\theta &= -45 \text{mV} \\
\tau &= 15 \text{ms} \\
R &= 40 \cdot 10^6 \Omega 
\end{split}$$
Adjust $I$ to get $0 \leq f \leq 40$ Hz.