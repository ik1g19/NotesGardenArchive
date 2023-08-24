---
title: Intro to Algorithmic Mechanism Design
---
# Mechanism Design
In systems with strategic participants:
- The system designer must anticipate strategic behaviour to create good and reliable design
- We cannot expect participants to behave against their own interests

**Goal**: Design rules so that strategic behaviour by participants leads to a desirable outcome

>[!Tip]
>Roughly speaking
>Assuming unknown individual utilities, we ask whether we can design a game such that, no matter what the secret utilities of the agents actually are, the equilibrium of the game is guaranteed to have a set of certain desired properties

# Algorithmic Mechanism Design (AMD)

A **mechanism** is an algorithm where the input is withheld by strategic selfish agents
AMD exists in the intersection between economic game theory and computer science

Settings in which:
- A center wants to solve an optimization problem but
- The inputs to this problem are the private information of self-interested agents

The center must design a mechanism that:
- Solves the optimization problem while
- Inducing the agents to act as the mechanism designer wishes (ideally truthfully revealing their information)

## AMD vs. Classical Economic Mechanism Design

AMD considers computational constraints to be of central importance
- Mechanisms that cannot be efficiently implemented in polynomial time are not considered to be viable solutions to a mechanism design problem
- Analytic tools of theoretic computer science such as worst case analysis and approximation ratios are employed

## Auctions

### Types of Auctions
- Single good
	- English auction
	- Dutch auction
	- First-price sealed-bid auction
	- Second-price sealed-bid (Vickrey) auction
- Multiunit auctions
- Combinatorial auctions
- Double auctions

### Single-Item Auctions
A seller with a single item
$n$ strategic bidders
Each bidder $i$ has a private valuation (or willingness to pay) $\theta_i$ for the item
Our bidder utilitiy model is a quasilinear utility model
- If $i$ loses, and has to pay $p_i$, their utility is $-p_i$
	- In auctions where only winners pay, $i$'s utility is 0
- If $i$ wins at a price $p_i$, their utility is $u_i(\theta_i)=\theta_i-p_i$

We are assuming
- Independent private value model i.e. a bidder's valuation does not depend on other bidder's valuations
- Bidders cannot collude

### Games Induced by Vickrey Auctions
>[!note]
>Vickrey Auction
>- The highest bid wins and pays the second-highest bid.
>- If both bidders bid the same value, then choose a tie-breaking rule, e.g.: $A$ wins, or $B$ wins, or neither win (item is unallocated).
>- The loser's utility is zero
>- The winner's utility is: winner's value - loser's bid

Let $b_i$ denote the bid placed by bidder $i$
Let $b=\left(b_1, b_2, \ldots, b_n\right)$ denote the bid profile of all bidders.
The set of **actions** available to each bidder is all possible bids that they can place
- virtually any non-negative real,
- unless there are rules in the auction, e.g. "only place integer bids", or "don't place a bid less than £3" (reserve price)
Let $u_i(b)$ denote the utility of bidder $i$ given bid profile $b$.
The **payoff (utility)** of each bidder $i$ depends on the outcome (allocation + payment), which in turn depends on $b_i$ and the bids placed by the other bidders
The game induced by the Vickrey auction (in fact, any auction) is a **Bayesian game**.

## Normal Form (Strategic Form) Game

A tuple $(N, A, u)$ where
- $N=\{1, \ldots, n\}$ is a finite set of agents.
- $A=A_1 \times \ldots \times A_n$, where $A_i$ is a finite set of actions (i.e. pure strategies) available to agent $i$.
- $u=\left(u_1, \ldots, u_n\right)$, where $u_i: A \mapsto \mathbb{R}$ is the utility (a.k.a. payoff) function for player $i$.

>[!Tip]
>$S_i$ is used to refer to the set of all (pure and mixed) strategies available to agent $i$
>$s_i$ is used to denote a mixed strategy of agent $i$
>$A_i$ is used to denote the set of actions (or pure strategies) available to agent $i$

## Bayesian Game

A tuple $(N, A, \Theta, p, u)$ where
- $N=\{1, \ldots, n\}$ is a finite set of agents
- $A=A_1 \times \ldots \times A_n$, where $A_i$ is the set of actions available to agent $i$
- $\Theta=\Theta_1 \times \ldots \times \Theta_n$ where $\Theta_i$ is the type space of player $i$
- $p: \Theta \mapsto[0,1]$ is a common-prior probability distribution on $\Theta$
- $u=\left(u_1, \ldots, u_n\right)$, where $u_i: A \times \Theta \mapsto \mathbb{R}$ is the utility function for player $i$

### vs. Normal Form Games
- The types of the agents determine which normal-form game they are playing.
- Agents don't know the type of the other agents, only $p$ is known.
- Based on $p$, each agent can assign a probability to what game they're playing.

### Bayesian Game with Strict Incomplete Information
A tuple $(N, A, \Theta, u)$ where
- $N=\{1, \ldots, n\}$ is a finite set of agents
- $A=A_1 \times \ldots \times A_n$, where $A_i$ is the set of actions available to agent $i$
- $\Theta=\Theta_1 \times \ldots \times \Theta_n$ where $\Theta_i$ is the type space of player $i$
- $u=\left(u_1, \ldots, u_n\right)$, where $u_i: A \times \Theta \mapsto \mathbb{R}$ is the utility function for player $i$
Sometimes **$p$ is not known**. That is we have no probabilistic information in the model

### Bayesian Game Setting
A tuple $(N, O, \Theta, p, u)$
- $N=\{1, \ldots, n\}$ is a finite set of agents
- $O$ is a set of outcomes
- $\Theta=\Theta_1 \times \ldots \times \Theta_n$ is a set of possible joint type vector
- $p$ is a common-prior probability distribution on $\Theta$
- $u=\left(u_1, \ldots, u_n\right)$, where $u_i: O \times \Theta \mapsto \mathbb{R}$ is the utility function for player $i$

The Bayesian Game Setting does not include actions for the agents and instead defines the utility function over the set of possible outcomes