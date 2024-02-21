---
title: "Strategic Form Games"
---

> [!Definition]
> A strategic form game is a tuple $$\langle N,S_1,...,S_n,u_1,...,u_n \rangle$$
Where
> - $N=\{1,...,n\}$ is a finite set of players
> - $S_i$ is a finite set of strategies for each player $i$
> - $u_i=S_1\times ...\times S_n\rightarrow \mathbb{R}$ is a utility function for player $i$

Each $(s_1,...,s_n) \in S_1 \times ... \times S_n$ is called a strategy profile or strategy combination
Strategy profiles are also denoted by $$(s_i,s_{-i})$$
to highlight the strategy of player $i$
$s_{-i}$ denotes the strategy combination with player $i$ $$s_{-i}=(s_1,...,s_{-i},s_{i+1},...,s_n)$$
We assume players are rational decision makers and have complete and common knowledge about each others strategies, utilities and their rationality

# Strictly Dominated Strategies
In a situation where the same choice will yield the player 1 a better outcome regardless of the player 2's choice, we say that the other player 2's choice is strictly dominated by player 1's

> [!Definition]
> A strategy $s_i$ of player $i$ is strictly dominated if there exists another strategy $s_i'$ of player $i$ such that for each strategy vector $s_{-i}\in S_{-i}$ of the other players $$u_i(s_i ,s_{-i})<u_i(s_i',s_{-i})$$
- In this case we say $s_i$ is strictly dominated by $s_i'$
- We have assumed all players are rational and know about each others rationality
- Therefore we can assume that rational players will never play strictly dominated strategies, which can be eliminated from the game

Not all games have strictly dominated strategies, so we cannot always reach an outcome by elimination

When eliminating strictly dominated strategies, the result is always independent of the order of elimination

## Prisoner's Dilemna Example
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221020163339.png]]
# Weakly Dominated Strategies
> [!Definition]
A strategy $s_i$ of player $i$ is weakly dominated if there exists another strategy $s_i'$ of player $i$ satisfying  the following two conditions
> - For every strategy vector $s_{-i}\in S_{-i}$ of the other players $$u_i(s_i,S_{-i})\leq u_i(s_i',s_{-i})$$
> - There exists a strategy vector $t_{-i}\in S_{-i}$ of the other players such that $$u_i(s_i,t_{-i})< u_i(s_i',t_{-i})$$

In this case we say $s_i$ is weakly dominated by $s_i'$
We can then assume rational players will never play weakly dominated strategies, which can then be eliminated from the game

Weakly dominated strategies cannot always be performed
Unlike strictly dominated strategies, the order of elimination does matter and we can get different results
#### Example 1
![[notes/Uni Content/Intelligent Agents/Images/weak1.gif]]
#### example 2
![[notes/Uni Content/Intelligent Agents/Images/weak2.gif]]
#### example 3
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221116135136.png]]
# Pure Nash Equilibria
We cannot perform elimination of dominated strategies in all games

A player's best response to a strategy profile is a choice that gives the player the highest utility
A best response does not have to be unique

> [!Definition]
Let $S_{-i}$ be a strategy vector for all the players not including $i$
Player $i$'s strategy $s_i$ is called a best response to $S_{-i}$ if $$u_i(s_i,s_{-i})=\max\limits_{s_i'\in S_i}u_i(s_i',s_{-i})$$

#### example
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221025190126.png]]
The strategy combination $(C,F)$ is such that the strategies are the best response to each other
If players select this combination, none of them will benefit from changing their choices, because they have chosen a best response
$(C,F)$ is an example of **Nash Equilibrium**

## Nash Equilibria
> [!Definition]
> A strategy combination $(s_1,...,s_n)$ is a **Nash Equilibrium** if $s_i$ is a best response to $s_{-i}$ for every player $i\in N$

Determining the existence of a nash equilibrium for a strategic form game is in logarithmic space

## Computing Nash Equilibria
For each player, compute the strategy combination where their strategy is a best response
Take the intersection of the sets of all players
#### example
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221025193701.png]]
Player 1's combinations:
$\{(B,D),(A,E),(C,F)\}$
Player 2's combinations:
$\{(A,D),(B,E),(C,F)\}$
The intersection $(C,F)$ is a nash equilibrium

Alternatively, for each strategy combination, check if any player can increase their utility by deviating
If they can't, it is a nash equilibrium

# Coordination Games
Nash equilibria may not be unique
Coordination games are exmaples of games with multiple Nash Equilibria
Equilibria arise when players coordinate on the same strategy
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221026142837.png]]

# Matching Pennies
Not all games have Nash Equilibria
Matching pennies is an example

Two players toss a penny simultaneously
If the outcomes match, player 1 keeps both pennies
If the outcomes dont match, player 2 keeps both coins

# Iterated Elimination and Nash Equilibria
Let $(s_1,...,s_n)$ be a strategy profile obtained from iterated elimination of strictly dominated strategies
Then $(s_1,...,s_n)$ is a nash equilibrium
$(s_1,...,s_n)$ is the unique equilibrium of the game
Iterated elimination of strictly dominated strategies does not eliminate equilibria

Given a game $G$, let $G^*$ be the game obtained by iterated elimination of weakly dominated strategies
The set of equilibria of $G^*$ is a subset of equilibria of $G$
Meaning the iterated elimination of weakly dominated strategies can result in the elimination of some of the equilibria of the original game
 