---
title: "Preference Elicitation"
---

# Preference Orderings
For finite outcome set $O$
$y\succeq z$ means $y$ is weakly prefered to $z$
$y\succ z$ means $y$ is strictly prefered to $z$
- It is true iff $y\succeq z$ and $z\cancel{\succeq}y$
$y\sim z$ means indifferent between $y$ and $z$
- It is true iff $y\succeq z$ and $z \succeq y$

### Conditions
#### Reflexive
$x\succeq x$ for all $x\in O$
#### transitive
For all $x,y,z\in O$, if $x\succeq y$ and $y\succeq z$ then $x\succeq z$
#### total/connected
$y\succeq z$ or $z\succeq y$ for all $y,z\in O$

$\succeq$ that satisfies the above conditions is called a total preorder

### Equivalence Classes
A **tie** or **equivalence class** consists of outcomes that we are indifferent between

# Preference Uncertainty
Learning our preferences is costly
Often there are too many outcomes and ranking them is too costly
Instead we partially learn our preferences

# Preference Elicitation
We start with partial (or no) information about our preferences
We learn more about preferences by making queries

**Pairwise Queries** - Compare two given outcomes
**Interviews** - Learn as much as possible about the value of an outcome

## Pairwise Queries
Two given outcomes $x$ and $y$ are compared against each other and the result is one of the following
- $x \succ y$ 
- $y\succ x$
- $x\sim y$

## Interviews
A given outcome $x$ is thoroughly investigated
After interviewing $\ell$ outcomes, we fully learn our preference ordering over these $\ell$ outcomes

## Pairwise Queries vs Interviews
Interviews are generally assumed to be a lot more costly than pairwise comparisons
- Pairwise comparisons are useful if the two outcomes are sufficiently distinct
- Interviews are needed when the outcomes are similar and more information is needed to rank them

## Elicitation Scheme/Strategy/Plan
An elicitation plan describes when and what to ask
The plan may depend on the result of the previous queries

## Probabilistic Preferences
Not all query results are deterministic

# Multi Criteria Ranking using Multi-Attribute Additive Functions
## Multi-Criteria Decision Analysis (MCDA)
A finite set of outcomes or alternatives $O=\{a,b,c,d,...\}$ is evaluated on a family of $n$ criteria or issues where $g_i(o)\in \mathbb{R}$ is the evaluation of issue $i$ in outcome $o$, for all $i\in\{1,...,n\}$ and $o\in O$

The greater $g_i(o)$,$o\in O$, the better outcome $o$ on issue $i$
- $a$ is at least as good as $b$ with respect to issue $i$ where $g_i(a)\geq g_i(b)$

## Multi-Attribute Additive Value Functions (MAAVF)
The agents utility is in the form of an additive value function, such that $$U(o)=\sum\limits_{i=1}^{n}u_i(g_i(o))$$
Where $u_i : \mathbb{R}\rightarrow\mathbb{R}$ is a non-decreasing marginal value function for issue $i,i\in\{1,...,n\}$
Sometimes $u_i(g_i(o_i))$ will just be referred to as $u_i(o_i)$

Value functions are increasing with respect to preference ordering
- $a\succ b \Longleftrightarrow U(a)>U(b)$
- $a\sim b \Longleftrightarrow U(a) = U(b)$

## Weighted Additive Utility Value Functions
Weighted additive value/utility functions are a particular case of the multi-attribute value function where $u_i=w_i\cdot g_i(o)$

## Ordinal Regression
The agent has some partial information about their preference ordering
$u_i$'s are unknown
Usually assumed that $g_i$'s are known

