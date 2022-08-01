---
title: Introduction to Neural and Cognitive Modelling (CS9.427)
subtitle: |
          | Monsoon 2022, IIIT Hyderabad
          | 01 August, Monday (Lecture 2)
author: Taught by Prof. Bapi Raju
---

# Studying the Brain
## Experimental Methodology
The working of the brain has been studied in various ways – lesioning, stimulation (electrical or magnetic), and recording (using EEGs or MRIs, say) are some of these.

Studying the diseased brain can also give insights into the functioning of the working brain; for example, a study of aphasia revealed that a similar region of the brain (including what are now called Broca's and Wernicke's areas) was affected across all patients. Thus these areas were concluded to be the "control centre" for language in the human brain.

## The Brain as a Computing Device
The brain is composed of $10^11$ repeatable units, called neurons. Individually, they are slow and noisy; they are combined into multiple parallel subsystems that work independently but in a coordinated manner.  
Each neuron has, on average, $10^4$ connections – the network is densely connected. This ensures that every neuron is just "a few synapses away" from every other.

Learning occurs due to changes in the properties of neurons and synapses. In a sense, the synapses between neurons are responsible for memories; stimulus statistics from the outside world are stored in the *paths* that signals follow through the brain.

Neural systems span a range of scales from micrometres (neurons) to metres (the central nerous system), forming structures at every level. They also operate at various time scales, from one-hundredth of a second (action potential) to a year (learning to walk). These are roughly classified into

* fast adaptive mechanisms (neurons and synapses; short-term memory)
* developmental learning (sensory and motor representations; plasticity)
* behaviour learning (achieving goals/receive rewards)
* evolutionary learning (adaptional by natural selection)

## Marr's Three-Level Framework
David Marr proposed three levels of analysis:

* the computational level – a specification of the input and output of the system.
* the algorithmic level – a high-level model of the problem.
* the implementation level – how neural networks actually accomplish the task

This can be illustrated by the examples of vision and memory.

### Vision
The problem in the case of vision is to convert a 2-D image on the retina to a 3-D reconstruction of the scene.  
In modern terms, the output is considered to be a *reconstruction of latent variables*.

The algorithm in this case might make use of graphical models, which represent variables as vertices and conditional dependencies as edges. The model describes the dependence of *peripheral spikes* (observed properties in the image) on *latent variables* (true properties of the object), by which the latent variables can be estimated.  

At the implementation level, we have no idea how the task is carried out.

### Memory
The problem in this case is to recall events, usually based on partial information (*associative* or *content-addressable* memory).

The algorithm here models memory as a dynamical system with fixed points, which are designated as "memories". We have an *activity space*, in which the partial information is situated; retrieval follows a path from the partial information to the fixed point, where the complete information is stored. The region around the memory from which the memory can be found is called its *basin of attraction* (in dynamical systems terms).

One neural implementation of this problem is the *Hopfield model*, which models neurons as the process
$$x_i = \text{sign}(\sum_j J_{ij} x_j).$$

## Abbott and Dayan's Classification
Abbott and Dayan classify models into three main types:

* descriptive – based on experimental data
* mechanistic – based on known anatomy and physiology
* interpretive – based on computational and information-theoretic principles