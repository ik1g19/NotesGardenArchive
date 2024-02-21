---
title: "Cooperative Games"
---

# Coalitional Games
Cooperative games are also called coalitional games

>[!Definition]
>A coalitional game with transferable utility is a pair $(N,v)$ such that
>- $N=\{1,2,...,n\}$ is a finit set of players. A subset $S$ of $N$ is called a *coalition*. The collection of call coalitions is denoted by $2^N$
>- $v : 2^N\rightarrow\mathbb{R}$ is a function associating every coalition $S$ witha  real number $v(S)$ satisfying $v(\theta)=0$. This function is called the *coalitional function* of the game

The real number $v(S)$ is called the *worth of the coalition*
If the members of $S$ agree to form the coalition, then, as a result, they can expect receieve utility $v(S)$
The utilities of all the players can be measured in a common unit (real number)
Utility can be transferred between players
The coalition of all players is called the *grand coalition*

When players form a coalition, they all agree to join it and commit to it
A coalition cannot form without the agreement of all its members
When two coalitions $S$ and $T$ are formed, we assume they are disjoint i.e. $S\cap T=\emptyset$
In a coalitional game, the value of the coalition and what players can expect to get does not depend on the behaviour of players that are not in it, nor on other coalitions that may form

# Types of Coalitional Games
## Superadditive Games
>[!Definition]
>A coalitional game $(N,v)$ is said to be *superadditive* if it satisfies $$v(s)+v(T)\leq v(S\cup T)$$ for every pair of disjoint coalitions $S,T \subseteq N$

Players have no compelling reason to form separate coalitions
Agents can earn at least as much profit by working together within the grand coalition
It is usually assumed that the agents form the grand coalition

>[!Tip]
>A game is super additive if the agents can earn more in a coalition than their individual parts combined
#### Example 1
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114221444.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114221457.png]]
#### Example 2
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114221522.png]]
## Simple Games

>[!Definition]
>A coalitional game $(N,v)$ is called *simple* if for each coalition $S$, either $v(S)=0$ or $v(S)=1$

A coalitional game is simple if the worth of any coalition is either 1 or 0
A coalition $S$ is called *winning* if $v(S)=1$ and is called losing if $v(S)=0$
Sometimes it is convenient to represent simple games by indicating the family of winning coalitions $$W=\{S\subseteq N\text{ }|\text{ }v(S)=1\}$$
Simple games can model committee votes
#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114222113.png]]
## Weighted Majority Games
Weighted majority games are a special case of simple games
>[!Definition]
>A coalitional game is a *weighted majority game* if there exists a *quota* $q\geq 0$ and non-negative real weights $w_i$,$i\in N$, one for each player, such that the worth of each non-empty coalition $S$ is $$v(S)\begin{cases}1 & \sum_{i\in S}w_i\geq q\\ 0 & \sum_{i\in S}w_i < q\end{cases}$$

>[!Tip]
>In a weighted majority game, each player or coalition is assigned a weight or value, and a coalition is considered winning if the sum of the weights of its members exceeds a certain threshold or quota.

A weighted majority game can be given an *explicit representation* denoted by $$[q;w_1,...,w_n]$$
#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114222245.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114223051.png]]

# Outcomes
>[!Definition]
>Given a coalitional game $(N,v)$, a *coalition structure* over $N$ is a partition of $N$, i.e. a collection of non-empty subsets $CS=\{S_1,...,S_k\}$ such that
>- $\cup_{j=1}^k S_j=N$, and
>- $S_i \cap S_j = \emptyset$ for any $i,j\in \{1,...,k\}$ such that $i\neq j$

We denote the space of coalition structures over $N$ by $CS_N$

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230114223554.png]]

>[!Definition]
>Given a coalition game $(N,v)$, a vector $x=(x_1,...,x_n)\in\mathbb{R}^n$ such that $$x_i \geq 0$$
>For all $i\in N$ is called a *payoff vector*

>[!Definition]
>An *outcome* of a coalitional game $(N,v)$ is a pair $(CS,x)$, where $CS$ is a coalition structure over $N$ and $x$ is a payoff vector

Given a payoff vector $x$, we write $$x(S)=\sum\limits_{i\in S}x_i$$ to denote the total payoff of a coalition $s\subseteq N$

>[!Defintion]
>Given a coalitional game $(N,v)$ and a coalition structure $CS=\{S_1,...,S_k\}$, a payoff vector $x$ is called efficietn if $$x(S_j)=v(S_j)$$ for every $j\in \{1,...,k\}$

When players divide into coalitions, we can assume they divide its worth among themselves
They cannot assign to themselves more than their worth
It is unreasonable to assume they will assign less than the total, wasting part of their worth
A payoff vector is efficient for a coalition structure if every coalition gets exactly its worth

>[!Definition]
>Given a coalitional game $(N,v)$, a payoff vector $x$ is called *individually rational* if $$x_i\geq v(\{i\})$$ for all $i\in N$

Each player $i$ can guarantee themselves $v(\{x_i\})$
It is reasonable to assume that a player will agree to be part of a coalition if they can at least get as much as they would get by staying alone

>[!Defintion]
>Let $(N,v)$ be a coalitional game and $CS$ a coalition structure. A vector $x$ is called an *imputation* if it is efficient for $CS$ and is individually rational

It is reasonable to assume that players will look for an outcome where each coalition gets its worth and where they don't commit to join forces with others while they'd be better off by themsevles
Then the only outcomes we will consider are those where the vector is an imputation
Not all such outcomes are ideal or desirable though
We evaluation outcomes following different criteria
- *Stability* - What are the incentive for a player to stay on the coalition structure
- *Fairness* - How well each agent's payoff relfects their contribution

