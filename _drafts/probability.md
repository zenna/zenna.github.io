---
layout: classic
title:  "Probability Theory"
date:   2014-03-31 20:30:18
categories: probability theory
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>


# Outline



- Prevalence of uncertainty: where it comes from, why it is important
- Science of human thinking.  Logic.  Probability  theory  as
extended  logic  reproduces  many  aspects  of  human  mental  activity,  sometimes  in  surprising  and
even disturbing detail. 

- Probability Theory
- Connection to logic
- Relationship to science
- Generative model vs discriminative model

- 
- History of statistics/Bayes/
- Frequentist/Bayesian
 Difference from existing introductions
- Measure theoretic without the technicalities.
- Less emphasis on Bayes theorem
- More emphasis on representation



# Reasoning Under Uncertainty

“Uncertainty is the only certainty there is, and knowing how to live with insecurity is the only security.”

Suppose some late night a patient is found unconscious outside a bar.
Paramedics arrive at the scene, and do X.
But by what principles anre processes does he arrive at this conclusion

## From Determinism to Non-Determinism



Probability theory provides tools to reason in an uncertain world.
Uncertainty can stem from randomness; by definition, it is impossible to be certain about the result of a truly random physical process.
Probability allows us to reason about processes which may be deterministic but for all intents and purposes behave randomly, such as rolling a die.
Probability theory also allows us to model processes which we may not think of as random at all, but over which there may still be uncertainty due to our limited access to information, or limited resources to compute.

## Basic Definitionsa
Probability theory is notoriously confusing.  Some of this confusion stems from the fact that some concepts which are counter intuitive.
however, confusing naming, notation and inconsistent interpretations of the same thing do not help.
Fortunately, we can eliminate many of these problems by using a language which is formal to the extent it must satisfy a computer

Here I will argue that the basic principles of probability theory are simple.

### Probability Spaces
Probability theory is built on a small number of mathematical objects and simple axioms.  Often these axioms are given as is without motivation, and easily forgotten.

The most primitive principle at the foundation of probability is non-determinism, the idea that there are many ways the world could be.
Probability theory captures this idea using the most basic of mathematical objects: the set.
That is, we will assume there is a true, unknown world, which we will denote $$\omega$$, beloning to a larger set $$\Omega$$ of possible but untrue worlds.
$$\Omega$$ could be fininte or infinite, countable or uncountable; it is a choice that we will make, for reasons that will become clearer as we progress.

For example, suppose we wish to model the outcome of a die we are about to roll.

```julia
Ω = Set([1,2,3,4,5,6])
```

Even with this simple structure we can engange in some (non-probabilistic) reasoning.
For example we might gain some additional information that the die will roll even.

```julia
Ω2 = Set([ω for ω in Ω if iseven(ω)])
```

This operation of incorporating information by filtering the elements of $$\Omega$$ appears to be quite useful.
Rath

```julia
cond(Ω, predicate) = Set([ω for ω in Ω if predicate(ω)])
```
Reasoning non-deterministically is useful in some scenarios, but has clear limitations.  more often that not we want to consider which scenarios or more likely.

There are several ways we could try to quantify uncertainty.  For instance, rather than use a set to represent the set of scenarios, we could partially order the elements of $$\Omega$$, so that if we deem 1 to be more likely 2 then 1 > 2.  An obvious limitation is that we are unable to express that some outcome is much more likely than others.

A better approach is to associate each element of $$\Omega$$ with a value

Alternatively, we might follow the survey approach: associate each element of $$\Omega$$ with an uncertainty level impossible, unlikely, neutral, likely, certain.
As a first attempt, we might decide to formalize this as a function which maps elements of $$Omega$$

### Random Variables

Provided we've defined a probability space we can ask probability questions.
But we're still not done.
Suppose for examplew we want to model something more accurte.
Can use a different richer Omega.
We want to ask

```julia
N(om) = 
```

[[Relationship between random variables and functions]]

In normal notation, we do not often see random variables represented as a function.
This is for historical reasons--understanding random variables as functions is a more recent development than--and in many statisticians eyes, detracts from the semantic content.

## Transformations on Random Variables
Often phenomena are best modeled by complex probability distributions.
Complexity here derives from composing simpler distributions, which msore formally we can think of as the result of applying functions or transformations to distributioInnferns.

Suppose $$X:\Omega \to E$$ is a random variable defined on some probability space $$(\Omega, \mathcal{F}, \mathbb{P})$$.
Our transformation $$g:E \to F$$ is a function and whose domain is the set which supports $$X$$ and range is an arbitrary set.
Typically when one speaks of random variables they refer to real valued variables, and hence $$E$$ and $$F$$ are both $$\mathbb{R}$$



```
num- :: Omega ->
```

## What is a distribution, exactly?

Representation

We have constructed several mathematical objects--probability spaces, probability measures, sigma-algebras, and random variables--but are yet to see possibly the most commonly used probability object: the distribution.

There are all kinds of distributions - uniform distributions, gaussian distributions, bernoulli distributions, and so on.
But when we talk about *a* distribution, what is that thing exactly, and is it different to something which *follows* some distribution, e.g. the grades were uniformly distributed.

A probability distribution is simply the probability measure which assigns probabilities to events.

## 