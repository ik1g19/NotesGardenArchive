---
title: Basics of Mechanism Design
---
# Mechanism

>[!Definition]
>A (deterministic) mechanism (for a Bayesian game setting $(N, O, \Theta, p, u))$ is a pair $(A, M)$, where
>- $A=A_1 \times \ldots \times A_n$, where $A_i$ is the set of actions available to agent $i$, and
>- $M: A \mapsto O$ maps each action profile to an outcome

## Direct Mechanism

A **direct mechanism** is a mechanism in which the only action available to each agent is to announce his private information
So in a direct mechanism $A_i=\Theta_i$ for each $i$
A (deterministic) direct mechanism (for a Bayesian game setting $(N, O, \Theta, p, u))$ is a pair $\color{#ff82b2}(A, M)$, where
- $A=A_1 \times \ldots \times A_n$, where $\color{#ff82b2}A_i=\Theta_i$ is the set of actions available to agent $i$, and
- $M: A \mapsto O$ maps each action profile to an outcome.

## Quasilinear Utility Settings

In a **quasilinear utility setting**:
- the set of outcomes is $O=X \times \mathbb{R}^n$ for a finite set of choices $X$, and
- when outcome $o=\left(x,\left(p_1, \ldots, p_n\right)\right)$ is chosen, the utility of an agent $i$ given joint type $\theta$ is $u_i(o, \theta)=u_i(x, \theta)-p_i$

When we assume **Independent Private Values** (IPVs), we can write agent $i$ 's utility function as $u_i\left(x, \theta_i\right)$.

We can then also refer to an agent's **valuation** for choice $x$, written $v_i(x)=u_i\left(x, \theta_i\right)$
- $v_i$ is the maximum amount of money $i$ is willing to pay for the mechanism to choose $x$.
- The notation of $v_i$ does not explicitly refer to $\theta_i$, but an agent's valuation does depend on her type $\left(\theta_i\right.$ is dropped for simplicity of notation and because it can be inferred from the context)

### Mechanisms in Quasilinear Settings

>[!Definition]
>**Quasilinear Mechanism**
>A quasilinear mechanism is a triple $(A, \chi, p)$, where
>- $A=A_1 \times \ldots \times A_n$, where $A_i$ is the set of actions available to agent $i$,
>- Choice function $\chi: A \mapsto X$ maps each action profile to a choice in $X$, and
>- Payment function $p: A \mapsto \mathbb{R}^n$ maps each action profile to a payment for each agent

## Bayes-Nash Equilibrium

In normal-form games we have Nash equilibrium
In Bayesian form games we have **Bayes-Nash equilibrium**
They are conceptually the same: A Bayes-Nash equilibrium is a mixed-strategy profile $s$ such that each $s_i$ is a best response to $s_{-i}$.
It's only that the calculation is more involved as to compute the best response, each agent has to take into account the probability distribution $p$ over the set of possible joint type vectors $\Theta$

## Mechanism Design

Either:
- Perform an **optimisation** problem, given that the **values** of (some of) the inputs are **unknown** (withheld by the agents)
- Design a game that **implements** a particular **social choice function** in equilibrium, given that the designer does not know agents' preferences and the agents might lie

## Social Choice Setting

$\color{#ff82b2}O$ : a set of outcomes, e.g.
- possible locations for a bridge or library
- possible meeting times
- candidates for local MPs

$\color{#ff82b2}N$ : a set of agents who have preferences over the outcomes

**Goal**: Designing/picking a social choice function $f$ that maps from agents' preferences to a particular outcome, which is enforced

## Bayesian Game Setting vs. Social Choice Setting

Bayesian game setting extends the social choice setting to a new setting where agents are **strategic** and hence cannot be relied upon to disclose their preferences honestly

## Implementation in Dominant Strategies

A mechanism $M$ implements a social choice function $f$ in **dominant strategies** if for some dominant strategy equilibrium of the induced game, we have that the mechanism $M$ chooses the same outcome (given action profile of the agents) as does $f$ (given true utilities of the agents)

## Dominant-Strategy Truthful Mechanism

A strategy profile $\left(s_1, \ldots, s_n\right)$ in which every $s_i$ is a dominant strategy for agent $i$ is called an equilibrium in dominant strategies

>[!Definition]
>**Dominant-Strategy Truthfulness**
>A direct mechanism is dominant-strategy truthful if, for every agent $i$, telling the truth (i.e. revealing the true valuation) maximises $i$ 's utility, no matter what strategy the other players pick.

Also known as
- **strategy-proof** mechanism
- **dominant-strategy incentive-compatible** mechanism
- **truthful** mechanism

If Mechanism $M$ is dominant-strategy truthful then truth-telling is a (very weakly) dominant strategy for each agent

## Dominant Strategy Truthfulness in Single-Item Auctions

A single-item auction $(\Theta, \chi, p)$ is dominant-strategy truthful if for each bidder $i$, bidding $b_i=\theta_i$ maximises $i$ 's utility, no matter what bids the other bidders place:
$$
v_i\left(\chi\left(\theta_i, b_{-i}\right)\right)-p\left(\theta_i, b_{-i}\right) \geq v_i\left(\chi\left(b_i, b_{-i}\right)\right)-p\left(b_i, b_{-i}\right), \forall b_i \forall b_{-i} \forall \theta_i
$$
We can actually write the above inequality as
$$
v_i\left(\chi\left(\theta_i, \theta_{-i}\right)\right)-p\left(\theta_i, \theta_{-i}\right) \geq v_i\left(\chi\left(b_i, \theta_{-i}\right)\right)-p\left(b_i, \theta_{-i}\right), \forall b_i \forall \theta_{-i} \forall \theta_i
$$

To simplify notation, sometimes we write $v_i$ as a function of action profiles instead of outcomes, e.g. write $v_i\left(b_i, b_{-i}\right)$ instead of $v_i\left(\chi\left(b_i, b_{-i}\right)\right)$

### Vickrey Auction is Dominant-Strategy Truthful
#### Proof
Assume that the other bidders bid in some arbitrary way. We show that $i$ maximises her utility by bidding truthfully. We break the proof into two cases:
1. By bidding honestly, $i$ wins the auction.
2. By bidding honestly, $i$ loses the auction.
**Case 1**: By bidding honestly, $i$ wins
- If $i$ submitted a higher bid, she would still win and pay the same amount
- If $i$ submitted a lower bid, she would either still win and pay the same amount... or lose and get utility zero.
**Case 2**: By bidding honestly, $i$ loses
- If $i$ submitted a lower bid, she would still lose and pay nothing
- If $i$ submitted a higher bid, she would either lose and still pay nothing... or win and pay more than her valuation.
In either case, bidding truthfully maximises $i$'s utility