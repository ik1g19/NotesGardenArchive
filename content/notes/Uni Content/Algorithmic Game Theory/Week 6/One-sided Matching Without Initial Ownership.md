# Pareto-Optimality

Given an initial situation (allocation), a Pareto improvement is a new situation where some agents will gain, and no agents will lose.

A situation is called Pareto dominated if there exists a possible Pareto improvement.

A situation is called Pareto optimal or Pareto efficient if no other situation could lead to an improvement for some agent without some other agent losing or if there's no scope for further Pareto improvement.

The Pareto frontier is the set of all Pareto efficient allocations

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515173256.png|300]]


# Serial Dictatorship

Fix an ordering of the agents $a_1, a_2, \ldots, a_n$
- It is a deterministic mechanism.

Let them take turns to pick their most preferred item that is still available

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515173111.png|600]]

- Serial Dictatorship is **Pareto-Optimal**
- Serial Dictatorship is **Truthful**

# **R**andom **S**erial **D**ictatorship/**R**andom **P**riority

- Draw a permutation of the agents uniformly at random. Then, let them successively choose an item in that order (so the first agent in the ordering gets first pick and so on).
- It is a randomized mechanism

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515173610.png|600]]

Random Serial Dictatorship is
- Ex-post Pareto-optimal, but it is not ex-ante PO
- When the decision process is random, there is a difference between ex-post (after) and ex-ante (before) Pareto-efficiency
- Ex-post Pareto-efficiency means that any outcome of the random process is Pareto efficient.
- Ex-ante Pareto-efficiency means that the lottery (randomized allocation) determined by the process is Pareto-efficient with respect to the expected utilities. That is: no other lottery gives a higher expected utility to one agent and at least as high expected utility to all agents

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515174357.png|500]]

Random Serial Dictatorship is
- Universal truthful
- For randomised mechanisms, there is a difference between universal truthfulness and truthful-in-expectation.
- Universal Truthfulness: A universally-truthful mechanism is a probability distribution over deterministic truthful mechanisms. The mechanism is truthful for any realisation of the set of mechanisms.
- Truthfulness-in-Expectation: A mechanism is truthful in expectation if an agent always maximises their expected utility by acting truthfully. The expectation is taken over the randomisation of the allocations

# Probabilistic Serial Mechanism

## Simultaneous Eating (Uniform Speed)

Agents simultaneously “eat” their most preferred items at a uniform speed, moving onto their next most preferred item whenever an item is fully eaten

![[notes/Uni Content/Algorithmic Game Theory/Images/simultaneous_eating.gif|500]]

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515175538.png|500]]

