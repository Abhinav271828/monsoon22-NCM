---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 28 July, Thursday (Lecture 1)
author: Taught by Prof. Bapi Raju
---

# Computational Neuroscience
There are many ways we can improve our understanding of the functioning of the brain; for example, behavioural studies, eye tracking studies, computational models, and so on. Computational neuroscience is a field of study that aims to understand the mechanisms underlying brain function by building quantitative models.

These models are influenced by considerations from anatomy, cognitive psychology, AI, statistics and dynamical systems.

# Modelling
## Levels and Types of Models
Modelling neural processes is done along a continuum of levels, from the abstract to the concrete. All models, however, make simplifications to be useful – the degree of simplification is the differentiating factor.  

Consider a model for a simple neuron. It could be:

* a binary threshold unit
* a continuous unit
* an integrate-and-fire model
* a spiking process
* a number of compartments, few or many
* a detailed model describing channel dynamics, etc., at the level of tissues.

A good model should not only explain what is already known, but also make testable predictions about the system – it should be *falsifiable*.

## Modelling Process
There are broadly two modelling strategies – bottom-up and top-down. Bottom-up models start from sub-neural components and build up to neurons, neural networks, brain regions, and finally the behaviour of the organism; top-down models, on the other hand, begin with behavioural information and break it down progressively until we reach sub-neural processes.