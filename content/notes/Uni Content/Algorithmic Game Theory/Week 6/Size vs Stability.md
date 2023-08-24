# Maximum Size Stable Matching

## Stable Matchings of Different Sizes

All stable matchings in a given instance of SM, or SMT, or SMI, are of the same size.

When both ties and incomplete lists are allowed (i.e. we have an instance of SMTI), stable matchings can have different sizes

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515153652.png|400]]

A maximum (cardinality) stable matching can be (at most) twice the size of a minimum stable matching

## Maximum Stable Matchings

Problem of finding a maximum stable matching in an instance of SMTI (MAX SMTI) is NP-hard, even if (simultaneously):
- the ties occur on one side only
- each preference list is either strictly ordered or is a single tie
- and
- either each tie is of length 2
- or each preference list is of length $\leq 3$ 

This result implies that MAX HRT is also NP-hard

Minimisation problem is NP-hard too, for similar restrictions

## Reminder: Computational Complexity

- Given two functions $f$ and $g$, we say $f(n)=\mathrm{O}(g(n))$ if there are positive constants $c$ and $N$ such that $f(n) \leq c$.g $(n)$ for all $n \geq N$
- An algorithm for a problem has time complexity $O(g(n))$ if its running time $f$ satisfies $f(n)=\mathrm{O}(g(n))$ where $n$ is the input size
- An algorithm runs in polynomial time if its time complexity is $\mathrm{O}\left(n^k\right)$ for some constant $k$, where $n$ is the input size
- A decision problem is a problem whose solution is yes or no for any input
- A decision problem belongs to the class $\mathbf{P}$ if it can be solved by a polynomialtime algorithm
- A decision problem belongs to the class NP if it can be verified in polynomial time
- A decision problem $\boldsymbol{A}$ is NP-hard if every other problem in NP reduces to $\boldsymbol{A}$.
- A decision problem $A$ is NP-complete if it NP-hard and it belongs to NP.
- If a decision problem is NP-complete it has no polynomial-time algorithm unless $\mathbf{P}=\mathbf{N P}$

## Reminder: Approximation Algorithms

- An optimisation problem is a problem that involves maximising or minimising (subject to a suitable measure) over a set of feasible solutions for a given instance
- e.g., colour a graph using as few colours as possible
- If an optimisation problem is NP-hard it has no polynomial-time algorithm unless $\mathbf{P}=\mathbf{N P}$
- An approximation algorithm $A$ for an optimisation problem is a polynomialtime algorithm that produces a feasible solution $A(I)$ for any instance $I$.
- $A$ has performance guarantee $c$, for some $c>1$ if
- $|A(I)| \leq c$.opt(I) for any instance $I$ (in the case of a minimisation problem)
- $|A(I)| \geq(1 / c)$. opt $(I)$ for any instance $I$ (in the case of a maximisation problem)
where opt(I) is the measure of an optimal solution and $|A(I)|$ the size of the solution produced by $A$.
We say that $A$ is a c-approximation algorithm for this problem.

## Kiraly's $\frac{3}{2}$ - approximation for MAX SMTI

### Leader Oriented Version
Extension of Gale-Shapely

When a leader is rejected by all followers in his list, he is given a second chance

#### Preferences
For a leader $l$, and for two followers $f_i$ and $f_j$, we say that $l$ prefers $f_i$ to $f_j$ if
1. either he prefers $f_i$ in the usual sense
2. or he is indifferent between the two, $f_j$ is engaged and $f_i$ is free.

For a follower $\mathrm{f}$, and for two leaders $l_{\mathrm{i}}$ and $l_{\mathrm{j}}$, we say that $\mathrm{f}$ prefers $l_{\mathrm{i}}$ to $l_{\mathrm{j}}$ if 1. either she prefers $l_{\mathrm{i}}$ in the usual sense
2. or she is indifferent between the two, $l_{\mathrm{i}}$ has a second chance (he is proposing to the followers in his list for the $2^{\text {nd }}$ time) and $l_j$ does not (he is proposing to the followers in his list for the $1^{\text {st }}$ time)

#### Proposals and rejections
An assigned follower $f$ accepts a new proposal from a leader $l$, and rejects her current partner $l_{\mathrm{k}}$, if
1. either she prefers $l$ to her current partner, according to her new definition of prefers
2. or her current partner prefers some follower to $f$, again according to his new definition of prefers. (In this case we call $\mathrm{f}$ precarious.)

When a follower $f$ rejects a leader $l$, and she is not precarious, $l$ and $f$ are deleted from each others' lists

### Dominant-Strategy Truthfulness
Is Kiraly's algorithm DS truthful?
- No. (Recall Roth's impossibility theorem)

Is the leader-oriented Kiraly DS truthful for leaders?
- No. (Exercise: prove this; a simple example works)

If not, can we achieve $3 / 2$ approximation ratio with another mechanism that is DS for leaders?
- No

If not, can we achieve $3 / 2$ approximation ratio with another mechanism that is DS for leaders and ties are only on one side of the market?
- No if ties are on followers' side.
- Yes if ties are on leaders' side

# 'Almost Stable' Matchings

Sometimes matching more people is very import

A small number of blockings pairs could be tolerated if it is possible to find a larger matching

MAX SIZE MIN BP SMI is the problem of finding a matching, out of all maximum cardinality matchings, which has the minimum number of blocking pairs, given an instance of SMI.

- is NP-hard even if every preference list is of length $\leq 3$
- not approximable within $n^{1-\varepsilon}$, for any $\varepsilon>0$, unless $P=N P$
- Solvable in polynomial time if each follower's list is of length $\leq \mathbf{2}$