---
title: "Extensive-Form Games"
---

In strategic form games, players make a move simultaneously
In extensive form games players make choices sequentially
Extensive form games model different kinds of strategic sequential decision making
- Games with perfect information - Players know exactly how the current state of the game was reached
- Games with imperfect information - Players may be uncertain about previous moves, may not know how the current state was reached
- Games of perfect recall - No player forgets the action they previously chose
# Ultimatum Game

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107154631.png]]

Two agents want to share a cake
1. First player suggests a split
2. $P2$ can either accept the proposed split or reject it
Game is represented as a tree
A choice is made by one of the players are each non-terminal node
Every edge represents a possible action
Leaves represent the final outcome
# Extensive Form Games
> [!Definition]
> A finite extensive-form game with perfect information is a tuple $$G=(N,A,H,Z,\alpha,\pi,\sigma,u)$$ where
> - $N$ is a finite set of players
> - $A$ is a single set of actions
> - $H$ is a set of nonterminal choice nodes
> - $Z$ is a set of terminal nodes, disjoint from $H$
> - $\alpha : H \rightarrow 2^A$ is the action function, which assigns to each choice node a set of possible actions
> - $\pi : H \rightarrow N$ is the player function, which assigns to each nonterminal node a player $i \in N$ who chooses an action at that node
> - $\sigma : H \times A \rightarrow H \cup Z$ is the successor function, which maps a choice node and an action to a new choice node or terminal node such that for all $h_1,h_2\in H$ and $a_1,a_2\in A$, if $\sigma (h_1,a_1)=\sigma (h_2,a_2)$, then $h_1=h_2$ and $a_1=a_2$
> - $u = (u_1,...,u_n)$, where $u_i : Z \rightarrow \mathbb{R}$ is a real valued utility function for player $i$ on the terminal nodes $Z$

#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107164833.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107165127.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107165331.png]]
## Strategies
A strategy for player $i$ in an extensive-form game is a complete specification of the action taken at every note belonging to the player
An agents strategy requires a decision at each choice node, regardless of whether or not it is possible to reach that node given the other choice nodes
> [!Definition]
> Let $G$ be a perfect-information extensive-form game. The pure strategies of player $i$ consist of the cartesian product $$\prod\limits_{h\in H, \pi (h)=i}\alpha(h)$$

#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107170609.png]]
# Strategic Form Transformation
We can assign a utility value for each player
We then convert the extensive-form game into a strategic-form game

It is always possible to transform an extensive-form game into a strategic form game
The transformation negates the temporal nature of the game
Redundant elements are also added

It is not always possible to transform a strategic form game into an extensive form game

#### Example

![[notes/Uni Content/Intelligent Agents/Images/exten to strat.gif]]

>[!Tip]
>You compute the set of pure strategies by taking the cross product of the Players actions
>To convert to a strategic form game, you write out the grid and then work out what you would end up with if you were to follow the corresponding actions at that tile


# Equilibria
Once an extensive form game is transformed to a strategic form game, we can compute the pure strategy Nash equilibria
The existence of pure Nash equilibria is always guaranteed in extensive form games
> [!Theorem (Zermelo)]
> Given any finite perfect-information extensive form game $G$, let $G*$ be its strategic form. Then $G*$ has a pure strategy Nash equilibrium

>[!Tip]
>Pure strategy Nash equilibria are found the same way in a converted strategic form as you would find them in a normal one

## Subgames
Some equilibria are unsatisfying (the choices do not match what we would expect rational players to make)
Subgame perfect equilibrium captures why equilibria can be unsatisfying
> [!Definition (Subgame)]
> Given a perfect information extensive form game $G$, the subgame of $G$ rooted a node $h$ is the restriction of $G$ to the descendants of $h$
> The set of subgames of $G$ consist of all subgames rooted at some node in $G$

To find the subgames of an extensive form game, we look at each nonterminal node of the game and take the tree originating from the node

![[notes/Uni Content/Intelligent Agents/Images/subtrees.gif]]
### Subgame Perfect Equilibria
>[!Definition]
>A strategy profile $s$ in an extensive form game $G$ is a **subgame perfect equilibrium** if, for each subgame $G'$ of $G$, the restriction of $s$ to $G'$ is a pure strategy Nash equilibrium

>[!Theorem]
>Every extensive form game has a subgame perfect equilibrium

>[!Theorem]
>For every extensive form game the set of subgame perfect equilibria is a subset of the set of pure strategy Nash equilibria

#### Example

![[content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107181717.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107181821.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107181848.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107181917.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221107182003.png]]
# Backward Induction
Backwards induction algorithm to reach the concept of a subgame perfect equilibrium

1. Take the tree representing an extensive form game with $n$ players
2. Starting from the smallest subgames (i.e. those rooted at nodes whose children are terminal nodes), compute the Nash equilibrium for the player making the choice
3. Replace the subgame with utility $u$ obtained (i.e. make the node of the subgame a terminal node and label it with the utility of the equilibrium)
4. Repeat the process for every subgame rooted in a node leading to terminal nodes (i.e. compute the Nash equilibirum and replace the game with the result of its equilibrium)
5. If at any step a subgame has multiple Nash equilibria (i.e. when the utilities of  different choices are the same), select any of them
6. Terminate when we reach the root node of the whole game

The algorithm runs in polynomial time in the size of the tree
For every player $i$, let $s_i$ be the vector where each component is the choice made by the player in the process of selecting the equilibrium of a subgame
$(s_1,...,s_n)$ is a subgame perfect equilibrium and the utility $u$ at the root node is the value of the equilibrium

![[notes/Uni Content/Intelligent Agents/Images/subgame_perfect.gif]]
#### Example

![[notes/Uni Content/Intelligent Agents/Images/subgame_perfect_example.gif]]
# Ultimatum Game (General Version)
1. Player 1 can propose a division of the cake in $n$ parts, for any natural number $n > 1$
2. Player 2 can either accept the subdivision or reject it, in that case, nobody gets anything
3. For any game of this kind, no matter what $n$ we choose, there are always exactly two subgame perfect equilibria

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221113204129.png]]
In the first equilibrium, $P2$ chooses yes at every node, and so $P1$ choose $\frac{n}{0}$

In the second equilibrium, $P2$ chooses yes at every node except at the left most node - so $P1$ chooses $n-\frac{1}{1}$

While there are only two subgame perfect equilibria, there are many more Nash equiibria
Any strategy combination $$(\frac{n}{0},(yes,x_1,...,x_n))$$ where each $x_i\in\{no,yes\}$ is a choice by player 2, is a Nash equilibrium
$P1$ gets the best possible payoff by choosing $\frac{n}{0}$
When $P1$ chooses $\frac{n}{0}$, the payoff for player 2 will be the same no matter what choice is made
# Centipede Game

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221113204812.png]]

Two player game with 100 stages
In odd stages ($t=1,3,...,99$) player 1 can either
- Stop the game $S$ with payoff of $(t,t-1)$
- Continue the game $C$
In even stages ($t=2,4,...,100$) player 2 can either
- Stop the game $S$ with payoff of $(t-2,t+1)$
- Continute the game $C$
The game ends after 100 stages if no player decides to stop before

Backward induction shows that players choose to stop the game at every stage
This is the only subgame perfect equilibrium
At this equilibrium, player 1 stops the game at the first stage and the payoff is $(1,0)$
No player will be satisfied with this outcome and they can do much better by continuing the game