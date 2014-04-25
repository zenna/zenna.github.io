---
layout: classic
title:  "An Overview"
date:   2014-03-31 20:30:18
categories: research overview
---
Welcome to my humble page.  It is under construction so please excuse typos or mysteriously unfinished sentences, paragraphs or sections.

I currently spend my days as a graduate student in the Brain and Cognitive Sciences at MIT, I will share here the problems I find interesting, and intend to solve.  Specifically:

<blockquote>If I am to write a computer program that practically and principally has the capacity for human level thought, what is the simplest set on primitives I must endow this program with, and in what language must I write it?</blockquote>

Many clever people think this is in principle impossible. A larger group tell me it's infeasible for the foreseeable future.  I prefer difficult.  My approach sits somewhere between cognitive science, computer science and engineering. The key words are program induction, intrinsic motivation, associative memory models of computation, computational complexity and meta-computation.

##Carrots and Sticks

You are, it seems, able to influence the world through action.
The actions you choose to take are also not entirely arbitrary.
Instead, they often lead you towards some goal, or the reward from achieving a goal.  A number of people have taken mathematical precision to this idea, formulating the problem as how an agent should take actions in an environment so as to maximise some notion of cumulative reward.  The field has assumed the label <i>reinforcement learning</i>, and both cognitive and neuro scientists have applied it to understanding behaviour, while engineers and computer scientists have built robots and chess players based on the principle.

There are a number of assumptions made in the original formulation of reinforcement learning that have since been relaxed to allow greater generality.
The most prominent of which concerns the agent's capacity for observation; instead of assuming that she has an omniscient and perfect knowledge of her environment, we can more feasibly suggest she can observe only partially and with uncertainty.  However another glaring assumption remains, false in almost any realistic problem, is that rewards are numerical values, embedded in the environment.
It is akin to suggesting that consuming an apple or graduating from university results in some fundamental reward stuff being transferred from the universe into you.

But assumptions often exist for a reason; if the rewards are not intrinsic to the environment, then where do they come from?  Or from the practictioners point of view, if I don't tell my agent that something is good, why will it do anything at all, let alone something useful?
A trivial, but apparently not obvious explanation is that you define your own goals, and derive, or compute the reward from achieving them (or not).
This is an incomplete solution however, since whether defined intrinsically or extrinsically there must be some fundamental motivation for useful behaviour.
I hope to stay an inch above, in terms of computability, one obvious evolutionary argument - you do stuff to avoid death and pass on your genes - but acknowledge that it is likely unavoidable that evolution has led to some primitive desires, which have no fundamental basis other than that they have proved themselves useful.  Take hunger for example, it invariably modulates several hours of your behaviour every day.  Yet you could forgo eating for some objective you deem more imperative given the circumstances, such as catching a falling baby.
You are able to create goals across a continuum of precision, from fine grained hand movements to New Year's resolutions of self improvement.
You can also abstract this process away from the real world to another domain, such as proving a mathematical theorem, or not falling down holes in Super Mario Land 2: 6 Golden Coins.
This leads to my next hypothesis:

<blockquote>
		There are are number of primitive goals, and a program which with consideration to these primitives, the world, the agent, and itself, dynamically manages the creation, modification and deletion of goals.
</blockquote>

Note the the framing in terms of goals, which is not new; in the similar problem of <i>planning</i> one seeks a sequence of actions which will lead to a goal state.  In one respect rewards are a generalisation of goals, where a goal is a special case where one particular class of states has reward 1, and everything else 0.
However it is not clear this generalisation expands in the correct dimension.  We want a system with.  consider a square grid world.

1. Collect the maximal number of coins within a given time frame</li>
2. Move on a circle trajectory until the original position and stop at hte original position.

The system: must defin goals in a structured form
From this form it must derive subgoals and select an active:
From subgoals it must derive actions

Assuming each x, y position of our agent represents one state in the statespace, it becomes very troublesome to translate this objective into a reward function, since if we reward moving from the current position we will never be able to stop there on return.  Of course we could reformulate the state space to be the set of all possible finite paths on our grid, making a reward function interpretation possible in principle, yet wildly impractical.  But even this approach breaks down if we make our grid world infinitely sized, despite the objective remaining tractable.  More importantly it shouldn't be up to us (the programmer) to be making these decisions.  make the reward function be dynamic If we abandon a classical RL state-reward framework for a declarative language of objectivesEvidently we already many in the form of human language

