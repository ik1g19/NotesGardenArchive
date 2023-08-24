---
title: Extensions of Stable Matching Problem
---
# Classical Stable Matching Problem

## Participants
- A set of $n$ leaders
- A set of $n$ followers

## Preferences
- Each leader has **strict preferences** over all followers
- Each follower has **strict preferences** over all leaders

Every leader ranks all followers (i.e. finds them **acceptable**) and vice versa.

## Objective
Find a one-to-one **stable** matching
- (one-to-one) Matching: each leader is paired with at most one follower and vice versa
- Stable: no **blocking pair**
	- $(\boldsymbol{l}, \boldsymbol{f})$ is a blocking pair iff they both prefer each other to their assigned partners

# Concurrent Proposals

Gale-Shapley is **non-deterministic** - When choosing a free leader (who hasn’t proposed to every follower ) to propose, the algorithm can choose any such leader arbitrarily

We can consider a (parallelised) variant of GS in which all free leaders (who haven’t proposed to every follower ) propose at the **same time**
• If a follower receives several proposals, she compares them all with their current fiancé (if any), picks the one she most prefers and rejects the rest

# Extensions of Stable Matching Problem

## **S**table **M**atching with **I**ncomplete Lists

Agents may declare some candidates unacceptable
An agent prefers to remain unmatched than to get matched to an unaccpetable partner

**Matching** - an individually rational pairing of leaders and followers.  
1. Each leader is paired with at most one follower and vice versa.  
2. Each agent finds his/her partner acceptable.  
**Stable Matching** - a matching with no blocking pair

![|300](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230319185114.png)
>[!Tip]
>In this example, $f_1$ finds $l_1$ unacceptable

### Gale-Shapley for SMI
The same algorithm, but with changes in lines 2,4 and 12

```C
assign all leaders and followers to be free; //initial state  
while (some leader l is free and hasn’t proposed to every follower 𝗵𝗲 𝗳𝗶𝗻𝗱𝘀 𝗮𝗰𝗰𝗲𝗽𝘁𝗮𝗯𝗹𝗲)
	f = first follower on l's list to whom l hasn't yet proposed;  
	// next: l proposes to f  
	if (f is free and finds l 𝗮𝗰𝗰𝗲𝗽𝘁𝗮𝗯𝗹𝗲)
		assign l and f to be engaged; //tentatively matched  
	else if (f prefers l to her fiancé l') { //f is engaged  
		set l and f to be engaged;  
		set l' to be free;  
	else f rejects l; //and l remains free  
output the 𝗲𝗻𝗴𝗮𝗴𝗲𝗱 𝗽𝗮𝗶𝗿𝘀, who form a stable matching;
```

## **S**table **M**atching with **T**ies

Agents may be indifferent among several candidates

**Blocking Pair** - when ties are allowed, three different types of blocking pairs can be defined. The straightforward extension of the one you are already familiar with is the following:  
• There is no leader-follower pair, each of whom would **strictly** prefer to match with each other rather than their assigned partner

**Stable Matching** - A matching with no blocking pair

![|300](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230319185348.png)
>[!Tip]
>In this example, $f_1$ is indifferent between $l_2$ and $l_1$ and $l_2$ is indifferent between $f_2$ and $f_1$

## **S**table **M**atching with **T**ies and **I**ncomplete Lists

Both incomplete lists and indifferences are allowed

Same Gale-Shapley algorithm for SMI works for SMTI
- **Only change** - Break ties in preferences arbitrarily first

# Optimal Stable Matchings

## Achievable Candidates

For a given instance, there may be several stable matchings

![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313201143.png)
This instance has two stable matchings - <strong><font color="00b050">Green</font></strong> and <strong><font color="800080">Purple</font></strong>
- Both $f_1$ and $f_2$ are achievable to $l_1$
- Only $l_3$ is achievable to $f_3$

>[!Definition]
>A leader $l$ and a follower $f$ are **achievable** to each other if there exists a stable matching in which $l$ and $f$ are matched

## Leader-Optimal Matching

**Leader-optimal matching** - a stable matching in which each leader receives his best achievable partner.  
**Follower-optimal matching** - a stable matching in which each follower receives her best achievable partner

**Claim** - When preferences are strict, all executions of leader-oriented GS return the leader-optimal matching
<strong><font color="00b050">Proof</font></strong> (By Contradiction):
- Suppose a leader is matched with a follower other than best achievable partner
- Leaders propose in decreasing order of preferences
	$\Rightarrow$ some leader is rejected by an achievable partner during GS
- Let $l$ be first such leader and let $f$ be the first (and hence best) achievable partner that rejects $l$
- Let $\boldsymbol{\mu}$ be a stable matching where $\boldsymbol{l}$ and $f$ are matched.
- When $f$ rejects $l$ in GS, she forms (or re-affirms) commitment to a leader, say $l^{\prime} \Rightarrow$ f prefers $l^{\prime}$ to $l$
- Let $f^{\prime}$ be the partner of $l^{\prime}$ in $\boldsymbol{\mu}$
- $l^{\prime}$ had not been rejected by any achievable partner (including $f^{\prime}$ ) at the point when $l$ is rejected by $f$
	- Because this is the first rejection by an achievable partner
