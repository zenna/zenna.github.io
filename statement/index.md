---
layout: page
title: Research Statement
tags: [statement]
comments: true
---

How can we build machines that can reason coherently about the real
world, in all of its complexity and ambiguity? Machines that are both
logically consistent, i.e., free of self-contradiction, as well as
consistent with observed data. Machines that can distinguish causation
from correlation, and cause from effect. Machines that can truly
explain, at the appropriate level of abstraction, attuned to both the
knowledge and intentions of the recipient. Machines that can introspect
on their own reasoning to explain how and why they arrive at the
conclusions that they do. Machines that achieve all of these tasks not
only accurately and efficiently, but while adhering to the societal
norms and human values that we wish to uphold.

My research agenda is to answer these questions -- to understand the
principles governing such a machine, and from these principles to
ultimately construct one. To this end, I have taken probabilistic
programming as a starting point. Its central thesis is that (i)
real-world phenomena can be modelled to tremendous levels of detail
using simulation programs expressed in universal programming
languages[^1], (ii) any uncertainty about these phenomena can be
expressed with probability distributions within the simulations, and
(iii) we can use inference algorithms to automatically compute answers
to queries about our models, and consequently derive conclusions about
the phenomena themselves.

However, probabilistic programming in its current form is unable to
address all of the criteria laid out above. A primary challenge is that
probabilistic inference is in general computationally intractable: the
set of queries for which we can efficiently compute answers remains a
small subset of those of interest. A more fundamental limitation is that
there are kinds of knowledge and classes of query that are inexpressible
even within universal probabilistic programming. A prime example of this
is causality, which cannot, in principle, be handled within the language
of probability. My research has focused on addressing both of these
problems. Concretely:

1.  I develop algorithms for probabilistic and causal reasoning. These
    algorithms are generic in the sense that they are able to compute
    answers to a wide variety of queries posed on a wide variety of
    models.

2.  I formalise novel forms of reasoning, reducing the gap between what
    we can reason about as humans, and what is within the domain of
    automated reasoning.

To address these problems, my research exploits the compositional
structure of programs. Programs are not black-boxes; we can do more than
simply execute them. They are structured, symbolic objects that can be
interrogated, manipulated, and interpreted in different ways. Moreover,
programs are compositional -- even extremely complex programs, millions
of lines long, are no more than a small number of primitive expressions
composed together. Taking advantage of this structure, I have developed
methods that execute programs backwards from observations to causal
factors, and methods that intervene on the causal structure of programs
to automate counter-factual "what-if" reasoning. Below, I elaborate on
these and other projects, followed by my plans for future work.

### Inference With Declarative Knowledge {#inference-with-declarative-knowledge .unnumbered}

Much of human knowledge is *declarative* -- we believe and communicate
facts, such as that the stove is on, that Barack Obama was the 44th
American president, or that London is the capital of the United Kingdom.
Probability theory governs how to reason with declarative knowledge in
exactly the same manner as with observed data, but in practice most
methods of inference do not support most expressions of declarative
knowledge.

I introduced a framework called **Predicate Exchange**
[@tavares2019predicate] to support inference with declarative knowledge.
In this framework, generative knowledge is expressed in the form of
probabilistic simulation programs. In one example, we modelled a
diabetic patient's glucose levels over time as a simulation of a
stochastic dynamical system, using probability distributions to
represent uncertain causal factors that affect the transition from one
time-step to the next. Declarative knowledge, in contrast, is expressed
in the form of predicates: programs that compute whether a proposition
about the generative process is true or false. For example, the
proposition that the patient is having a hypoglycemic episode is
expressible through a predicate which computes whether the glucose
levels have fallen below a threshold. Predicate exchange conditions a
generative model on a predicate, revising the model such that
declarative propositions become fact, and updating all interdependent
factors correspondingly. Continuing the example, conditional on the
hypoglycemic episode occurring, the probability that the patient had
recently eaten decreases, and the necessity of a medical intervention
increases.