Goal is to find the agent's preference ordering
Use the partial preference ordering and a set of parameters (i.e. $u_i$'s) that respect the partial information found to generate a complete preference ordering

**UTA** - The first and well-known additive [[content/notes/Uni Content/Intelligent_Agents/Week 7/Notes/Ordinal Regression]] method
- Assumes that the agent knows their complete preference ordering over a set of reference outcomes (or alternatives) $O^R\subseteq O$
- Among many compatible additive value functions that are consistent with the partial preference information, only one is selected and used to generate a complete preference ordering
- Assumes that marginal value functions $u_i$'s are piecewise-linear

**UTA$^{GMS}$** - The first method of robust additive [[content/notes/Uni Content/Intelligent_Agents/Week 7/Notes/Ordinal Regression]]
- The agents ranking of reference outcomes does not need to be complete
- Takes into consideration the whole set of compatible additive value functions
- Marginal value functions are general non-decreasing functions

# Ordinal Regression via Linear Programming
## Principle of the UTA Method
### Assumptions
Agent knows their complete preference ordering over a set of reference outcomes $O^R \subseteq O$
The range of $g_i$ is $[\alpha_i,\beta_i]$,$\alpha_i<\beta_i$
- Finite bound
- $\alpha_i$ is the worst finite evaluation for issue $i$
- $\beta_i$ is the best finite evaluation for issue $i$
$u_i$'s are piecewise-linear, so that the interval $[\alpha_i,\beta_i]$ is divided into $\gamma_i\leq 1$ equal sub-intervals
$u_i$'s are normalised to bound $U(o)$ in the interval $[0,1]$
- $u_i(\alpha_i)=0$,$\forall i \in \{1,...,n\}$
- $\sum\limits_{i=1}^{n}u_i(\beta_i)=1$

### Reference Outcomes
A value function $U$ is compatible if and only if for each $c,d\in O^R$
- $U(c)\geq U(d)\Longleftrightarrow c\succeq d$
- $U(c)>U(d)\Longleftrightarrow c\succ d$
- $U(c)=U(d)\Longleftrightarrow c\sim d$

### Piece-Wise Linear Marginal Value Functions
For each $i\in \{1,...,n\}$, the range of $g_i$ is $[\alpha_i,\beta_i]$,$\alpha_i<\beta_i$
This interval is divided into $\gamma_i\geq 1$ equal sub-intervals $$[x_i^0,x_i^1],[x_i^1,x_i^2],...,[x_i^{\gamma_i-1},x_i^{\gamma_i}]$$ where $x_i^j=\alpha_i+\frac{j}{\gamma_i}(\beta_i-\alpha_i),j=1\text{...}\gamma_i$

The marginal value of an outcome $o\in O$ on issue $i$ is obtained by linear interpolation $$u_i(o_i)=u_i(x_i^j)+\frac{o_i-x_i^j}{x_i^{j+1}-x_i^j}(u_i(x_i^{j+1})-u_i(x_i^j))$$ $$o_i\in[x_i^j,x_i^{j+1}]$$The piecewise-linear additive model is completely defined by the marginal values at the breakpoints
i.e. $u_i(x_i^0)=u_i(\alpha_i),u_i(x_i^1),\text{...},u_i(x_i^{\gamma_i})=u_i(\beta_i)$

### Constraints for a Compatible Value Function
A value function $U(o)=\sum\limits_{i=1}^n u_i(o_i)$ is compatible if it satisfies the following set of constraints
$$\begin{array}{l}
        U(c)>U(d)\Longleftrightarrow c\succ d\\
        U(c)=U(d)\Longleftrightarrow c\sim d\\
    \end{array}
 \biggr\}\forall c,d\in O^R$$
 $$u_i(x_i^{j+1})-u_i(x_i^j)\geq 0,i=1,...,n,j=1,...,\gamma_i-1$$
 $$\begin{array} uu_i(\alpha_i)=0 & i=1,...,n\\\end{array}$$
$$\sum\limits_{i=1}^nu_i(\beta_i)=1$$

#### Example
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221125175642.png)
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221125180245.png)

### Solution or No Solution
If the optimal value of the objective function is equal to zero (i.e. if all $\sigma^+(c)'s$ and $\sigma^-(c)'s$ are set to zero), then there exists at least one value function $U(o)=\sum\limits_{i=1}^{n}u_i(\sigma_i)$ compatible with the preference ordering on $O^R$

If the optimal value of the objective function is greater than zero, then there is no compatible value function
in this case you can consider
- Increasing $\gamma_i$ for one or several marginal values
- Revising the preference ordering on $O^R$

# Robust Ordinal Regression ($UTA^{GMS}$)
## Limitations of UTA
If the linear program is feasible, then the choice of a compatible value function is arbitrary
Marginal value functions are limited to piecewise linear function
Complete preference ordering on reference outcomes is needed

## $UTA^{GMS}$
Takes into consideration the whole set of compatible additive value functions
Marginal value functions are general non-decreasing functions
The agent's ranking of reference outcomes does not need to be complete

## Assumptions
Agent knows their partial preference ordering over a set of reference outcomes $O^R\subset O,|O^R|=m$
Same assumptions as in UTA

## Necessary and Possible weak Preference Relations
Necessary weak preference relation $\succeq^N$ where $\alpha\succeq^N b\Leftrightarrow U(a)\geq U(b)$ for all compatible value functions
Possible weak preference relation $\succeq^p$ where $\alpha\succeq^p b\Leftrightarrow U(a)\geq U(b)$ for all compatible value function

## From Partial Preference Ordering
For any $a,b\in O^R$
- If $\alpha\succeq b\Rightarrow a\succeq^N b$
- If $\alpha\succ b\Rightarrow \neg(b \succeq^p a)$

## Constraints for a Compatible Value Function
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221205153020.png)

## Turning $E^{A^R}$ into a Linear Program
Use the same trick as used for UTA, we can rewrite the first set of constraints as $$U(c)\geq U(d)+\epsilon \Leftrightarrow c \succ d$$ for an aribitrarily small $\epsilon$

## Computation of $\succeq^N$ and $\succeq^P$
For all pairs of outcomes $(a,b)\in O \times O$, let $\pi_i$ be a permutation of the indices of outcomes from set $O^R\cup \{a,b\}$ that reorders them according to increasing evaluation on attribute $i$ i.e. $$g_i(a_{\pi_i(1)})\leq g_i(a_{\pi_i(2)})\leq...\leq g_i(a_{\pi_i(w)})$$ where $w=|O^R\cup \{a,b\}|$

Fix the characteristic points of $u_i,i=1,...,n$ in $g_i^0=\alpha_i$, $g_i^j=g_i(a_{\pi_i(j)})$ for $j=1,...,w$, $g_i^{w+1}=\beta_i$

## Ordinal Regression Constraints $E(a,b)$
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221205161107.png)

## Linear Programs to compute $\succeq^N$
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221205161229.png)
## Linear Program to compute $\succeq^p$
![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221205161328.png)
## Summary of $UTA^{GMS}$

![|450](content/notes/Uni%20Content/Intelligent_Agents/Images/Pasted%20image%2020221205161438.png)