# The Core
Consider a coalitional game $(N,v)$ and an outcome $(CS,x)$ where $x$ is an imputation
If $x(S)<v(S)$ for some coalition $S$, the agents in $S$ could do better by abandoning the coalition structure $CS$ and forming a coalition of their own

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115183207.png]]

This outcome is unstable because some players will have an incentive to break the coalition structure

>[!Definition]
>The *core* of a coalitional game $(N,v)$, denoted by $\text{core}(N,v)$, is the collection of all outcomes $(CS,x)$ where $x$ is an imputation such that $$x(S)\geq v(S)$$ for every $s\subseteq N$

## Core of Superadditive Games
For superadditive games, the core contains outcomes based on the grand coalition and is the set of all vectors $x$ that satisfy:
- $x_i>0$ for all $i\in N$
- $x(N)=v(N)$
- $x(S)\geq v(S)$ for all $S\subseteq N$

#### Example
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115183811.png]]
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115183821.png]]
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115183833.png]]

## Games with an Empty Core
Consider the following three-player majority game $(N,v)$ where $$N=\{1,2,3\}$$ and $$v(S)\begin{cases}1 & |S|\geq 2\\ 0 & |S|< 2\\\end{cases}$$ for all $S\subseteq N$

A coalition $S$ is winning if it includes at least two players
This is a superadditive game, so we assume the outcome is based on the grand coalition

We show the game has an empty core
For any outcome to be in the core it must be the case that $$\begin{vmatrix}x_1+x_2\geq x_1 & x_1 + x_3 \geq 1 & x_2 + x_3 \geq 1 \\ \end{vmatrix}$$
This means that $$x_1 + x_2 + x_3 \geq \frac{3}{2}$$ contradicting the efficiency requirement $$x_1 + x_2 + x_3 = 1$$
So the core is empty

# The Shapley Value
The Shapley value is a solution concept that tries to capture the notion of fairness
It is usually formulated with respect to the grand coalition and it assigns to every coalition game an imputation
Based on the inutation that the payment that each agent recieves should be proptional to their contribution

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115185756.png]]
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115185812.png]]
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115185843.png]]

The *marginal contribution* of an agent $i$ with respect to a permutation $\pi$ in a coalitional game $(N,v)$ is denoted by $\Delta_\pi^{(N,v)}(i)$ and given by $$\Delta_\pi^{(N,v)}(i)=v(S_\pi (i)\cup \{i\})-v(S_\pi (i))$$
This quantity measures by how much $i$ increases the value of the coalition consiting of its predecessors when $i$ joins the coalition
We define the Shapley value of a player $i$ as the average marginal contribution, where the average is taken over all permutation of $N$

>[!Defintion]
>Given a coalitional game $(N,v)$ with $|N|=n$, the Shapley value fo a player $i\in N$ denoted by $Sh_i(N,v)$ is given by $$Sh_i(N,v)=\frac{1}{n!}\sum\limits_{\pi\in \Pi_N}\Delta_\pi^{(N,v)}(i)$$

#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115190520.png]]

## Properties of the Shapley Value
The Shapley value is efficient
- i.e. it distributes the value of the grand coalition among all agents

>[!Proposition]
>For any coalitional game $(N,v)$ $$\sum\limits_{i=1}^n Sh_i(N,v)=v(N)$$

A player $i$ is called a *dummy player* if for any coalition $S\subseteq N$, $v(S)=v(S\cup \{i\})$
The Shapely value does not allocate any payoff to dummy players
- i.e. those players who do not contribute to any coalition

>[!Proposition]
>For any coalitional game $(N,v)$, if a player $i$ is a dummy player then $$Sh_i(N,v)=0$$

Two players $i$, $j$ are symmetric if they contribute equally to each coalition
- i.e. for all $S\subseteq N$, $v(S\cup \{i\})=v(S\cup \{j\})$
>[!Proposition]
>For any coalitional game $(N,v)$, if $i, j\in N$ are symmetric then $$Sh_i(N,v)=Sh_j(N,v)$$

Consider players $N$ involved in coalitional games $(N,v)$ and $(N,v')$
The sum of $(N,v)$ and $(N,v')$ is the game $(N,v+v')$
>[!Proposition]
>Given two coalitional games $(N,v)$ and $(N,v')$ and their sum $(N,v+v')$, we have $$Sh_i(N,v+v')=Sh_i(N,v)+Sh_i(N,v')$$ for all players $i\in N$

We have seen that the Shapley value has the following properties
- Efficiency
- Dummy player
- Symmetry
- Additivity
These properties can be used to simplify the computation of the Shapley value

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115201651.png]]

# The Banzhaf Index
Another solution concept motivated by fairness
Measures the players' expected marginal contributions
Instead of averaging over all permutations of players, it averages over all coalitions in the game

>[!Defintion]
>Given a coalitional game $(N,v)$ with $|N|=n$, the *Banzhaf index* of a player $i\in N$ denoted by $Ba_i(N,v)$ is given by $$Ba_i(N,v)=\frac{1}{2^{n-1}}\sum\limits_{S\subseteq N \setminus \{i\}}(v(S\cup\{i\})-v(S))$$

The Banzhaf index satisfies the same properties as the Shapley value, except efficiency

# Power of a Player
The Banzhaf index and Shapley value measure the power of a player
- i.e. the probability that the player can influence the outcome of the game

A player is said to be *pivotal* for a coalition $S\subseteq N$ in a game $(N,v)$, if $v(S)=1$ and $v(S\setminus \{i\})=0$
A player is *pivotal* for a permutation $\pi:N\rightarrow N$ if it is pivotal for the coalition $S_\pi (i)\cup\{i\}$ consisting of the player and the predecessor

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20230115202847.png]]