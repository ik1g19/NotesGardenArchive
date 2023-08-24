---
title: Dominant Strategy Implementation
---
### Are Indirect Mechanisms ever useful
A direct truthful mechanism forces the agents to reveal their types completely. There might be settings where agents are not willing to compromise their privacy to this degree

Full revelation can sometimes place an unreasonable burden on the communication channel

Agents' equilibrium strategies might be difficult to compute; in this case the additional burden absorbed by the mechanism might be considerable

# Implementable Choice Rules

## Weak Monotonicity

>[!Definition]
>**Weak Monotonicity**
>A social choice function $\chi$ satisfies weak monotonicity (WMON) if for all agents $i$ and all possible valuation profiles of the other agents $v_{-i}$ we have that $\chi\left(v_i, v_{-i}\right)=x \neq y=\chi\left(v_i^{\prime}, v_{-i}\right)$ implies that $v_i^{\prime}(y)-v_i^{\prime}(x) \geq v_i(y)-v_i(x)$

- WMON means that if the social choice changes when a single agent changes her declaration, then it must be that this change expressed a relative increase in preference for the new choice over the old choice.
- Alternatively (if you rearrange the inequality terms) you can say that the increase in her value for the new choice (i.e. $\left.v_i^{\prime}(y)-v_i(y)\right)$ is at least as large as the increase in her value for the old choice (i.e. $\left.v_i^{\prime}(x)-v_i(x)\right)$

### WMON is Necessary
>[!Theorem]
>**WMON is Necessary**
>If a mechanism $(\chi, p)$ is $D S$ truthful, then $\chi$ satisfies WMON

>[!Theorem]
>**When WMON is Sufficient**
>If all domains of preferences $V_i$ are convex sets (as subsets of Euclidean space) then for every social choice function $\chi$ that satisfies WMON there exists payment functions $p_1, \ldots, p_n$ such that $(\chi, p)$ is DS truthful

### What Social Choice Functions are WMON
Known for two extreme cases:
1. Unrestricted quasilinear settings where $V_i=\mathbb{R}^X$
2. Single dimensional settings

#### Case for Unrestricted Quasilinear Settings
##### Affine Maximiser or Weighted VCG
>[!Definition]
>**Affine Maximiser**
>A social choice function $\chi$ is an affine maximiser if for some subrange $X^{\prime} \subseteq X$, for some agent weights $w_i \in \mathbb{R}^{+}$, and for some outcome weights $\gamma_x \in \mathbb{R}, \forall x \in X^{\prime}, \chi$ has the form
>
$\hspace{14em}\underset{x \in X^{\prime}}{\operatorname{argmax}}\left(\gamma_x+\sum_i w_i v_i(x)\right)
$

>[!Theorem]
>**Roberts**
>If there are **at least three** choices that a social choice function will choose given some input, and if agents have **general quasilinear preferences**, then the set of (deterministic) **social choice functions implementable in dominant strategies** is precisely the set of **affine maximisers**

###### Understanding Robert's Theorem
In the case of **general quasilinear preferences** (i.e., when each agent can have any valuation for each choice $x \in X)$ and where the choice function selects from more than two alternatives, affine maximisers are **the only DS-implementable** social choice functions.
Efficiency is an affine-maximising social choice function for which $\forall x \in X, \gamma_x=0$ and $\forall i \in N, w_i=1$
- Affine maximising mechanisms are **weighted Groves mechanisms**.
- They transform both the choices and the agents' valuations by applying linear weights, then effectively run a Groves mechanism in the transformed space.
- Thus, we cannot stray very far from Groves mechanisms even if we give up on efficiency.

It is possible to implement a **richer set of functions** when agents' preferences are restricted further

#### Case for Single Dimensional Settings
##### Single-Parameter Domains
The opposite case to full dimensionality of unrestricted quasilinear
There is a single real parameter that directly determines the whole valuation vector $v_i$
There are several possible levels of generality in which to formalize this, we will consider an intermediate level that is simple and yet sufficient for most applications

