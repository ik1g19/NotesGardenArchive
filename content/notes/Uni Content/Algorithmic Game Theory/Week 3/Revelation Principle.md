---
title: Revelation Principle
---
# Revelation Principle

The **Revelation Principle** tell us that any social choice function that can be implemented (in Dominant Strategy) by any mechanism, can also be implemented by a direct, truthful mechanism

>[!Theorem]
>**Revelation Principle**
>For every mechanism in which every participant has a dominant strategy (no matter what her private information), there is an equivalent direct dominant-strategy truthful mechanism

## Proof

The revelation principle claims that: for every mechanism in which every participant has a dominant strategy (no matter what its private information), there is an equivalent direct dominant-strategy truthful mechanism.
Consider an arbitrary, non-truthful mechanism (e.g. may be indirect)
Recall that a mechanism defines a game, and consider a DS equilibrium $s=\left(s_1, \ldots, s_n\right)$
![|600](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230228210943.png)
We can construct a new direct mechanism
This mechanism is truthful by exactly the same argument that $s$ was a DS equilibrium in the original mechanism
The agents don't have to lie, because the mechanism already lies for them.
So, $s_i^{\prime}\left(\theta_i\right)=\theta_i$
![|600](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230228211033.png)

The Revelation Principle is good for:
- recognition that truthfulness is not a restrictive assumption
- for analysis purposes, we can consider only truthful mechanisms, and be assured that such a mechanism exists
- recognition that indirect mechanisms can't do (inherently) better than direct mechanisms

The set of equilibria is not always the same in the original mechanism and revelation mechanism
- of course, we've shown that the revelation mechanism does have the original equilibrium of interest
- however, in the case of indirect mechanisms, even if the indirect mechanism had a unique equilibrium, the revelation mechanism can also have new, bad equilibria

# Direct vs. Indirect Mechanisms

**Direct** - the mechanism asks agents to reveal their type
- Set of actions available to each agent is equal to their type space, $A_i=\Theta_i$
- Agents each simultaneously send a single message to the center (the mechanism)
**Indirect** - agents may send a sequence of messages; in between, information may be (partially) revealed about the messages that were sent previously (like extensive form game)

## Advantages of an Indirect Mechanism

- A direct truthful mechanism forces the agents to reveal their types completely. There might be settings where agents are not willing to compromise their privacy to this degree
- Full revelation can sometimes place an unreasonable burden on the communication channel
- Agents' equilibrium strategies might be difficult to compute; in this case the additional burden absorbed by the mechanism might be considerable

# Characterization of Dominant Strategy Truthful Mechanisms

In some applications, maximising social welfare is a hard computational problem (NP-complete), but there are efficient algorithms that approximate the maximum social welfare
Can we implement their corresponding social choice functions?

In some settings the mechanism designer has some other objectives that she wants to optimise. E.g.
- revenue
- some kind of fairness
- makespan (in scheduling applications)

## Direct Characterisation

Let $X_i\left(\hat{v}_{-i}\right) \subseteq X$ denote the set of choices that can be selected by the choice rule $\chi$ given the declaration $\hat{v}_{-i}$ by the agents other than $i$ (i.e. the range of $\left.\chi\left(., \hat{v}_{-i}\right)\right)$

>[!Theorem]
A mechanism is dominant-strategy truthful if and only if it satisfies the following conditions for every agent $i$ and every $\hat{v}_{-i}$ :
>1. The payment function $p_i(\hat{v})$ can be written as $p_i\left(\hat{v}_{-i}, \chi(\hat{v})\right)$.
>2. $\forall v_i, \chi\left(v_i, \hat{v}_{-i}\right) \in \operatorname{argmax}_{x \in X_i\left(\hat{v}_{-i}\right)}\left(v_i(x)-p_i\left(\hat{v}_{-i}, x\right)\right)$


- An agent's payment can only depend on other agents' declarations and the selected choice
- The mechanism optimises for each agent: taking the other agents' declarations and the payment function into account, from every player's point of view the mechanism selects the most preferable choice.