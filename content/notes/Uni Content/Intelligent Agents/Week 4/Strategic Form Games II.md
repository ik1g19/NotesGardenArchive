---
title: "Strategic Form Games II"
---

# Mixed Nash Equilibria
To guarantee the existence of equilibria, we extend the concept of a strategic form game with the notion of mixed strategy

> [!Definition]
> In a strategic form game, a mixed strategy $\sigma_i$ for player $i$ is a probability distribution over the set of strategies $S_i$, i.e. a function $\sigma_i : S_i\rightarrow [0,1]$ such that $$\sum\limits_{s_i\in S_i}\sigma_i(s_i)=1$$

To distinguish from mixed strategies, each strategy $s_i\in S_i$, for all players $i$, a pure strategy

Given a strategic form game, for each player $i$, let $\Sigma_i$ be the set of all mixed strategies over $S_i$, i.e. $$\Sigma_i=\{\sigma_i | \sigma_i : S_i \rightarrow [0,1],\sum\limits_{s_i\in S_i}\sigma_i(s_i)=1\}$$
Let $\Sigma = \Sigma_1 \times ... \times \Sigma_n$
We call every element $(\sigma_1 ,..., \sigma_n)\in \Sigma$ a mixed strategy or mixed strategy combination

Given a mixed strategy profile $(\sigma_1,...,\sigma_n)$, the expected utility of player $i$ is given by $$EU_i(\sigma_1,...,\sigma_n)=\sum\limits_{(s_1,...,s_n)\in S_1\times ... \times S_n} \bigg( \bigg(\prod\limits_{j\in N}\sigma_j(s_j) \bigg) u_i(s_1,...,s_n) \bigg)$$
>[!Tip]
> The expected utility is the sum of the weighted utilities for each possible outcome
> Expected Utility of Player 1:
> Probability of Player 1's row $\times$ Probability of Player 2's column $\times$ Player 1's utility
> Do this for every box and sum it all together

## Mixed Extension
> [!Definition]
> Let $$G=\langle N,S_1,...,S_n,u_1,...,u_n\rangle$$
be a strategic form game. The **mixed extension** of $G$ is the game $$\Gamma = \langle N,\Sigma_1,..., \Sigma_n, U_1,...,U_n\rangle$$
Where
> - Each $\Sigma_i$ is the set of mixed strategies of player $i$ over $S_i$
> - Each $U_i : \Sigma \rightarrow \mathbb{R}$ is a payoff function that associates with each mixed strategy combination $(\sigma_1,...,\sigma_n)\in \Sigma$ its expected utility
$$U_i(\sigma_1,...,\sigma_n)=EU_i(\sigma_1,...,\sigma_n)=\sum\limits_{(s_1,...,s_n)\in S_1\times ... \times S_n} \bigg( \bigg(\prod\limits_{j\in N}\sigma_j(s_j) \bigg) u_i(s_1,...,s_n) \bigg)$$

- A mixed extension is a "new" game built on top of a strategic-form game with only pure strategies
- Each player now has a new set of strategies - i.e. all the mixed strategies defined over their original strategy set
- Each player also has a new utility function, which, for each mixed strategy combination, outputs the expected utility determined by the players selecting those mixed strategies
- This generalises the concept of a strategic-form game
	- Because pure strategies are special cases of mixed strategies - i.e. pure strategies correspond to those cases where a probability distribution assigns 1 to one pure strategy

# Generalising Nash Equilibrium
We want to generalise the concept of a Nash Equilibrium to mixed strategies
In order to do so, we first generalise the concept of a best response
> [!Definition]
> Let $G$ be a strategic-form game and let $\Gamma$ be its mixed exntension. Let $\sigma_{-i}$ be a mixed strategy vector for all the players not including $i$. Player $i$'s' mixed strategy $\sigma_i$ is called a **best response** to $\sigma_{-i}$ if $$EU_i(\sigma_i,\sigma_{-i})=\max\limits_{\sigma_i'\in\Sigma_i}EU_i(\sigma_i',\sigma_{-i})$$ 

