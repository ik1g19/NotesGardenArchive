---
title: Vickrey-Clarks-Grove (VCG) Mechanism
---
# Quasilinear Mechanism

In a quasilinear utility setting:
- the set of outcomes is $O=X \times \mathbb{R}^n$ for a finite set of choices $X$, and
- when outcome $o=\left(x,\left(p_1, \ldots, p_n\right)\right)$ is chosen, the utility of an agent $i$ given joint type $\theta$ is $u_i(o, \theta)=u_i(x, \theta)-p_i$

>[!Definition]
>**Quaislinear Mechanism**
>A quasilinear mechanism is a triple $(A, \chi, p)$, where
>- $A=A_1 \times \ldots \times A_n$, where $A_i$ is the set of actions available to agent $i$,
>- Choice function $\chi: A \mapsto X$ maps each action profile to a choice in $X$, and
>- Payment function $p: A \mapsto \mathbb{R}^n$ maps each action profile to a payment for each agent

## Direct Quasilinear Mechanism

>[!Definition]
>**Direct Quasilinear Mechanism**
>A **direct** quasilinear mechanism is a triple $(A, \chi, p)$, where
>- $A=A_1 \times \ldots \times A_n$, where $A_i=\Theta_i$ is the set of actions available to agent $i$,
>- Choice function $\chi: A \mapsto X$ maps each action profile to a choice in $X$, and
>- Payment function $p: A \mapsto \mathbb{R}^n$ maps each action profile to a payment for each agent

# Types

Type of an agent encapsulates all the private information that the agent has
Often the type of an agent is simply their private utility function $u_i$

In a quasilinear setting $u_i(o, \theta)=u_i(x, \theta)-p_i$
Assuming IPVs, $u_i(o, \theta)=u_i\left(o, \theta_i\right)$
In a quasilinear setting with IPVs $u_i(o, \theta)=u_i\left(x, \theta_i\right)-p_i$

We refer to $u_i\left(x, \theta_i\right)$ as agent $i$ 's **valuation** for choice $x$ and use a shorthand $v_i(x)$
In a quasilinear setting with IPVs, the **type** of an agent is "equivalent" to their valuation function.
- So when a direct mechanism asks agent $i$ to reveal their **type** $\theta_i$, it is asking $i$ to reveal $v_i$

# Direct Quasilinear Mechanism with IPVs

Setting:
- $n$ strategic agents
- A finite set $X$ of choices
- An agent's valuation for choice $x \in X$ is $v_i(x)=u_i\left(x, \theta_i\right)$
- the maximum amount $i$ is willing to pay for $x$ to be chosen
In a direct mechanism:
- Agents are asked to declare $v_i(x)$ for each $x \in X$
- Let $\hat{v}_i$ denote the valuation that agent $i$ declares to the mechanism
	- $\hat{v}_i$ may be different from her true valuation $v_i$
	- Let $\hat{v}$ denote the declared valuation profile of all agents, and $\hat{v}_{-i}$ the declared valuation profile of all agents except $i$
- The mechanism maps $\hat{v}$ to a **choice** $x \in X$ and a **payment** for each agent

Often when it is understood we are in a quasilinear setting, $x \in X$ is referred to as an **outcome**

# Truthfulness

## Properties of Dominant-Strategy Truthfulness

### Efficiency

>[!Definition]
>**Efficiency**
>A quasilinear mechanism is efficient, or social-welfare maximising, if in equilibrium selects a choice $x$ that maximises $\sum_{i=1}^n v_i(x)$

- Efficiency is also called economic efficiency to distinguish from other (e.g. computational) notions.
- Note that efficiency is defined in terms of true (not declared) valuations

### (Dominant-Strategy) Truthfulness

