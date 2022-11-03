# Abstract
* how do IF neurons process multimodal input?
    * propose new computational model
    * alternative to TMs, attractor NNs
    * based on high-dimensional dynamical systems + statistical learning theory
* inherent transient dynamics of HDDSs (neural circuit) -> memory
* readout neurons extract information about current & past inputs
* based on liquid state machine
    * does not require sequential transitions between discrete states
    * universal computational power under idealised conditions

# 1 Introduction
* env. info is processed by stereotypic microcircuits
    * how?
* multiple recurrent loops are intractable for TMs, attractor NNs
    * difficulty in IF neurons is rapidly changing inputs
    * especially in HDDS like neural microcircuits
        * heterogeneity

* most common approach for modelling: control HD dynamics
    * review: Pearlmutter, 1995
    * cannot apply to networks of spiking neurons
* other: constructions of artificial NNs simulating TMs
    * some capable of real-time computing
    * but do not work for spiking neurons
* M96: can construct circuits of spiking neurons to imitate TMs
    * but central clock required
    * also require construction, not evolution/adaptation
* all these approaches break down on application of noise

* attractor NNs are robust to noise
    * hard to control
    * large set of attractors (2^n)
    * less suitable for real-time computing
        * latency in convergence

* also, neither of these can parallelise

* analyse dynamics of microcircuits from pov of readout neuron
    * extracts info and report results to other circuits
* can learn to extract salient info from transient states
    * learn to define its own (==) and work on novel input
        -> shows how invariant reading without having same state
* multiple modules can perform different tasks on same state trajectory
    -> parallelisation

* present model that does not require convergence
    * info about past input is captured in perturbations

# 2 Computing Without Attractors
* illustration of general approach
    * consider series of transient perturbations in liquid
    * as an attractor NN: only one attractor state so useless
    * but perturbed state at any t represents past inputs
    * to be informative, perturbations must be nonchaotic
        * depends on time constant, local interactions, etc.
    * neural microcircuits are ideal liquids
        * large diversity of elements
        * large variety of mechanisms, time constants

* foundation is liquid state machine
* two conditions for computing:
    * separation: difference in trajectories of system due to two diff. input streams
        * depends on complexity of liquid
    * approximation: capability to distinguish, transform diff. states to given outputs
        * depends on adaptability of readout mechanism

# 3 Liquid State Machines
* rigorous mathematical framework
    * universal computational power
    * real-time computing with fading memory

* input function u() is continuous sequence of disturbances
* target output y(): analysis of sequence
* machine M generates internal "liquid state" x_u(t) at every t
    * = current response to u(s ≤ t)
    * consists of analog values
    * filter of input function: x = Lu
    * not task-specific
* memoryless readout map f transforms x(t) to output
    * y = f • x
    * task-specific
    * may be many that operate in parallel

* memory storage in stable states is unnecessary
    * can be decaying
* consider only separation question: at which t will diff. u, v give different x_u(t), x_v(t)?

# 4 Universal Computational Power of LSMs for Time-Varying Inputs
* it has ucp if any time-invariant filter F with fading memory can be approximated to any degree of precision
* arguably, all maps that an organism needs to compute

* LSMs have ucp regardless of implementation (appendix A)
    * basis filters from which L is composed should satisfy point-wise separation
    * class from which f is drawn should satisfy approximation

* basis of SP, AP previously mentioned
* no serious a priori limits for computational power
    * theoretical support
    * no need for arbitrarily constructed circuits

* can also cover spike trains
    * sequence of point events

# 5 Neural Microcircuits as Implementation of LSMs
* computer simulation
    * generic recurrent circuit of IF neurons used as filter
    * evaluated performance on benchmark tasks

* input = 1+ input spike trains
    * injected current into 30% random "liquid neurons"
    * amplitudes of synapses chosen from gauss
* liquid state = all info that a neuron can extract at t
    * = output at t of liquid neuron
    * realistically, contributions of all liq neurons to membrane potential at t
    * x(t) = o_vec(t) • e^(-t/30)