In most cases, declarative propositions that we would like to condition
on are extremely unlikely to be true of the generative process *a
priori*. As a result, sampling values of variables that are consistent
with the declarative knowledge becomes an extremely challenging
constraint problem. Predicate exchange aims to address this, motivated
by my observation that predicates provide only a single, impoverished
bit of information (true or false), even though there is often a sense
in which a proposition is almost (or very far from) true, such as if the
patient's glucose levels are almost below the hypoglycemic threshold.
Predicate exchange applies an automatic program transformation to
predicates such that they output a number between 0 and 1 rather than
just true or false, whereby a value close to but not quite 1 indicates
that the predicate is close to but not quite satisfied. Informally,
these *soft Boolean* values provide partial credit, guiding an inference
procedure towards regions that are consistent with the declarative
propositions. Formally, they are used as a quasi-likelihood in a Markov
Chain Monte Carlo process, yielding an inference procedure that is both
efficient and asymptotically exact.

### Parametric Inversion of Non-Invertible Programs {#parametric-inversion-of-non-invertible-programs .unnumbered}

I have taken this approach of inference-through-program-transformation
further, motivated by the observation that every inference problem
involves the inversion of a function. That is, a probabilistic model
computes the values of observable variables as a function of latent
causes, and inference involves the inverse process of computing latent
causes given values of observable variables. One example of this I have
worked on is vision as inverse rendering -- given a prior distribution
over three dimensional scenes (geometry, lighting, camera pose, etc.)
and a rendering function that simulates light to transform a scene into
a two dimensional image, a fundamental vision problem is to invert the
rendering function to infer the scene causally responsible for an
observed image. Virtually all methods of inference tackle inverse
problems indirectly, in part by simulating the model in the forward
direction and evaluating consistency with the observed output. I
developed a framework called **parametric inversion** [@tavares2021pi]
which takes the idea of inversion literally, inverting a program to
compute its input from a given output.

Most functions of interest are deemed *non-invertible* since they
transform multiple different inputs to the same output, which renders
the inverse process ambiguous. As a mathematical framework, parametric
inversion is an answer to the question of what it means to invert a
non-invertible function. A parametric inverse is a kind of generalized
inverse function that parametrically represents the set of all inputs
that a function maps to a particular output. In other words, given a
function $f$ that maps $x$ to $y$, its parametric inverse $f^{-1}$ maps
$y$ and some parameter $\theta$ to $x$, such that (i) $f(x) = y$, and
(ii) changing $\theta$ yields a different input $x'$ that also maps to
$y$.

To invert a complex program, parametric inversion uses a program
transformation that first replaces each primitive function in the
composition with a corresponding primitive parametric inverse. Then, it
reverses the order in which they are executed. This method is provably
*sound* and *complete* in the sense that it produces correct inverses
and is applicable to any program. While several technical hurdles remain
(inverting non-invertible functions is unsurprisingly very hard!),
promising initial results inverting programs of rendering-level
complexity provides evidence in support of radically different
approaches to inference that necessarily exploit programmatic structure.

