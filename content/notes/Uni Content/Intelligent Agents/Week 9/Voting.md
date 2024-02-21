---
title: "Voting"
---

# Components of a Social Choice Model
Assume a set $Ag=\{1,...,n\}$ of agents (or voters)
These are the entities that will be expressing preferences

Voters make group decisions with respect to a set $$\Omega=\{\omega_1,\omega_2,...\}$$ of outcomes (or candidates)
- If we have $|\Omega|=2$ then we have a pairwise election
- If we have $|\Omega|>2$ then we have a general voting scenario

Each voter has preferences over $\Omega$

$\Pi(\Omega)$ is the set of all preference orderings over $\Omega$
Let $\succ_i\in\Pi(\Omega)$ be a preference ordering for agent $i$
$\omega \succ_i \omega'$ represents that outcome $\omega$ is ranked above the outcome $\omega'$ in agent $i$'s preference order $\succ_i$
Given a set of agents $Ag$, we denote by $[\succ]$ any preference ordering profile i.e. $$[\succ]\in\underbrace{\Pi(\Omega)\times...\times\Pi(\Omega)}_{n}$$

# The Social Choice Problem
How to combine different preference orderings to derive a group decision

A *Social Welfare Function* $f$ takes $n$ voters' preferences and produces a *social preference order* $$f:\underbrace{\Pi(\Omega)\times...\times\Pi(\Omega)}_n\rightarrow \Pi(\Omega)$$
A social choice function obtains just one of the possible outcomes $$f:\underbrace{Pi(\Omega)\times...\times\Pi(\Omega)}\rightarrow\Omega$$
We use $\succ^*$ to refer to the outcome of a social welfare function
Given preference ordering $[\succ]$ and social welfare function $f$, $f([\succ])=\succ^*$ is called the aggregate ranking for $[\succ]$
- $\omega\succ^*\omega'$ means that $\omega$ is ranked above $\omega'$ in the social outcome

# Voting Procedures
## Plurality Vote
Every candidate gets one point for every preference order that ranks them first

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113175533.png]]
 
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113175607.png]]
### The Condorcet Paradox
*Condorcet's paradox* tells us that there are scenarios in which no matter which outcome we choose, a majority of voters will be unhappy
### The Condorcet Criterion
A *Condorcet winner* is the candidate who always wins in pair-wise elections using plurality
A Condorcet winner does not always exist
A voting system satisfies the *Condorcet criterion*, if it always chooses a Condorcet winner when one exists
Rules satisfying this property are called *Condorcet methods* and are said to be *Condorcet consistent*
#### Example

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113180402.png]]
 
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113180419.png]]
## Copeland Method
Each candidate is scored based on its pairwise victories minus its pairwise losses
This method is Condorcet consistent

The Copeland method also works when there is no Condorcet winner
#### Example

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113181740.png]]
 
Wine wins twice, Beer has 1 win, Milk always loses

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113182313.png]]
 
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113182333.png]]
There is no Condorcet winner, but A is a Copeland winner
## Borda Count
The Borda Count takes into account all the information from a preference order
Borda count:
- With $x$ candidates, each voter awards $x$ points to their first choice, $x-1$ to their second and so on
- The candidate with the most points wins

The Borda count is not a Condorcet method

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113185557.png]]
#### Example

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230113185413.png]]
Beer gets 30 points, Wine gets 31 points, Milk gets 29 points

# Social Welfare Functions
## Desirable Properties
### Pareto Efficiency
A social welfare function is *Pareto efficient*, if, whenever every agent $i$ prefers $\omega$ over $\omega'$, then $\omega\succ^*\omega'$
### Independence of Irrelevant Alternatives (IIA)
A social welfare function is independent of irrelevant alternatives, if whether $\omega$ is ranked above $\omega'$ in the social outcome depends only on the relative orderings of $\omega$ and $\omega'$ in agents preferences

>[!Tip]
>A social welfare function is IIA if the outcome only depends on the relative orderings of candidates
>i.e. if $A$ $\succ$ $B$ then the outcome won't change so long as $A$ is always ordered somewhere above $B$
#### Example

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114173700.png]]
### Nondictatorship
A social welfare function is nondictatorial whenever there is no voter $i$ such that for all $\omega$, $\omega'$, if $\omega\succ_i\omega'$ then $\omega\succ^*\omega'$
## Arrow's Theorem
We say a social welfare function is *dictatorial* if it does not satisfy nondictatorship

>[!Theorem]
>For elections with more than 2 candidates, any social welfare function satisfying Pareto efficiency and IIA is dictatorial

There are fundamental limits to democratic decision making
Arrow's theorem tells us we cannot hope to find a voting scheme that satisfies all of the notions of fairness that we find desirable

# Social Choice Functions
## Desirable Properties
### Weak Pareto Efficiency
A social choice function is *weakly pareto efficient*, if, when every agent $i$ prefers $\omega$ over $\omega'$, then $\omega'$ cannot be the outcome of the social choice function

>[!Tip]
>A social choice function is weakly Pareto efficient if the outcome of the function is such that there is no other alternative that could make at least one person better off without making anyone else worse off
### Monotonicity
A social choice function $f$ is monotonic if, for every preference profile $[\succ]$, such that $f([\succ])=\omega$, if $[\succ']$ is another profile such that $\omega\succ_i'\omega'$ whenever $\omega\succ_i\omega'$ for every agent and every alternative $\omega'$, then $f([\omega'])=\omega$ as well

>[!Tip]
>If a certain option is the winner under a certain set of preferences, it should still be the winner if the preferences are slightly changed in its favor. This property is a desirable feature in social choice functions as it ensures that the outcome does not change arbitrarily with small changes in the preferences of the voters.
### Nondictatorship
A social choice function $f$ is *nondictatorial* if there does not exist an agent $i$ such that $f$ always selects the top choice in $i$'s preference ordering
## Muller-Satterthwaites's Theorem
We say a social choice function is *dictatorial* if it does not satisfy nondictatorship
>[!Theorem]
>For elections with more than 2 canddiates, any social choice function satisfying weak pareto efficiency and monotonicity is dictatorial

# Strategic Voters
A social choice function $f$, is manipulable if, for some preference ordering profile $$\succ_1,...,\succ_i,...,\succ_n$$ and voter $i$, there exists some $\succ_i'$ such that $$f(\succ_1,...,\succ_i',...,\succ_n)\succ_if(\succ_1,...,\succ_i,...,\succ_n)$$
- A voter can obtain a better outcome for themselves by unilateraly changing their preference profiles
- By misreporting their preferences to the voting procedure

Although voting procedures are manipulable, their manipulation is computationaly complex
- Not easy to manipulate some voting procedures intelligently
- Various unknowns
- Computing a lie can be costly
## Gibbard-Satterthwaitte's Theorem
Any social choice function with at least three outcomes that satisfies citizen sovreignty and is truthful (i.e. non-manipulable) is dictatorial

*Citizen sovreignty* - For every outcome $\omega$, there exists a preference profile $[\succ]$ such that the social choice function returns $\omega$