* readout map f = separate population P of IF neurons
    * no lateral or recurrent connections
    * current firing activity p(t) of P = analog output of f
    * theoretically satisfies AP
    * if readout in Z_2 enough, single neuron will do
    * readout neurons can be trained using local learning rule
        * y = particular weighted sums of x(t)

* evaluate separation property of neural microcircuits on spike train inputs
    * large set of pairs of poisson spike trains u(), v() injected
    * resulting trajectories x_u(), x_v() recorded
    * avg. distance |x_u - x_v| at t plotted

# 6 Exploring the Computational Power of Models for Neural Microcircuit
* first test: applied to classification task
    * spoken words -> noise-corrupted spatiotemporal spike patterns
    * output was correct as soon as liquid state has obtained info
    * correctness = |target – readout|'
    * certainty = avg. correctness(t' ≤ t)

* giving constant output for time-varying liquid state is challenge
* second task: classification where all info contained in temporal evolution (interspike intervals of train)
    * impossible to classify from single interval
    * need to classify old segments of input also
    * works :+1:

    * tried on static synapses
    * big L
    * short-term dynamics play an essential role

* statistical distribution of connection lengths
    * f_3 was bad for small λ, and big λ
    * so best is local connections + some long-range

* general theory: power increases with improvement in SP, AP
    * main limitation is in SP
    * can be engineered in many ways
        * neuron diversity
        * specific synaptic architectures
        * connectivity
        * more columns (next section)

# 7 Adding Computational Power
* computational power can be enlarged by adding circuitry, without rewiring
    * difference between neural and artificial systems

* compare adding columns w/ adding connections
    * #columns improves SP
    * #connections improves SP but quasi-chaotically
        * increases sensitivity to noise

# 8 Parallel Computing in Real-Time on Novel Inputs
* does not have to be trained for a task
    * mutiple spike trains, multiple readout neurons trained
    * diverse and rapidly changing target

# 9 Readout-Assigned Equivalent States of a Dynamical System
* real-time computation => readout should generate appropriately scaled for any input
* dynamics of resout pools can be independent from liq

* in fig 3
    * firing activity in liq was dynamic, but constant in readout
        * not because readout samples few neurons
        * (distribution of synaptic weights on readout)
    * readout has learnt to define "equivalence" on liq states
        * inevitable in the collapsing of HDDS to single dim
        * but they are actually meaningful
        * allow real-time computation on novel inputs
    * exist purely from perspective of readout
        * property defining classes is different for different readouts

# 10 Discussion

* LSM: new paradigim for real-time computing on input streams
    * does not require circuit/program for task
    * relies on HDDSs and learning theory
        * adapt unspecific recurrent circuitry for task
    * same circuit can support different computations
        * parallel
* emphasis importance of perturbations in dynamical systems
    * separation, approximation enough for ucp

* demonstrated computational universality
    * generic recurrent circuits of IF neurons
    * first stable and generally applicable method

* simulations: possible explanations
    * computational role of neural circuits
    * characteristic distribution of connection lengths
        * between strictly local and uniform global
    * important role of dynamic synpases

* enhanced by presence of diverse units

* biologically realistic
    * unlike CS models
    * temporal aspects =/=> transitions between stable states or anything
    * trajectory of states is source of info

* offers new ideas for computationality of cognition
    * more global info about preceding inputs is preserved in HDDS state trajectories
    * readout maps implement specific tasks

* suggests that recurrent neural circuits are units of computation
    * give rise to models that link LSM columns to form cortical areas
        * columns may perform both liquid & readout fns
        * distinction is conceptual
    * plasticity in liquid may also be there

* might be useful in CS
    * real-time processing of complex input streams
        * tapped delay line in combination with NN/SVM/etc.
    * some issues are there for real-time reasons
    * projection of input time series into HD space
        * linear readouts from there

* neuromorphic engg and analog VLSI