![Parametric Inversion](){#fig:my_label}

### Counterfactual Generative Models {#counterfactual-generative-models .unnumbered}

There are several kinds of query that are not conventional probabilistic
inference queries. One powerful example of this is the counterfactual.
Counterfactuals are statements such as "If colonial powers hadn't
invaded, the Americas would be very different". More generally, they
take the form: "Given that $X$ is true, what if $Y$ were the case?".

I developed counterfactual reasoning within universal probabilistic
programming [@tavares2018language]. Counterfactuals require both
probabilistic conditioning ("Given that $X$ is true") and causal
interventions ("what if $Y$ were the case?") Conventional probabilistic
programming languages have, by definition, generic forms of
conditioning, but lack operators for causal interventions. Using a
programming languages concept called *lazy semantics*, I formulated
interventions as a kind of program transformation.

I developed a probabilistic programming language called Omega, which
includes causal interventions and general conditioning as primitives.
The result is the ability to compute counterfactual queries in the kinds
of simulation models that can only be expressed as probabilistic
programs. For instance, I used Omega to emulate the kind of decision a
conservationist might make: assuming a dynamical predator-prey system
that models competing populations over time, could culling the prey
species in the past have prevented overpopulation of the predator
species now?

Omega allows us to just as easily pose queries that are not strictly
counterfactuals but are causal and useful nonetheless. For instance, we
could ask "Suppose we were to give a medical treatment and subsequently
patient $A$ recovers, what should we predict about the treatment's
effect on patient $B$?". We can even infer the *distribution over
interventions* that is likely to bring about a desired outcome, such as
the patient surviving.

### Distributional Inference {#distributional-inference .unnumbered}

I formalised another non-standard form of inference that I call
**distributional inference** [@tavares2019random]. Distributional
inference allows us to incorporate statistics into our probabilistic
models. For example, a report on near-term climate change
[@kirtman2013near] places the *expected* increase in the range 700
ppm[^2] to 1000 ppm over the next two decades. If a climatologist
constructs a probabilistic dynamical simulation of emissions,
distributional inference is a mechanism to incorporate this expectation
bound directly into her model. In addition, as elaborated on below,
enforcing fairness, robustness, and many of the criteria of
trustworthiness onto intelligent systems are problems of distributional
inference that can be addressed within the framework.

Distributional inference provides a mechanism to condition a
probabilistic model such that a probability, expectation, divergence,
entropy, or any other distributional property takes a desired value. To
formalize this, I introduced a novel mathematical construct that I call
the **random conditional distribution**. The random conditional
distribution is an answer to the question of what it means to condition,
say, a probability to take a particular value, which is non-obvious
since conventionally a probability is fixed and hence cannot be
conditioned. Informally, a probability or any distributional property
can be viewed as uncertain -- and hence becomes conditionable -- if its
value is contingent on other causal factors in the model. For instance,
even if the probability of rain tomorrow under a weather simulation is
60%, this probability would change if clouds were observed. Uncertainty
over whether or not clouds will emerge can therefore be used to induce
uncertainty over the probability of rain occurring. The random
conditional distribution captures this concept in a generalisation of
the probability concept of a *conditional expectation*, relying on
introspection of the program's causal structure using the causal
framework outlined above, as well as mechanisms from higher-order
functional programming.

I incorporated the random conditional distribution operator into Omega
as a primitive. The benefits of this are analogous to those of making
conditioning a primitive construct in conventional probabilistic
programming languages: (i) distributional inference problems can be
expressed extremely succinctly, often exactly mirroring their
mathematical form, (ii) different distributional inference queries can
be posed against the same model, and (iii) different algorithms can be
used to perform distributional inference, which is often even more
computationally challenging than conventional inference.

## Future Directions {#future-directions .unnumbered}

Plainly put, the development of automatic probabilistic inference
methods able to handle the diversity of problems expressible within
probabilistic programming languages will be a major milestone. I believe
that analysis and manipulation of models' internal structure will be a
necessary part of any solution. Two possible future areas in this vein
are:

-   **Relational Inference:** Most inference methods simulate a model
    only in the forward direction. With parametric inversion I have
    demonstrated that inverse simulation is possible. Many effective
    methods of non-probabilistic reasoning such as SAT and SMT do
    neither of these extremes, and instead more freely choose what part
    of a model to evaluate when. This approach can be applied to
    universal probabilistic programming languages in a generalization of
    parametric inversion. Doing so will address some of the challenges
    in scaling parametric inversion up to very large and complex models.

-   **Model Specialization:** Many models have structure for which
    specialised inference procedures have been developed, such as
    Hamiltonian Monte Carlo for continuous models, and variable
    elimination in certain discrete models. Automatic identification of
    structural properties, such as independence, finiteness, and
    continuity, would allow automatic specialisation of inference
    procedures to different models or even parts of models.

Still, even in the hypothetical scenario of perfect inference, there are
several remaining challenges.

#### Causality Beyond Counterfactuals

Humans routinely ask and answer questions of *actual causality*: whether
some event $A$ that actually occurred (e.g., a vaccine was administered)
actually caused some other event $B$ to occur (e.g., a patient was
immune). I propose to build a system that can answer questions of actual
causality. Most formalisations of actual causality rely on
counterfactuals: $A$ actually caused $B$ means had $A$ not occurred (the
vaccine wasn't administered) neither would have $B$ (the patient
wouldn't have been immune). This suffers from the problem of
*preemption*: if some other event $C$ (e.g., the patient caught the
virus) would have caused $B$ to occur in the absence of $A$, following
this counterfactual definition leads us to erroneously conclude that $A$
is not the actual cause. An alternative approach that I will develop
will be based on analysing the primitive causal steps that occur in the
execution of a simulation model of the domain, rather than on
counterfactuals, hopefully sidestepping the preemption problem. This
approach will look more like how a programmer debugs a program --
starting at the error and working backwards, recursively using knowledge
of the language to answer, "Why did this happen?"

Actual causality lies at the heart of causal explanations. Explanation
has seen increased attention recently in machine learning, but much of
the structure, complexity, and utility of human explanations has not
been addressed. Human explanations are often communicative acts, taking
into account the knowledge and intentions of the explainer and
explainee. Constructing a system that generates causal explanations is,
in my view, a grand challenge of artificial intelligence that is within
reach. It will require probabilistic programs to capture both the
knowledge that causal explanations are based on and the beliefs and
intentions of its recipient, actual causality since causal explanations
denote actual causes, optimal program synthesis to explore the space of
causal explanations.

#### Trustworthiness {#trustworthiness .unnumbered}

Machine learning models often are brittle, violate privacy, and unfairly
replicate or exacerbate biases. Awareness of these failures has spurred
research into developing formal definitions of privacy, robustness, and
fairness. Typically, these definitions impose different kinds of
constraints on distributional properties.

Causal probabilistic programming is ideally suited to not only verify
whether models meet or fail these criteria, but also to synthesize
models that are trustworthy by construction. A concrete project I
propose to address is to synthesize models that are counterfactually
fair [@kusner2017counterfactual]. A decision that a person receives is
counterfactually unfair if it would have been different had some
protected property such as race or gender been different. Enforcing
counterfactual fairness requires both the distributional and
counterfactual inference frameworks that I have developed. Moreover,
counterfactual fairness relies on a counterfactual definition of actual
causality, and hence suffers from the problems of preemption mentioned
above. Developing better methods to compute actual causality will
therefore yield better definitions of fairness.

#### Polystructural Models: From Reasoning to Understanding {#polystructural-models-from-reasoning-to-understanding .unnumbered}

Human knowledge is broad, spanning a multitude of different domains, and
deep, describing phenomena from multiple perspectives and degrees of
abstraction. Human reasoning is able to span both this breadth and
depth. For example, an epidemiologist may predict how a mutation in
SARS-CoV-2's morphology will likely affect the border restrictions or
long term economic growth of a country. In contrast, formal
computational models, including probabilistic programs, tend to be
narrow and shallow, focusing on only one domain in isolation to a single
degree of abstraction. In my opinion, this is the primary foundational
gap between the current paradigms of modelling and inference, and
machines that could, for example, infer that the assassination of Franz
Ferdinand was the probable cause of World War I; that an experiment for
X should control for Y; or that an unreliable water supply is ultimately
caused by chronic government underinvestment.

Rather than a single isolated model, one avenue towards this would be to
construct representations of interconnected networks of models, whereby
multiple models of the same thing can both coexist and interact by
virtue of sharing structure. Such a "model-base" could be incrementally
built, incorporating more and more types and sources of knowledge.
Perhaps speculatively, I conjecture that this may take us a few steps
from automated reasoning towards a form of understanding and meaning,
whereby the meaning of a concept is a function of the conceptual role it
plays in all the different models within the network.

## Broader Vision {#broader-vision .unnumbered}

As is true for many, I am driven both by a basic curiosity to uncover
the workings of cognition -- particularly in reasoning, knowledge, and
learning -- but also to build technology that has a positive impact on
society. Fortunately, under the program I have described, these desires
have not only been compatible but mutually reinforcing. The complex
demands of societal problems casts an unflattering light upon the
inadequacies of even state of the art technical solutions. Still, in my
view, causal probabilistic programming is the most compelling candidate
for a foundation to meet these demands, enabling us to encode the
knowledge that we have, to learn from data, to support various forms of
reasoning, and to enforce important societal values and constraints.
However, building effective, trustworthy systems is not purely a
technical problem. Fairness, robustness, and privacy are elevated in
current literature largely because they may be simple enough to be
captured with our current mathematical formalisms, and not because they
are any more important than the more nebulous concepts of power,
freedom, and equality, to name just a few. Moreover, even these are
fraught with difficulties; on what basis should we decide if a
definition is "correct", especially given the real disagreement among
people? As summarised potently by Kalluri in [@kalluri2020don]: fairness
according to whom? Answering these questions will require humility,
conceptual breakthroughs, and deep collaboration across fields as
diverse as philosophy and sociology, all of which I am tremendously
excited to do.

[^1]: A programming language that is Turing-universal can express any
    (computable) computation.

[^2]: ppm (parts per million) is the ratio of the number of gas
    molecules to the total number of molecules of dry air
