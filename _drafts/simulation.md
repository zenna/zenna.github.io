---
layout: classic
title:  "Simulation Review"
date:   2014-03-31 20:30:18
categories: simulation physical
---
# Simulation for physical inference

## Simulation as an engine of physical scene understanding - Peter W. Battaglia, Hessica B. Hamrick, Joshua B. Tenenbaum.
Authors want to explain how humans make inferences about the physical world.
They distinguish their approach from earlier literature in that they focus on

1. More realistic scenes composed of large numbers of interacting objects
2. Deal with geometric
2. Short-term prediction
3. Approximate answers.
4. Numerical, geometric computations as opposed to symbolic propositional reasoning.

Their central claim is that aproximate probabilstic simulation is key to human capacity for physical scene understanding, can explain how people make rich inferences in a diverse range of setting.
__My comment: heuristic account 
1. Humans possess an intuitive physics engine (IPE) akin to that used in video games
2. IPE performs prediction by simulation i.e. the engine is run through as a sequential program.  This is in contrast to attempting to analytically solve the problem.
3. IPE incorporates uncertainty by making these simulations stochastic - at various points in the simulation random choices are made.

Implementation
The IPE is based on Open Dynamics ENgine which performs rigid-body simulations over objects represented as polyhedra and mass distribution by inertial tensors.

1. Sample object scene (object positions)
2. Use this sample with a normal physics engine as a black box sense
3. Repeat 1 and 2 some large number of times
4. Use the resulting samples as a distribution, to compute answers to questions from.

The sampling is based on three parameters
theta - gaussian noise over object positions

When the task requires an accurate simulation, IPE fails to replicate human findings.  Simple heuristics more informative.

### Possible appoximations
The authors emphasise that such simulations are approximate; they posit will take trade fidelity for speed, moreover they will aggressively favour the latter.
They suggest three possible places to approximate:

1. The physics:
2. the scene
3. the probabilities

### The Scope and Limits of Simulation in Automated Reasoning. Ernest David and Gary Marcus

Claim simulation is deceptively appealing, works well in some situations, not at all in others, and not as effective as alternatives in many.
They define simulation as
1. Defining initial conditions
2. Defining some dynamic fully specified laws
3. The program simulates, i.e. executes a state after discrete state until a terminating condition is met

In fields which attempt to actually simulate reality, as opposed to emulate it to an aesthetically plausible result, it is widely known that accurate simulations are often unobtainable.
Simulations contain many fine tuned parameters to get good results in the limited domains they are applicable.

Many theories of physics, especially more complex ones involving fluids and temperature are significantly incomplete.
__Zenna__ I Am not sure what the argument here is. That because we don't have a full formal theory of all of physics our brains can't simulate it? This is as specious as claiming that defiencies in our knowledge in formal kinematics prevent us from walking.

1. __Time Discretisation:__ Poor discretisation can lead to problems of self intersection.
2. __Dependendence on initial conditions__: i.c.s can strongly affect output.  Can not strongly
3. __Choosing idealisation__: Different physics engines vary, and within any one engine there are numerous parameters which change how a physical scene is modeled.  *I Suppose the argument here is that from a modelling perspective it is difficult to decide which one to choose?*
4. __How to rapdily draw easy inferences__: Simulations always produce precise (if not accurate) result.  Many tasks do not require precise simulation of dynamics.  Example: reasoning that after shaking marbles in box they are still in the box.  You can answer this question through application of a simple rule - That "An object in a closed container remains in the container".
5. __Extra-physical information__: We can reason about things which depend on things not thought of as physical, e.g. the mental states of other agents, mechanics, interfaces.
6. __Incomplete Information__ : Simulation engines require precise specifications, yet humans can reason with only partially or uncertainly specified information.  For instance we can reason that we cannot cycle with a dining table without knowing the particular geometry of the dining table.
7. __Limits to Monte Carlo__: MC makes sense if we know the shape of an object and we just have some noise over in some standard form.  But what if we have imperfect knowledge of the *shape*. No natural probability distribution over the class of all shapes. __Zenna__: *this is just poorly informed. Secondly, it is hard to compute conditional probabiltiies given some conditions.  E.g. if I observe a nut in a bolt and have uncertain information about the occluded geometry.  If I want to compute some proposition about the dynamics conditioned on the bolt being in the nut, it will be very hard to satisfy this constraint. __Zenna__: Or will it?
8. __Physical dynamics of unknown entities__: Things can have unknown dynamics..
9. __Irrelevant Information__: Humans are able to reason physically while ignoring information irrelevant to the task.  Pouring lemon at a theme park is no more than pouring it in a vacuum.  Etching some engravings onto the bolt does not make the reasoning task harder.
10. __Polaris__: I don't get hte point here
11. __Non-applicabiltiy to many reasoning domains__: Planning) Sample space too vast 
12. __Frame problem (or bastardisation of))__: Picture two towers far apart, two scenes with two towers far apart.  Physics engine would have to keep simulating dynamics of tower B even though we are only interacting with tower A.  __Zenna__: *This is not true even in current day physics engine*.



### My Points
1. They say the resulting judgements are largely independent of details of particular collisions
## Bataglia 