In our setting, each bidder has a scalar value for **"winning"**, with "losing" having value of 0
Each agent is associated with a subset of **winning alternatives** $W_i \subseteq X$ where all $x \in W_i$ are equivalent to each others (in terms of their value) to agent $i$, and all $x \notin W_i$ are valued at 0 by $i$

###### Examples
- Single-item auction where (as we have assumed in this module) agents only care about whether they receive the item or not. So $W_i$ is the single outcome where $i$ wins
- A combinatorial auction setting with so called "known single-minded" agents, where each agent is only interested in a specific bundle of items (that is known to the mechanism), with only her value for the bundle being her private information. So $W_i$ are all the outcomes in which $i$ receives her bundle of interest
- Selfish routing setting where the mechanism wants to buy a path. $W_i$ is the set of all paths that contain edge $i$

##### Setting
- Each agent $i$ is associated with a subset of winning alternatives $W_i \subseteq X$, and a range of values $\left[t^0, t^1\right]$, which are both publicly known
- Agent $i$ values all $x \in W_i$ at $v_i$ (which is her private knowledge), and has value of 0 for all other choices

>[!Definition]
>**Monotonicity in Single-Parameter Domains**
>A social choice function $\chi$ on a single parameter domain is called monotone in $v_i$ if for every $v_{-i}$ and every $v_i^{\prime} \geq v_i$ we have that $\chi\left(v_i, v_{-i}\right) \in W_i$ implies that $\chi\left(v_i^{\prime}, v_{-i}\right) \in W_i$. That is, if valuation $v_i$ makes $i$ win, then so will every higher valuation $v_i^{\prime} \geq v_i$

## Critical Values
For a monotone function $\chi$, for every $v_{-i}$ for which agent $i$ can both win and lose, there is always a critical value $c_i\left(v_{-i}\right)$ at and below which $i$ loses and above which she wins

If $i$ wins for every $v_i$ then the critical value at $v_{-i}$ is undefined

## Normalised Mechansims
A mechanism on single parameter domain is called normalised if the payment for losing is always 0
That is, $p_i(v)=0$ if $\chi\left(v_i, v_{-i}\right) \notin W_i$

Every DS truthful mechanism can be easily turned into a normalised one. So it suffices to characterise normalised mechanisms

## Characterising Implementable Social Choice Functions
>[!Theorem]
>A normalised mechanism $(\chi, p)$ on a single parameter domain is $D S$ truthful if and only if the following conditions hold:
>1. $\chi$ is monotone in every $v_i$
>2. Every winning bid pays the critical value.
>	- If $\chi\left(v_i, v_{-i}\right) \in W_i$ then $p_i\left(v_i, v_{-i}\right)=c_i\left(v_{-i}\right)$.
>	- If $c_i\left(v_{-i}\right)$ is undefined (implying that given $v_{-i}, i$ wins for all $\left.v_i\right)$, then there exists some value $r_i, r_i \leq t^0$, such that $p_i\left(v_i, v_{-i}\right)=r_i$

Understanding this theorem:
- Not restricted to affine-maximisers
- E.g. $\chi=\operatorname{argmax}_x \sum_i v_i(x)^2$, or $\chi=\operatorname{argmax}_x \min _i v_i(x)$
- In many cases this flexibility allows the design of tractable (i.e. computationally efficient) **approximation** mechanisms for problems whose exact optimisation is computationally intractable

## Computational Applications of Mechanism Design

- Task scheduling: allocate tasks among agents to minimise makespan
- Bandwidth allocation in computer networks: allocate real-valued capacity of a single network link among users with different demand curves
- Multicast cost sharing: share the cost of a multicast transmission among the users who receive it
- Two-sided matching: pair up members of two groups according to their preferences, without imposing any payments, e.g. students and supervisors, hospitals and residents, kidney donors and recipients