We need a langauge capable of expressing any objective.  It needs to be declarative.  If this is so the agent needs to be able to interpret this language.  This means translating these declarations into actions, much like a compiler.  Need the reward function be dynamic If we abandon a classical RL state-reward framework for a declarative language of objectivesEvidently we already many in the form of human language

This hypothesis is formulated to support what a human can do, and there are presumably many reasons why this may be not true for humans, or any animal.  It highlights a can-should dichotomy: can your observations be modelled this way, and should they?  Given a sufficiently general framework, the answer to the former is often yes.  The latter is more difficult, perhaps you should only if you believe your model is representing the true underlying phenomena or (as in my case) it may be useful.  Hence my objective is to formalise the above hypothesis into a computational form, that is one precise enough to execute on a computer.<span> which is difficult.  So before let's take a simpler chunk, and explore what I think might be one of those primitives, curiosity</span>

If we pretend for the moment that we've figured out what the rewards are and where they come from, we are still left with finding that program.  In the interests of parsimony, we may want a single program precise enough that goals are unambiguously translated down to actions in the real world.
Alternatively we might have two programs, the hypothesised one for generating the goals, and another for inferring the required actions for these goals.
Whether one or two, I will hence forth refer to this particular program as the policy, and still need to find out what they are.
<i>Find</i> here is an appropriate word, as it leads to my next point:


<blockquote>
The agent's policy should be a program in a universal model of computation, and we should find it by searching through the space of possible program.
</blockquote>
<span>

But before we get to searching, I should address what may have been a niggling question thus far: what is a program?

<h2>Computation</h2>
In the 1950s Turing told there is more than one way to do computation, and when you get to a certain point no one way can do more than another.
Somewhat surprsingly, it doesn't take much to reach this point, and there are radically different forms of computation that do.
Considering the original problem of finding that reward/goal/action generating program; I need to choose what kind of program, that is, what <i>model of computation.</i>
I could of course use a conventional programming language such as C++ or javascript.  But here are some reasons as to why that might not be a good idea.  Firstly is existential evidence, despite has ever.  Secondly, and as a likely cause of the first argument, common programming languages are very brittle, make one small change and the whole thing collapses.

Here's a model I devised based on simple networks of elements which propagate information between themselves, and transform it along the way.
I devised it based on (simplistic) principles of how subatomic particles interact, and it bears a passing resemblence to neurons in the brain.
It turns out that in many ways its a generalisation of a well studied model of computation, known as the cellular automata. TODO: Add infon pictures


<ul>
<li>A number of particles, where each particle has a fixed length string from a finite alphabet
</li>
<li>
	Particles can influence one anotehr by the exchange of virtual particles
</li>
<li>
	Virtual particles act as functions, taking one source particle as an argument and placing the transformed output on another
</li>
<li>
	The transformation that occurs, depends on the body of the virtual particle.
</li>
<li>
	Virtual particles can be influenced just like any other normal particle.
</li>
</ul>

We can demonstate this system doing something useful.
The following networks are instantations of a conjunction, that is a function of two binary variables, where the output is 1 only if both the inputs are 1, and 0 in all other cases.

TODO: add AND infons

<div>
GO
</div>


Now we have a representation that contains our solution, we need to find the solution.
Most people think this search problem is hard.
So we need to address too more questions, what is search anyway? and what about this (and any) problem, makes it hard rather than easy?

</span>

<h2>What makes a problem hard?</h2>


Why some problems are easy and some are hard keeps many a poor soul awake at night.  The theoretical computer scientist ponders whether problems for which candidate solutions can be verified in practical time, can also be solved in practical time.  It's easy for example to check that a  timetable assigned to you has no clashes, but much more difficult create a timetable with no clashes.  Is this disparity in difficulty due to your lack of imagination, or are these fundamentally different problems?  So important is this problem, that solving it will <a href ="http://www.claymath.org/millennium/">land you a million dollars</a>, and there's even a film in the works fictionialising the reprocussions of a proof.



I'll consider what makes a narrower class of problems - local search - easy or difficult.  In local search, you have a problem to which you can easily generate candidate solutions, and check how good these solutions are.