>[!Definition]
>**Dominant-Strategy Truthful Mechanism**
>A direct quasilinear mechanism is dominant-strategy truthful (truthful) if for each agent $i$, declaring $\hat{v}_i=v_i$ maximises $i$ 's utility, no matter what the other agents declare:
>
>$u_i\left(\chi\left(v_i, v_{-i}\right), p_i\left(v_i, v_{-i}\right)\right) \geq u_i\left(\chi\left(\hat{v}_i, v_{-i}\right), p_i\left(\hat{v}_i, v_{-i}\right)\right), \forall \hat{v}_i \forall v_{-i} \forall v_i$
>
>Our definition before, adapted for the quasilinear setting

### Individual Rationality

>[!Defintion]
>**Ex post Individual Rationality**
>A mechanism is ex post individually rational if in equilibrium, the utility of each agent is at least 0
>- So no agent loses by participating in the mechanism.
>- There is also the notion of ex interim individual rationality

### Budget Balance

>[!Definition]
> **Budget Balance**
> A quasilinear mechanism is budget balance when $\forall v, \sum_{i=1}^n p_i(s(v))=0$, where $s$ is the equilibrium strategy profile.
>- Regardless of the agents' types, the mechanism collects and disburses the same amount of money from and to the agents.
>- There are also weak and ex ante variants.

### Tractability

>[!Definition]
>**Tractability**
>A quasilinear mechanism is tractable if for all $\hat{v}, \chi(\hat{v})$ and $p(\hat{v})$ can be computed in polynomial time.
>- The mechanism is computationally feasible

### Other Properties
- Revenue Maximisation
- Fairness

## Efficiency + Dominant-Strategy Truthfulness

Vickrey (second price) auction is both efficient (social-welfare maximising) and dominant-strategy truthful
The general class of mechanisms that are both efficient and dominant-strategy truthful are called **Groves Mechanisms**

# Groves Mechanisms

>[!Definition]
>**Groves Mechanisms**
>Any direct quasilinear mechanism $(\chi, p)$ where
$\hspace{14em}\begin{gathered}\chi(\hat{v})=\underset{x}{\operatorname{argmax}} \sum_i \hat{v}_i(x) \\p_i(\hat{v})=h_i\left(\hat{v}_{-i}\right)-\sum_{j \neq i} \hat{v}_j(\chi(\hat{v}))\end{gathered}$
>- VCG is a specific mechanism within the class of Groves mechanism. (The most famous mechanism within this class.)
>- Some people refer to Groves mechanisms as VCG mechanisms.
>- Vickrey auction is a special case of VCG, and hence VCG is sometimes known as generalised vickrey auction

