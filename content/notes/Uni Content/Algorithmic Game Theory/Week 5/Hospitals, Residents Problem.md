---
title: Hospitals, Residents Problem
---
# **H**ospitals/**R**esidents Problem and **H**ospitals/**R**esidents with **T**ies

- Agents on one side can get matched to several candidates
- Many-one stable matching problem

Working in practise:
- Junior doctors (or residents) must undergo training in hospitals  
- Applicants rank hospitals in order of preference  
- Hospitals do likewise with their applicants  
- Centralised matching schemes (clearinghouses) produce a matching in several countries

## **H**ospitals/**R**esidents Problem

Participants
- A set of $n_1$ residents $\left\{r_1, r_2, \ldots, r_{n_1}\right\}$
- A set of $n_2$ hospitals $\left\{h_1, h_2, \ldots, h_{n_2}\right\}$

Each hospital has a **capacity**

Preferences:
- Residents rank **acceptable** hospitals in strict order of preference, hospitals do likewise
- We assume that unacceptability is **mutual**: if $h$ finds $r$ unacceptable then $r$ finds $h$ unacceptable and vice versa

### Matching in **HR**
A matching $M$ is a set of resident-hospital pairs such that:
- $(r, h) \in M \Rightarrow r, h$ find each other acceptable
- No resident appears in more than one pair
- No hospital appears in more pairs than its capacity

#### Example Matching
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314161213.png)

### Stability
Matching $M$ is stable if $M$ admits no blocking pair

$(r, h)$ is a blocking pair of matching $M$ if:
1. $r, h$ find each other acceptable and
2. either $r$ is unmatched in $M$ or $r$ prefers $h$ to his/her assigned hospital in $M$ and
3. either $h$ is undersubscribed in $M$ or $h$ prefers $r$ to its worst resident assigned in $M$

A matching $M$ is a set of resident-hospital pairs such that:
- $(r, h) \in M \Rightarrow r, h$ find each other acceptable
- No resident appears in more than one pair
- No hospital appears in more pairs than its capacity

Matching $M$ is stable if $M$ admits no blocking pair 
$(r, h)$ is a blocking pair of matching $M$ if:
1. $r, h$ find each other acceptable and
2. either $r$ is unmatched in $M$ or $r$ prefers $h$ to his/her assigned hospital in $M$ and
3. either $h$ is undersubscribed in $M$ or $h$ prefers $r$ to its worst resident assigned in $M$

#### Examples
##### Blocking Pair 1
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314161427.png)

##### Blocking Pair 2
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314161444.png)

##### Blocking Pair 3
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314161503.png)

##### Stable Matching
![|500](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314161524.png)



### **R**esident-Oriented **G**ale **S**hapley
Extension of Gale-Shapley to HR
```C
M = ∅; //assign all residents and hospitals to be free  
while (some resident rᵢ is unmatched and has a non-empty list)  
	rᵢ applies to the first hospital hⱼ on her list;  
	M = M ∪ {(rᵢ , hⱼ )};  
	if (hⱼ is over-subscribed)  
		rₖ = worst resident assigned to hⱼ ;  
		M = M ∖ {(rₖ, hⱼ )}; //rₖ is set free  
	if (hⱼ is full)  
		rₖ = worst resident assigned to hⱼ ;  
		for (each successor rₗ of rₖ on hⱼ’s list)  
			delete rₗ from hⱼ’s list;  
			delete hⱼ from rₗ’s list;  
output the engaged pairs, who form a stable matching;
```

#### Example
![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314162451.png)
![|450](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314162507.png)

### Optimal Stable Matchings
Extension of results for SMI

**Claim** - When preferences are strict, all executions of **resident**-oriented GS (RGS) return the resident-optimal (stable) matching

**Claim** - When preferences are strict, all executions of **hospital**-oriented GS (HGS) return the hospital-optimal (stable) matching

**Claim** - When preferences are strict, the hospital-optimal matching is the **resident-pessimal** matching, and vice versa

### **H**ospital-Oriented **G**ale **S**hapley
```C
M = ∅; //assign all residents and hospitals to be free  
while (some hospital hᵢ is undersubscribed and has non-empty list)  
	sᵢ = qᵢ - |M(hᵢ)|; //the number of available seats in hᵢ
	hᵢ applies to the first sᵢ residents on its list;  
	foreach (rⱼ that hᵢ applies to)  
		if (rⱼ is free) M = M ∪ {(rⱼ , hᵢ )};  
		else if (rⱼ prefers hᵢ to her current hospital h’)  
			M = M ∪ {(rⱼ , hᵢ )} \ {(rⱼ , h’)}; //h’ is set free  
		for (each successor hₗ of M(rⱼ ) on rⱼ’s list)  
			delete hₗ from rⱼ’s list;  
			delete rⱼ from hₗ’s list;  
output the engaged pairs, who form a stable matching;
```

#### Example
![|400](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314163607.png)

![|450](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314163625.png)

### Hospital-Optimal vs. Resident-Optimal
![|450](notes/Uni%20Content/Algorithmic%20Game%20Theory/Images/Pasted%20image%2020230314165052.png)

### Rural Hospitals Theorem
>[!Theorem]
>In a given instance of HR:  
>1. the **same residents** are assigned in all stable matchings;  
>2. each hospital is assigned the **same number of residents** in all stable matchings;  
>3. any hospital that is **undersubscribed** in one stable matching is assigned **exactly the same set of residents** in all stable matchings

### Dominant Strategy Truthfulness
>[!Theorem]
>A stable matching mechanism that yields the **resident-optimal** matching makes it a **dominant strategy for all residents** to state their true preferences
>- Under strict preferences, RGS is dominant-strategy truthful for residents

>[!Theorem]
>**No stable matching mechanism exists** that makes it a dominant strategy for **all hospitals** to state their true preferences.  
>- Even when hospital-oriented GS (HGS) is executed and preferences are strict, some hospitals may benefit from misreporting their preferences

## **H**ospitals/**R**esidents problem with **T**ies

Resident's preference lists are short
Hospital's lists are generally long, so ties may be used

A hospital may be **indifferent** among several residents

An instance of HRT may not admit a hospital-optimal and/or a resident-optimal matching
A matching $M$ is stable in an HRT instance $I$ if and only if $M$ is stable in some instance $I$ ' of HR obtained from $I$ by breaking the ties

## **H**ospitals/**R**esidents problem with **C**ouples

Pairs of residents who wish to be matched to geographically close hospitals form couples
Each couple $\left(r_i, r_j\right)$ ranks in order of preference a set of pairs of hospitals $\left(h_p, \boldsymbol{h}_q\right)$ representing the assignment of $r_i$ to $h_p$ and $r_j$ to $h_q$

A stable matching need not exist
Stable matchings can have different sizes

The problem of determining whether a stable matching exists in a given HRC instance is NP-complete, even if each hospital has capacity 1 and:  
- there are no single residents  

- there are no single residents, and  
- each couple has a preference list of length ≤2, and  
- each hospital has a preference list of length ≤3  

- the preference list of each single resident, couple and hospital is derived from a strictly ordered master list of hospitals, pairs of hospitals and residents respectively , and  
- each preference list is of length ≤3, and  
- the instance forms a “dual market”

