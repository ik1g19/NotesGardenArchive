---
title: Stable Roommates
---
Find your roommate
Each student has a strict preferemce list
Same notion of stability as stable marriage
No longer a bipartite graph
Stable matching (stable marriage) is a special case

# **S**table **R**oommates Problem

**Participants**
- $2 n$ students or agents

**Preferences**
- Each agent has strict preferences over all other (2n-1) agents

**Matching**
- A set of $\mathrm{n}$ disjoint pairs of agents

**Stable Matching**
- A matching $M$ with no blocking pair
- That is, no $\{p, q\} \notin M$ such that $p$ prefers $q$ to her partner in $\mathbf{M}$, and $\mathbf{q}$ prefers $p$ to her partner in $\mathbf{M}$

A stable matching does not always exist

#### Example

![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314175655.png)

## Irving's Algorithm for SR

Given an instance of SR, decides whether a stable matching exists
And if so, finds one

Runs in $O(n^2)$ time
Works in two phases:
- **Phase 1** - Similar to Gale-Shapley algorithms for the Stable Matching problem
- **Phase 2** - Elimination of "rotations"

### Semiengagement
Engagement is not a symmetric relation (unlike in SM)
- If $x$ is engaged to $y$, it is not necessarily the case that $y$ is engaged to $x$
- So we use the term semiengage and say that " $\mathrm{x}$ is semiengaged to $\mathrm{y}^{\prime \prime}$
- y could be free, semiengaged to another agent $z$, or semiengaged to $x$

All agents **start out free**
A semiengaged agent $\mathbf{x}$ becomes **free** when her semi-fiancé rejects $\mathrm{x}$

$\mathbf{x}$ becomes semiengaged when she **proposes** to someone
- The algorithm is designed so that when $\mathrm{x}$ proposes to $\mathrm{y}$ it must be the case that $y$ is either free or finds $x$ preferable to the current proposal she is holding

### Phase 1
Similar to Gale-Shapley

```C
Assign all agents to be free; //initial state  
while (some free agent x has a nonempty list)  
	y = first agent on x's list  
	// next: x proposes to y  
	if (some person z is semiengaged to y)  
		assign z to be free; // y rejects z  
	Assign x to be semiengaged to y;  
	for (each successor w of x on y’s list)  
		delete w from y’s list;  
		delete y from w’s list;
```

After Phase 1, there are two possibilities:
1. Exist an agent who got rejected by everyone else
	- No stable matching
2. Every agent holds a proposal. In other words, each row should have one top bar and one bottom bar (could coincide)
	1. If every row has only one remaining entry (top bar and bottom bar coincide) then we have a unique stable matching
	2. -> **Phase 2**

#### Example
![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314181447.png)
![|300](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314181527.png)

### Phase 2
The reduced preference list from the end of phase 1 is referred to as **phase-1 table**

The preference table is further reduced until
- **All lists contain just one entry**, in which case it constitutes a stable matching, or
- Until **some list becomes empty**, in which case no stable matching exists

Reduction of preference table takes place by eliminating "exposed rotations"

High level intuition is:
- If the original preference table admits a stable matching, so does all subsequent reduced tables
- If a reduced table doesn't admit a stable matching, neither does the original preference table

Phase 1 always returns the same preference table
Depending on the order of elimination in phase 2, we may arrive at different stable matchings
So **not all executions of Irving's algorithm return the same matching**

#### Exposed Rotation
A pair of sequences $\rho=\left(\left(p_0, \ldots, p_{r-1}\right),\left(q_0, \ldots, q_{r-1}\right)\right)$ constitute an **exposed rotation** if
- $q_i$ is the second entry on $p_i^{\prime}$ s list, and
- $p_{i+1}$ is the last entry on $q_i^{\prime}$ s list
	- $i+1$ is taken modulo $r$

Exposed rotation $\rho=\left(\left(p_0, \ldots, p_{r-1}\right),\left(q_0, \ldots, q_{r-1}\right)\right)$ is eliminated by deleting $\left(q_i, p_{i+1}\right)$ from each other's lists, for all $\mathrm{i}$
- delete $\mathrm{q}_{\mathrm{i}}$ from $\mathrm{p}_{\mathrm{i}+1}$ 's list
- delete $\mathbf{p}_{i+1}$ from $q_i$ 's list

#### Algorithm
```C
T = phase-1 table; //initial state  
while ((some list in T has more than one entry) and (no list in T is empty))  
	find a rotation 𝝆 exposed in T  
	T = T / 𝝆 // eliminate 𝜌  
if (some list in T is empty)  
	return instance unsolvable;  
else  
	return T, which is a stable matching;
```

#### Example
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/stable%20roommates.gif)

# Extensions of **S**table **R**oommates

## Odd Number of Agents

There may be an odd number of agents
In any matching one agent is unmatched

Stability defined as before
An agent prefers being matched than to remain unmatched

### Extending Irving's Algorithm
If after phase 1 all preference lists are nonempty, then there exists no stable matching
If at the end of phase 1, exactly one agent's $x$ preference list becomes empty
- $x$ cannot be matched in any stable matching
- If there exists a stable matching, no other person is unmatched
- To check whether or not there exists a stable matching, we run phase 2 (without $x$)

## Unacceptable Partners

Some agents may find other agents unacceptable
In this case we get Stable Roommates with Incomplete Lists (SRI)

An agent prefers being matched to an acceptable partner than to remain unmatched

### Extending Irving's Algorithm
After phase 1, one or more preference lists may become empty
- Any agent with an empty list cannot be matched in any stable matching
- Any person with a nonempty list must be matched in every stable matching
- To check whether or not there exists a stable matching, we run phase 2 without those agents whose lists are empty at the end of phase 1

### Stable Pairs
Any pair $(x,y)$ removed during phase 1 cannot be a stable pair
- i.e. $x$ and $y$ are not matched in any of the stable matchings

For each agent, the **first entry** in the phase-1 table is their **best achievable roommate** (if there is any achievable roommate)
For each agent, the **last entry** in the phase-1 table is their **worst achievable roommate** (if there is any achievable roommate)

## Ties

Some agents might be indifferent between several other agents
In which case we get Stable Roommates with Ties (SRT)

As in SMT, different types of blocking pairs can be defined for SRT. Here we will focus on the straightforward extension of the stability notion we already know  
- A matching is stable if there is **no pair** such that each of whom would **strictly prefer to match with each other** rather than their assigned partner

>[!Theorem]
>Deciding whether a stable matching exists, given an instance of SRT, is **NP-complete**

Even if each preference list is either strictly ordered or contains a tie of length 2 at the head