- agent $i$ must pay some amount $\color{#ff82b2}h_i\left(\hat{v}_{-i}\right)$ that doesn't depend on his own declared valuation
- agent $i$ is paid the sum of others' declared valuations for the chosen choice

# Vickrey-Clarks-Groves (VCG) Mechanism

The **Clarke tax** sets the $h_i$ term in the definition of the Groves mechanism as:
$$
h_i\left(\hat{v}_{-i}\right)=\sum_{j \neq i} \hat{v}_j\left(\chi\left(\hat{v}_{-i}\right)\right)
$$
>[!Definition]
>
>The VCG mechanism is a direct quasilinear mechanism $(\chi, p)$ where
>
$\hspace{13.5em}
\begin{gathered}\chi(\hat{v})=\underset{x}{\operatorname{argmax}} \sum_i \hat{v}_i(x) \\p_i(\hat{v})=\sum_{j \neq i} \hat{v}_j\left(\chi\left(\hat{v}_{-i}\right)\right)-\sum_{j \neq i} \hat{v}_j(\chi(\hat{v}))\end{gathered}
$

![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230318203201.png)

Every agent pays his/her social cost
VCG is also called pivotal mechanism

Who pays 0
- Agents who don't affect the choice of the mechanism
Who pays more than 0
- Pivotal agents who make things worse for others by existing
Who gets paid
- Pivotal agents who make things better for others by existing

## Combinatorial Auction Example

Two goods $A$ and $B$
$n$ agents (here bidders)
Set of outcomes $X$ has $(n+1)^2$ elements: who gets $A$ (if anyone) and who gets $B$ (if anyone)
We assume (as is usually the case) that **each bidder only cares about what good s/he receives** (and hence values receiving no good at 0 )
Therefore, we can write an agent $i$ 's valuation by specifying only 3 values: $v_i(A), v_i(B)$ and $v_i(A B)$.

VCG chooses who gets what item(s) and how much each agent pays

What choice does VCG pick (i.e. who gets $A$ and who gets $B$ ), and what is the payment for each agent?
Combinatorial auction setting with two agents
- $v_1(A)=3, v_1(B)=2, v_1(A B)=6$
- $v_2(A)=1, v_2(B)=4, v_2(A B)=4$
- The social welfare maximising allocation awards $A$ to agent 1 and $B$ to agent 2 , hence achieving social welfare of $v_1(A)+v_2(B)=7$
- $p_1=4-4=0$ and $p_2=6-3=3$

## Selfish Routing Example

![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230225210802.png)

The number on each edge is the cost of transporting along that edge. Each edge is owned by a different agent and the costs are private information of the agents.
Goal: Find the shortest (least-cost) path from from $A$ to $F$.
The set of outcomes include all possible paths from from $A$ to $F$.
Note that numbers on edges are costs, not benefits.
- If we select a path that crosses an edge of cost $c$, its owner is incurring a cost of $c$ which means his value for this path is $-c$.
- If our path doesn't cross agent i's edge, his value for the path is 0

What choice will be selected by $\chi$ ? ABEF
How much will $A C$ have to pay?
- The shortest path when $A C$ is not present has length 5 and imposes cost of $-5$ on the remaining agents.
- The shortest path when $A C$ is present has length 5 , and imposes cost of $-5$ on other agents.
- Thus, $P_{A C}=(-5)-(-5)=0$.
Who else pays zero? $B D, C E, C F$ and $D F$

How much will $A B$ have to pay?
- The shortest path when $A B$ is absent is $A C E F$, which imposes a cost of $-6$ on the remaining agents.
- The shortest path when $A B$ is present has length 5 and imposes a cost of $-2$ on other agents.
- Thus $p_{A B}=(-6)-(-2)=-4$

How much will $B E$ have to pay? $p_{B E}=(-6)-(-4)=-2$
How much will $E F$ have to pay? $p_{E F}=(-7)-(-4)=-3$
$E F$ and $B E$ have the same costs but are paid different amounts. Why?
- $E F$ has more market power: for other agents, the situation without $E F$ is worse than the situation without $B E$

## Truthfulness

>[!Theorem]
>Truth-telling is a dominant strategy under Groves mechanisms

### Proof
Consider a situation where every agent $j$ other than $i$ follows some arbitrary strategy $\hat{v}_j$. Consider agent $i$ 's problem of choosing the best strategy $\hat{v}_i$. The best strategy for $i$ is one that solves
$$
\max _{\hat{v}_i}\left(v_i(\chi(\hat{v}))-p_i(\hat{v})\right)
$$
Substituting in the payment function from the Groves mechanism, we have
$$
\max _{\hat{v}_i}\left(v_i(\chi(\hat{v}))-h_i\left(\hat{v}_{-i}\right)+\sum_{j \neq i} \hat{v}_j(\chi(\hat{v}))\right)
$$
Since $h_i\left(\hat{v}_{-i}\right)$ does not depend on $\hat{v}_i$, it is sufficient to solve
$$
\max _{\hat{v}_i}\left(v_i(\chi(\hat{v}))+\sum_{j \neq i} \hat{v}_j(\chi(\hat{v}))\right)
$$
---
$$
\max _{\hat{v}_i}\left(v_i(\chi(\hat{v}))+\sum_{j \neq i} \hat{v}_j(\chi(\hat{v}))\right)
$$
The only way the declaration $\hat{v}_i$ influences this maximisation is through the choice of $\chi$. If possible, $i$ would like to pick a declaration $\hat{v}_i$ that will lead the mechanism to pick an $x \in X$ which solves
$$
\max _x\left(v_i(x)+\sum_{j \neq i} \hat{v}_j(x)\right)
$$
Under Groves mechanisms,
$$
\chi(\hat{v})=\underset{x}{\operatorname{argmax}}\left(\sum_i \hat{v}_i(x)\right)=\underset{x}{\operatorname{argmax}}\left(\hat{v}_i(x)+\sum_{j \neq i} \hat{v}_j(x)\right)
$$
A Groves mechanism will choose $x$ in a way that solves the maximisation problem in Equation (1) when $i$ declares $\hat{v}_i=v_i$. Because this argument does not depend in any way on the declarations of the other agents, truth-telling is a dominant strategy for agent $i$

### Proof Intuition
Externalities are internalized
- agents may be able to change the choice of the mechanism to another one that they prefer, by changing their declaration
- however, their utility doesn't just depend on the choice-it also depends on their payment.
- since they get paid the (reported) valuation of all the other agents under the chosen alternative/choice, they now have an interest in maximising everyone's utility rather than just their own

Individual's incentives are aligned with the society's incentives.
In general, DS truthful mechanisms have the property that an agent's payment doesn't (directly) depend on the amount of his declaration, but only on the other agents' declarations
- the agent's declaration is used only to choose the choice, and to set other agents' payments

## Groves Uniqueness

>[!Theorem]
>In settings where agents may have unrestricted quasilinear utilities, Groves mechanisms are the only mechanisms that are both efficient and dominant-strategy truthful

# VCG Summary

VCG, and Groves mechanisms in general, are efficient and dominant-strategy truthful.

Despite having these two fantastic properties, VCG is rarely used in practice because it also has a long list of weaknesses

An important weakness of VCG is that the **finding the social-welfare maximising choice might be hard** (NP-hard)
- This is true e.g. in combinatorial auctions.
- So VCG is **not tractable** in general combinatorial auctions

# Limitations of VCG

## Individual Rationality in VCG

>[!Definition]
>**Ex Post Individual Rationality**
>A mechanism is ex post individually rational if $\forall v$, in equilibrium the utility of each agent is at least 0

- VCG in general does not give rise to individual rationality
- VCG is individual rational if two mild constraints (next slide) are satisfied

## Two Assumptions

>[!Definition]
>**Choice-set Monotonicity**
>A setting exhibits choice-set monotonicity if $\forall i, X_{-i} \subseteq X$.
>- In other words: removing any agent weakly decreases-that is, never increases - the mechanism's set of possible choices $X$.

>[!Definition]
>**No Negative Externalities**
A setting exhibits no negative externalities if $\forall i, \forall x \in X_{-i}, v_i(x) \geq 0$
>- In other words: every agent has zero or positive utility for any choice that can be made without her participation

## VCG and Individual Rationality

>[!Theorem]
>The VCG mechanism is ex-post individual rational when the choice set monotonicity and no negative externalities properties hold

### Proof
All agents truthfully declare their valuations in equilibrium. Then
$$
\begin{gathered}
u_i=v_i(\chi(v))-\left(\sum_{j \neq i} v_j\left(\chi\left(v_{-i}\right)\right)-\sum_{j \neq i} v_j(\chi(v))\right) \\
=\sum_j v_j(\chi(v))-\sum_{j \neq i} v_j\left(\chi\left(v_{-i}\right)\right)
\end{gathered}
$$
$\chi(v)$ is the choice that maximises social welfare, and so the optimisation could have picked $\chi\left(v_{-i}\right)$ instead (by choice set monotonicity). Thus,
$$
\sum_j v_j(\chi(v)) \geq \sum_j v_j\left(\chi\left(v_{-i}\right)\right)
$$
---
$$
\sum_j v_j(\chi(v)) \geq \sum_j v_j\left(\chi\left(v_{-i}\right)\right)
$$
Furthermore, from no negative externalities,
$$
v_i\left(\chi\left(v_{-i}\right)\right) \geq 0
$$
Therefore,
$$
\sum_j v_j(\chi(v)) \geq \sum_{j \neq i} v_j\left(\chi\left(v_{-i}\right)\right)
$$
And thus Equation (2) is non-negative

## Budget Balance and VCG

>[!Definition]
>**Budget Balance**
>A quasilinear mechanism is budget balanced when $\forall v, \sum_{i=1}^n p_i(s(v))=0$, where $s$ is the equilibrium strategy profile
>- VCG is not budget balanced (even in a simple single-item auction).


>[!Definition]
>**Weak Budget Balance**
A quasilinear mechanism is weakly budget balanced when $\forall v, \sum_{i=1}^n p_i(s(v)) \geq 0$, where $s$ is the equilibrium strategy profile
>- Weak budget balance requires that the mechanism does not lose money.
>- VCG is not weakly budget balanced (e.g. in the selfish routing example it had to pay the agents and didn't collect any money)

## Another Property

>[!Definition]
>**No Single-Agent Effect**
>A setting exhibits no single-agent effect if $\forall i, \forall v_{-i}, \forall x \in \operatorname{argmax}_y \sum_j v_j(y)$ there exists a choice $x^{\prime}$ that is feasible without $i$ and that has $\sum_{j \neq i} v_j\left(x^{\prime}\right) \geq \sum_{j \neq i} v_j(x)$
>- In other words, total welfare of agents other than $i$ is weakly increased by dropping $i$

## Weakly Budget-Balanced and No Single-Agent Effect

>[!Theorem]
>The VCG mechanism is **weakly budget-balanced** when the no  
**single-agent effect** property holds

### Proof
All agents truthfully declare their valuations in equilibrium. We must show that the sum of transfers (i.e. payments) from agents to the center is greater than or equal to zero
$$
\sum_i p_i(v)=\sum_i\left(\sum_{j \neq i} v_j\left(\chi\left(v_{-i}\right)\right)-\sum_{j \neq i} v_j(\chi(v))\right)
$$
From no single-agent effect condition we have that for all $i$
$$
\sum_{j \neq i} v_j\left(\chi\left(v_{-i}\right)\right) \geq \sum_{j \neq i} v_j(\chi(v))
$$
The result thus directly follows

## Ex Post Individual Rationality

>[!Theorem]
>In any Bayesian game setting in which VCG is ex post individually rational, VCG collects at least as much revenue as any other efficient and ex interim individually-rational mechanism
>- Ex interim individual rationality is a weaker condition than ex post individual rationality
>- This result is somewhat surprising: does not require dominant strategies, and hence compares VCG to all Bayes-Nash mechanisms
>- A useful corollary: VCG is as budget balanced as any efficient mechanism can be
>- It satisfies weak budget balance in every case where any Bayes Nash Incentive Compatible, efficient and ex interim individual rational mechanism would be able to do so

## Disadvantages

>[!Theorem]
>No dominant-strategy truthful mechanism is always both efficient and weakly budget balanced, even if agents are restricted to the simple exchange setting.
>- simple exchange is an environment consisting of buyers and sellers with quasilinear utility functions, all interested in trading a single identical unit of some good.

>[!Theorem]
No Bayes-Nash incentive-compatible mechanism is always simultaneously efficient, weakly budget balanced and ex interim individual rational, even if agents are restricted to quasilinear utility functions.
>- Class of Bayes-Nash incentive-compatible mechanisms includes the class of dominant-strategy truthful mechanisms
>- ex interim IR is weaker than ex post IR