One metaphor to understand local search is that you (the searching algorithm) are situated in a rugged mountaneous landscape.  Every patch of this landscape represents a solution to your problem, and its altitude represents the quality of the solution. Your goal, as an adventure seeking exhilarist, is to find the tallest mountain in the land (the globally optimal solution).  Unfortunately for you, there is a pervasive fog so dense, you can only see as far as one step away.




<img src = "http://www.wunderground.com/data/wximagenew/p/pjpix/406.jpg"></img>


One approach would be to continuously look around yourself and take steps in the most uphill direction until no more can be taken. 
This problem with this heuristic, is that it may lead you to the top of a small mound, and lead you to think you've reached the top of the world.
This problem, getting stuck in a local maximum, is the bane of many algorithms.
I'll talk more about how to circumvent it in just a moment, but what we are interested in, is how the shape of this landscape affects how difficult it is to climb.



Mathematical formalisation of the landscape metaphor has given new explanatory power in fields diverse as molecular dynamics and evolutionary biology.  We may apply a similar line of thinking to search; much in the same way the difficulty of surmounting the greatest peak in a mountain range could be evaluated by properties such as the height or area of the tallest mountain, the number of smaller mountains, or even their spatial arrangement, many have hypothesised that the geometry of the landscape is a determinant of the difficulty in finding optimal solutions to a problem.



However a flaw in this method emerges when abstract from a fixed spatial topology such as three dimensions of the real world, and think in terms of abstract problems.  It suggests that explanatory success seen in molecular dynamics may not, at least naively, be applicable to search problems.
The difference is that in computational.
To take an extreme example, we may define a search algorithm where the local changes lead to a random solution, leading to a random landscape clearly completely uninformative of the difficulty of a problem.  Hence we may only sensibly make draw conclusions from a landscape defined by a search algorithm. that is:


<blockquote>
The landscape is induced entirely by the local search algorithm, and its topology determines how difficult the search problem will be.
</blockquote>


To demonstrate this, the following boxes are visualisations of two landscapes from a common search problem.  As described, each point represents a solution to the problem, their colour represents the quality from red(good) to blue (poor), and the lines connect solutions which can be reached within one step of the search algorithm.


<div>
TODO: GO - Add landscape box
</div>


We can see that these landscapes are very different, reitterating the point above.  In addition it demonstrates some of the qualities which easyness of a problem, for example a local smoothness, connectivity of the graph.
And while the above point is certainly depressing in delaying us from making few universal statements about problems (independent of search algorithms), it reveals possibilities: Equiped with an understanding of what landscape properties allow the discovery of better solutions, we can design of our search algorithm to induce landscapes with such properties.  Perh


<h2>Searching for programs</h2>


Having decided what we're searching for (a policy in a universal model of computation) in a representation we've decided may be suitable, we finally need to figure out how to search for it.
The local gradient ascent as noted above, is myopic; we're far too likely to get stuck in local maxima.
One powerful feature is that we can use reinforcement learning for both taking actions in the world, and for searching through program space to find new policies



This unification is elegant in my opinion, but in of itself it provides no qualitative differences to using a separate algorithm for policy search, like gradient ascent for example.
We can make a stronger statement however, that does change the game:


<blockquote>
The policy and search policy can be the same program.
</blockquote>


This implies that every time I find an new policy determining how to act in the world, I have a new search process of how to act in the world.
We want this new policy to be an improvement, so that not only is the agent a slightly better chess player for example, but also has a greater capacity for finding better policies.
One metaphor is to imagine a vast maze sparsely littered with treasure chests.  In addition to a few gold coins, each treasure chest contains a piece of advice about how to better search for treasure chests.


<blockquote>
The search algorithm must be replaced by a better search algorithm.  Where better reflects its ability to find better search algorithm.
</blockquote>


The recursive nature of this statement should trouble you.  At risk of appearing ungrateful, when granted three wishes by the genie, the most opportunitist of you would surely not emulate Alladin. More wishes would instead be wished for.  You'd be similarly astute enough not to ask for a single extra wish.  Somehow you're easily able to reason about the potential for infinite growth, without infinite mental resources.  To give a more practical example, .  Understanding how we are able to make decisions



For difficult problems, the .  We must abaondon the idea that we have discovered the best search algorithm and open up our ideas to modification.  




