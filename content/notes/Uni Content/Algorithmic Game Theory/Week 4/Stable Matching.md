---
title: Stable Matching
---
Leaders can only lead and followers can only follow

# Setting

## Participants

- A set of leaders $L=\{\mathbf{1}, \ldots, \boldsymbol{n}\}$
- A set of followers $\boldsymbol{F}=\{\mathbf{1}, \ldots, \boldsymbol{n}\}$

## Preferences
- Each leader has strict preferences over all followers
- Each follower has strict preferences over all leaders
All preferences together: **preference profile**

## Objective
- To find a one-to-one stable matching
- (one-to-one) Matching: each leader is paired with at most one follower and vice versa
- Stable: no pair $(\boldsymbol{l}, f)$ wants to deviate

# Stable Matching

![|200](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313184718.png)![|200](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313184737.png)

A matching is **stable** if
- There is no leader-follower pair, each of whom would prefer to match with each other rather than their assigned partner
In the latter case, this is called a **blocking pair**
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313185154.png)

>[!Tip]
>In this example this is a blocking pair as light blue would prefer to be matched with pink and pink would prefer to be matched with light blue

## Gale & Shapley Algorithm

>[!Theorem]
>**Gale & Shapley**
>A stable matching **always** exists, and can be found in polynomial time

### Leader Oriented

```C
Assign all leaders and followers to be free; //initial state  
while (some leader l is free and hasn’t proposed to every follower)  
	f = first follower on l's list to whom l hasn't yet proposed;  
	// next: l proposes to f  
	if (f is free)  
		assign l and f to be engaged; //tentatively matched  
	else if (f prefers l to her fiancé l') { //f is engaged  
		set l and f to be engaged;  
		set l' to be free;  
	else f rejects l; //and l remains free  
output the n engaged pairs, who form a stable matching;
```

![|600](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/stable%20matching.gif)

### Proof of Correctness
**Claim** - Gale-Shapley algorithm always terminates and returns a stable matching

In order to prove this we need to show that:  
1. The algorithm always terminates
2. The algorithm returns a matching (every leader is  
matched with at most one follower and vice versa)
3. The matching it returns is stable (no blocking pair)

#### Termination
**Observation 1.** Leaders propose to followers in decreasing  
order of preference  
**Observation 2.** Once a follower is matched up, s/he never  
becomes unmatched; only "trades up"

**Claim** - Algorithm terminates after at most $n^2$ iterations of  
While loop
<strong><font color="00b050">Proof</font></strong> - Each time through the while loop, a leader proposes to a new follower. Thus there are at most $n^2$ possible proposals

#### Matching
**Claim** - Gale-Shapley outputs a matching
<strong><font color="00b050">Proof</font></strong>:
- Leader proposes only if unmatched $\Rightarrow$ matched to $\leq 1$ follower
- Follower keeps only best leader $\Rightarrow$ matched to $\leq 1$ leader

#### The Matching is Perfect (Everyone is Matched)
**Claim** - In Gale-Shapley matching, all leaders get matched
<strong><font color="00b050">Proof</font></strong> (By Contradiction):
- Suppose, for a contradiction, that some leader $l$ is unmatched when Gale-Shapley terminates.
- Then some follower, say $f$, is unmatched upon termination.
- By Observation 2, $f$ was never proposed to.
- But, $l$ proposes to every follower, since $l$ ends up unmatched
- A contradiction!

**Claim** - In Gale-Shapley matching, all followers get matched
<strong><font color="00b050">Proof</font></strong> (By Counting) - By previous claim, all $n$ leaders get  
matched. Thus all $n$ followers get matched

#### Stability
**Claim** - In Gale-Shapley matching $\mu$, there are no blocking pairs
<strong><font color="00b050">Proof</font></strong>:
- Consider any pair $(\boldsymbol{l}, \boldsymbol{f})$ that is not in $\boldsymbol{\mu}$
- **Case 1**: $l$ never proposed to $f$
	$\Rightarrow \boldsymbol{l}$ prefers $\boldsymbol{\mu}(\boldsymbol{l})$ to $\boldsymbol{f}$. (since leaders propose in decreasing order of preferences
		$\mu(l)$ - Partner of $l$ in $\mu$
	$\Rightarrow(l, f)$ is not blocking
- **Case 2**: $l$ proposed to $f$
	$\Rightarrow f$ rejected $l$ (either right away or later)
	$\Rightarrow \boldsymbol{f}$ prefers $\boldsymbol{\mu}(\boldsymbol{f})$ to $\boldsymbol{l}$ (as followers only trade up)
		$\mu(f)$ - Partner of $f$ in $\mu$
	$\Rightarrow(l, f)$ is not blocking
- In either case, the pair $(l, f)$ is **not a blocking pair**

