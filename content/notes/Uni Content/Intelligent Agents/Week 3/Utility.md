---
title: "Utility"
---

# Basic Setting
A game is a mathematical model of interactive decision making
Different agents interact with the goal to achieve the best possible outcome

For an agent, making a decision means selecting one among multiple choices
$S = \{s_1,...,s_m\}$s denotes the choices available to an agent
Making a choice leads to an outcome
$\Omega = \{\omega_1,...,\omega_t\}$ denotes a set of outcomes

The outcome function $g:S\rightarrow \Omega$ maps each choice to an outcome
$g$ specifies the consequence of making a certain choice
We assume that given a pair of outcomes $(\omega,\omega ')$, an agent can say which they prefer
# Preferences
A preference is a binary relation $\succeq$ on $\Omega \times \Omega$
We assume the relation is
- Reflexive $$\omega \succeq \omega \text{ } \forall \text{ } \omega \in \Omega$$
- Total $$\forall \text{ } \omega, \omega '\in \Omega\text{,either }\omega \succeq \omega' \text{ or }\omega' \succeq \omega$$
- Transitive $$\forall\text{ }\omega,\omega',\omega''\in\Omega, \text{if } \omega\succeq\omega'\text{ and }\omega'\succeq\omega''\text{, then }\omega\succeq\omega'' $$
Given a pair of outcomes $\omega,\omega'$ $$\omega\succeq\omega'$$
Means that an agent prefers $\omega$ at least as much as $\omega'$
If both $$\omega\succeq\omega'\text{ and }\omega'\succeq\omega$$
then we are indifferent between the two - denoted by $$\omega \sim\omega'$$
If both $$\omega\succeq\omega'\text{ but not }\omega'\succeq\omega$$
then we strictly prefer $\omega$ over $\omega'$, and denote it by $$\omega\succ\omega'$$
# Utility
A utility function is a mapping $$u:\Omega\rightarrow\mathbb{R}$$
A utility function $u$ over $\Omega$ is said to represent a preference relation $\succeq$, iff for all $\omega,\omega'\in\Omega$ $$\omega\succeq\omega'\text{ iff }u(\omega)\geq u( \omega' )$$
Given a finite set $\Omega$, for every preference relation $\succeq$ on $\Omega\times\Omega$ there exists a utility function $u:\Omega\rightarrow\mathbb{R}$ that represents it

Utility functions are a numerical representation of preferences
An agent chooses an outcome over another not because of the numerical value but because of their preference
An agent choosing the best outcome is maximising their utility, as loong as the representation is the correct one
The numerical values themselves are not important, the relative order is
Utilities of different agents cannot generally be compared
# Formal Model of Decision
Formally representing decision-making as a tuple $$\langle S,\Omega ,g,\succeq ,u\rangle$$
Where
- $S$ and $\Omega$ are the set of choices and consequences
- $g:S\rightarrow\Omega$ is an outcome function that specifies the consequence of each choice
- $\succeq\subseteq\Omega\times\Omega$ is the agent's preference relation
- $u:\Omega\rightarrow\mathbb{R}$ is the utility function representing $\succeq$
# Rational Decision-Maker
A rational decision maker is one that makes the best possible choice
The agent makes the choice that maximises their utility $$s\in \text{argmax}_{s\in S}u(g(s))$$
# Decision under Uncertainty
Often we don't know what outcome will result by making a choice
For ervery option $s\in S$, there will be a range of possible outcomes with differing probabilities of occurring

Probability distributions are used to represent the uncertainty of an outcome
A probability distribution over a non-empty set of outcomes $\Omega$ is a function $$\mu:\Omega\rightarrow[0,1]$$
such that $$\sum\limits_{saddsa}\mu(\omega)=1$$
# Lotteries
A lottery over a set of outcomes $\Omega$ is a probability distribution over $\Omega$
A lottery is denoted by $L$
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221019124845.png]]
If the probability distribution of a conequence is 1, and all others 0, this is called a **degenerate lottery**
## Compound Lotteries
A lottery of lotteries
Given a set $L=\{L_1,...,L_n\}$ of lotteries, a compound lottery is a probability distribution $\mu$ over $L$ and is given by $$L*=[q_1(L_1),...,q_n(L_n)]$$
where $q_i=\mu(L_i)$
# Expected Utility
Given a set of outcomes $\Omega$ and a utility function $u:\Omega\rightarrow\mathbb{R}$, the expected utility of a lottery $L$, with probability distribution $\mu$, is given by $$EU(L)=\sum\limits_{\omega\in\Omega}u(\omega)\mu(\omega)$$
$EU$ is the expected value of the function $u$ given the probability distribution $\mu$
$EU$ is the average utility we could expect from the lottery
# Von Neumann Axioms
## Axiom (Continuity)
For every lotteries $L_1\succ L_2\succ L_3$, there exist $\alpha ,\beta \in [0,1]$ such that $$[\alpha L_1,(1-\alpha)L_3]\succ L_2 \succ [\beta L_1,(1-\beta)L_3]$$
## Axiom (Independence)
For all lotteries $L_1,L_2,L_3$ and $\alpha\in [0,1]$ $$L_1\succeq L_2\text{ iff }[\alpha L_1,(1-\alpha)L_3]\succeq[\alpha L_2, (1-\alpha)L_3]$$
## Morgenstern Theorem
Let $\hat{L}$ be the set of compound lotteries over a finite set $\Omega$ and let $\succeq$ be a preference relation over $\hat{L}$. Then the following are equivalent
- $\succeq$ satisfies continuity and independence
- There exists a utility function over $\Omega$ such that for all $L_1,L_2\in \hat{L}$ $$L_1\succeq L_2\text{ iff }EU(L_1)\geq EU(L_2)$$