We can now generalise the notion of a nash equilibrium
> [!Definition]
> A mixed strategy combination $(\sigma_1,...,\sigma_n)$ is a **mixed strategy Nash equilibrium** if $\sigma_i$ is a best response to $\sigma_{-i}$ for every player $i\in N$

Since pure strategies are a special form of mixed strategies, a pure Nash equilibrium is a special form of mixed Nash equilibrium
# Computing Mixed Nash Equilibria
Pure Nash equilibria do not always exist
This is not the case for mixed Nash equilibria
> [!Theorem (Nash, 1951)]
> Every strategic-form game has mixed extension that has mixed strategy Nash equilibria

> [!Theorem (Daskalakis, Goldberg, Papadimitriou, 2009)]
> Finding mixed Nash equilibria in a strategic-form game is PPAD-cmplete
## 2 x 2 Games
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102173113.png)
We represent a mixed strategy for player 1 as $x\in [0,1]$
- Play $T$ with probability $x$
- Play $B$ with probability $1-x$
We represent a mixed strategy for player 2 as $y\in [0,1]$
- Play $L$ with probability $y$
- Play $R$ with probability $1-y$
### Best Reponse Method
Compute the best response functions for mixed strategies, and draw a graphical representation of these functions
The best response function $br_1(y)$ for player 1 is $$br_1(y)=argmax_{x\in[0,1]}EU_1(x,y)$$
The best response function $br_2(x)$ for player 2 is $$argmax_{y\in[0,1]}EU_2(x,y)$$
The intersection between the best response functions will give the mixed Nash equilibria of the game
#### Example
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102173528.png)
The game has 2 pure strategy Nash equilibria $(H,H)$ and $(T,T)$
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102173637.png)
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102173653.png)
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102173802.png)
The intersection of the graphs of $br_1(y)$ and $br_2(x)$ gives us the set of all equilibria of the game
The pure strategy equilibria are included
![](content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221102174028.png)
### The Indifference Principle
> [!Theorem (indifference principle)]
> Let $(\sigma_1,...,\sigma_n)$ be a mixed Nash equilibrium of a strategic-form game, and let $s_i$ and $s_i'$ be two pure strategies of player $i$
> If $$\sigma_i(s_i)>0\text{ and }\sigma_i(s_i')>0,$$
> Then $$EU_i(s_i,\sigma_{-i})=EU_i(s_i',\sigma_{-i})$$

The indifference principle says that if in a mixed Nash equilibrium a player assigns positive probability to two different pure strategies, then the expected payoff of playing those strategies is the same
> [!Definition]
> We call a mixed strategy $\sigma_i$ of player $i$ a **completely mixed strategy** (or **fully mixed**) if $$\sigma_i(s_i)>0$$
> for every pure strategy $s_i\in S_i$
> We call a mixed Nash equilibrium $\sigma_1,...,\sigma_n$ a **completely mixed Nash equilibrium** (or **fully mixed**) if for every player $i$, the strategy $\sigma_i$ is completely mixed

The indifference principle tells us that if a completely mixed Nash equilibrium exists, then for each player the expected utility of playing any pure strategies (under the given equilibrium) is the same
Each player is indifferent to playing a pure strategy over another

>[!Tip]
>You can use the indifference principle to show a set of strategies does not form a mixed nash equilibirum
>Show that the expected utility of the player's strategies are not equal, since they are not equal - they cannot form a mixed nash equilibrium
#### Example
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107122216.png]]
### The Indifference Principle (2x2)
> [!Theorem]
> A pair of probability distributions $(x,y)\in (0,1)^2$ is a mixed Nash Equilibrium in the generic $2\times 2$ game if and only if $$EU_1(T,y)=EU_1(B,y)\text{ and }EU_2(L,x)=EU_2(R,x)$$

This provides a method finding completely mixed Nash equilibria
1. Check the equality $$EU_1(T,y)=EU_1(B,y)$$ and find solutions for $y$
2. Check the equality $$EU_2(L,x)=EU_2(R,x)$$ and find solutions for $x$
Any pair of solutions $(x,y)\in (0,1)^2$ is a mixed Nash equilibrium
We are dealing with linear inequalities, so we can solve them in polynomial time
#### example
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107122957.png]]
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107123131.png]]
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107123158.png]]
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107123408.png]]