- Thus, $l^{\prime}$ had not yet proposed to $f^{\prime}$ when $l^{\prime}$ proposed to $\mathrm{f} \Rightarrow l^{\prime}$ prefers $\mathrm{f}$ to $f^{\prime}$ 
- Thus $\left(l^{\prime}, \mathrm{f}\right)$ is a blocking pair in $\boldsymbol{\mu}$, a contradiction (to $\mu$ being stable)

**Corollary 1** - When preferences are strict, all executions of leader-oriented Gale -Shapley return the same stable matching
**Corollary 2** - When preferences are strict, there exists a leader-optimal stable matching and a follower-optimal stable matching

### Conflict of Interests
**Leader-pessimal matching** - a stable matching in which each  
leader receives his **worst achievable** partner
**Follower-pessimal matching** - a stable matching in which each  
follower receives her **worst achievable** partner

>[!Theorem]
>When preferences are strict, the leader-optimal matching is the follower-pessimal matching, and vice versa

### The Case with Ties
**Claim** - When **ties** are allowed, a **leader-optimal** stable matching and/or a **follower-optimal** stable matching **may not exist**

![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313203519.png)
This example has two stable matchings - <strong><font color="00b050">Green</font></strong> and <strong><font color="800080">Purple</font></strong> 
• Neither is a leader-optimal stable matching - $l_2$ prefers <strong><font color="800080">Purple</font></strong> but $l_3$  
prefers <strong><font color="00b050">Green</font></strong>
• Neither is a follower-optimal stable matching - $f_1$ and $f_2$ prefer <strong><font color="00b050">Green</font></strong> but $f_3$ prefers <strong><font color="800080">Purple</font></strong>

# Dominant Strategy Truthfulness

Agents (leaders and followers) declare their preferences to the centralised system  
• Agent are strategic - they misreport if it is in their benefit  
- i.e. if providing a different ranking over candidates results in the system matching them with a better one

A matching mechanism is **dominant-strategy truthful** (DS truthful), if every agent finds it in his/her best interest to declare his/her true preference list, no matter what other agents choose to do

## Is Gale-Shapley Dominant Strategy Truthful

Assume that **preferences are strict**

When the leader-oriented version of Gale-Shapley algorithm is executed, all **leaders** find it in their best interest to be **truthful**
Some followers, however, may benefit from **misreporting** their preferences

![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313204939.png)

![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313205041.png)

## Dominant Strategy Truthfulness

>[!Theorem]
>**Dubins and Freedleader**
>The mechanism that **yields the leader-optimal** stable matching (in terms of stated preferences) makes it a **dominant strategy for each leader** to state his **true** preferences

Similarly, the mechanism that yields the follower-optimal stable matching makes it a dominant strategy for every follower to state her true preferences
If we have ties in preferences but a leader-optimal stable matching exists, then leader-oriented GS is DS truthful for leaders

## Impossibility of Dominant Strategy Truthfulness

>[!Theorem]
>**Roth**
>No stable matching mechanism exists for which truth-telling is a dominant strategy for every agent, **even when preferences are strict**

### Proof of the Impossibility Result
#### Proof Sketch
1. Construct an instance of SMI
2. Show that whatever stable matching the mechanism chooses, at least one agent can benefit by misreporting (i.e. if that agent declares a different preference, the mechanism matches the agent with a better partner)

#### Proof
Consider the following instance with 2 leaders and 2 followers
![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230313205826.png)

1. This instance has two stable matchings - <strong><font color="00b050">Green</font></strong> and <strong><font color="800080">Purple</font></strong>  
2. Every stable matching mechanism must choose either <strong><font color="00b050">Green</font></strong> or <strong><font color="800080">Purple</font></strong>  
3. Suppose the mechanism chooses the <strong><font color="00b050">Green</font></strong> matching
4. If f 2 now only declares l 1 as acceptable then the only stable matching is the <strong><font color="800080">Purple</font></strong> matching.  
5. Similarly, if the mechanism chooses the purple matching, then if l 2 declares only f 2 as acceptable then only the <strong><font color="00b050">Green</font></strong> matching is stable
6. In either scenario, at least one agent benefits by not reporting truthfully

#### Observation
In the proof of the impossibility result, we allowed incomplete  
lists and agents could report by "**truncating**" their preferences  
and by falsely declaring an acceptable partner as unacceptable

## Impossibility of Truthful Nash Equilibrium

**Roth Corollary** - No stable matching mechanism exists for which stating the true preferences is always a best response for every agent when all other agents state their true preferences

**Alternative Statement for Corollary** - **No stable matching mechanism** exists for which it is always an **equilibrium** for every agent to state his or her **true preferences**

## Few People Can Manipulate

>[!Theorem]
>The number of students that have more than one achievable hospital vanishes. Therefore, with high probability, the truthful strategy is a dominant strategy

**Approximate Truthfulness** - The incentive to manipulate is smaller than epsilon