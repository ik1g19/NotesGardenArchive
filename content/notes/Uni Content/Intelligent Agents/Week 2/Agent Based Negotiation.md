---
title: "Agent Based Negotiation"
---

# **Conflict of Interest**
Conflict arises when agents have {different preferences or aims}
In [[content/notes/Uni Content/Intelligent Agents/Week 1/Introduction to Intelligent Agents#Multi-Agent System MAS|MAS]] conflicts arise when agents are {c1|self-interested} and the agents represent {c1|different stakeholders}
## Conflict Resolution
Conflict resolution is possible when there is {a mutual benefit to reach an agreement}
#### approaches for conflict resolution
- Auctions
- Voting
- Negotiation

### Auctions #flashcard 
Primarily used to allocate scarce resources or tasks

e.g.
- Items to buyers
- Advertising space
- Cloud computing
- Stocks and shares

#### Characterised by #flashcard 
- Clearly defined protocol
- Typically requires a trusted third party e.g. auctioneer
- Often involves a continuous resource such as money
- Exploits competition between agents - works better with more agents

### Voting #flashcard 
Used for group based decisions (**social chocice**)

#### characterised by #flashcard 
- A single decision from a (typically finite) number of options
- Each agent can have different preferences for each option - given by a preference order (ordinal utility function)
- Clearly defined protocol

### Negotiation #flashcard 
Governed by a protocol which defines the [[#rules of encounter flashcard|Rules of Encounter]] between the agents

{More flexible} compared to other approaches
- Prtocol typically involves {exchanging offers, but can also include other information such as arguments (reasons why)}
- Allows for {less structured} prtocols
- Often [[#Bilateral]], but some protocols support [[#Multi-Part Negotiation]]

Enables more complex types of agreements (multi-issue negotiation)
Often decentralised (can involve mediator - agent mediated negotiation)

##### Bilateral
Between two agents
##### Multi-Party Negotiation
Between more than two agents

#### rules of encounter #flashcard 
- Type of communication allowed
- Type of proposals that are allowed
- Who can make what proposal at what time

# **Negotiation**

## Characterising Agent Negotiations

### Negotiation Environment #flashcard 
Set of possible outcomes/agreements

#### Single-issue Negotiation (Distributive Bargaining) #flashcard 
- e.g. price
- Win-lose
- Competitive setting

#### Multi-issue Negotiation (Integrative Bargaining) #flashcard 
- Includes more issues
- Allows for mutual benefit and cooperation

### Agent Preferences #flashcard 
The preferences over all possible agreements (and disagreements), typically specified using utility functions

### Agent Negotiation Strategies #flashcard 
- Specifies the behaviour of the agents
- Actions employed at each possible decision point, given the information available to the agent

## Negotiation Protocols

- Ultimatum Game
- Alternating Offers
- Monotonic Concession Protocol
- Divide and Choose

### Single-Issue Negotiation
![|600](content/notes/Uni%20Content/Intelligent%20Agents/Images/Pasted%20image%2020221010165240.png)
Overlap between sellers minimum price and buyers maximum price is the agreement space

### Bilateral Negotiation: The Ultimatum Game #flashcard 
- Agent 1 suggests a division
- Agent 2 can only choose to accept or reject the proposed division
- If agent 2 rejects, no-one receives anything
- 'Take it or leave it'

#### Advantages/Disadvantages #flashcard 
- Agent 1 has a clear advantage - the **first-mover advantage**
- Assumes the agreement space (the size of the pie) is known - the seller's reserve and buyer's willingness to pay are shared knowledge
- No ability to explore the negotiation space

### Alternating Offers Protocol #flashcard 
- Negotiation consists of a number of rounds
- Agents exchange offers in an alternating fashion
- First player starts with proposing an offer
- Second player can either accept or reject and counter offer, or reject and break off negotiation
- Negotiation ends after set number of rounds (deadline) or if either players breaks off negotiations
![|400](content/notes/Uni%20Content/Intelligent%20Agents/Images/Pasted%20image%2020221010173339.png)

### Monotonic Concession Protocol #flashcard 
- Negotiations proceed in rounds
- In each round, agents simultaneously propose offers (without seeing the other offer)
- If both others 'match' then one of them is chosen
- Otherwise the negotiation proceeds to the next round
- In the next round at least one of the agents need to concede
- If neither of the agents concede, the negotiation ends without a deal

### Divide and Choose #flashcard 
- Used when a continuous resource needs to be divided between multiple agents
- Agent 1 divides the pie into 2 portions
- Agent 2 chooses one of the portions
![|400](content/notes/Uni%20Content/Intelligent%20Agents/Images/Pasted%20image%2020221014124749.png)

#### Properties #flashcard 
- Only works for resource allocation problems
- Also works for non-homogenous resources (when parts of the pie are more attractive)

## Desirable Properties of a Negotiation #flashcard 
- A deal should be better than no deal for all agents (individual rationality)
- There should be no pie left (Pareto efficiency)
- The agreement should be fair

## Agent Preferences
An agents preferences over outcomes are modelled using a utility function $U(o)$, where $o\in O$ is the offer and $O$ is the set of possible offers

### There are Two types of Utility Functions

#### Ordinal Preferences #flashcard 
A preference order over outcomes is specified but there is no numerical utility
The agents specify what they prefer but now by how much
- e.g. $U(o_1) > U(o_2)$ means that $o_1$ is preferred over $o_2$

#### Cardinal preferences
Each outcome has a numerical utility value
- e.g. $U(o_1) = 0.78, U(o_2) = 0.5$

We can always infer ordinal preferences from cardinal ones

## Price Negotiation: Utility Space
The utility space shows the utility of the two agents on respective axis for all possible outcomes
![[content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221014132155.png]]

## Time Pressure

### Deadlines #flashcard 
- Imposed by protocol
- Or determined by individual constraints (deadlines of agents can differ)

### Break-Off Probability #flashcard 
- Imposed by protocol
- Or agents can decide to break off negotiations themselves

### Bargaining Costs #flashcard 
- Fixed bargaining costs per round
- Discount factors

## Modelling Bargaining Costs
### Fixed Costs
Let $c_i$ denote the costs for agent $i$, and $t$ be the time or bargaining round, then the utility at time $t$ is given by: $$U_i^t = U_i - t \cdot c_i$$
### Discount Factors
Let $\delta_i < 1$ be the discount factor of agent $i$, then the utility is given by: $$U_i^t = U_i \cdot \delta_i^t$$
## Multi-Issue Negotiation
An offer/outcome $o$ is a vector consisting of a value $o_j$ for each issue $j$
Often a weighted additive utility function is assumed: $$U_i(o) = \sum_j w_{i,j} \cdot U_{i,j}(o_j)$$
Where $U_{i,j}(o_j)$ is the utility for issue $j$

## Pareto-Efficient Agreements
An agreement is said to be Pareto efficient (Pareto optimal) if no further improvement is possible in the utility of one agent, without reducing the utility of the other agents

**Pareto Efficient Frontier** - Set of all Pareto efficient agreements

![|500](content/notes/Uni%20Content/Intelligent%20Agents/Images/Pasted%20image%2020221014135629.png)

## Desriable Properties
- Agreements should be individually rational - $U(o)>U(disagreement)$
- Agreements should be Pareto efficient
- Agreements should be fair

## Fairness
### Utilitarian Social Welfare
Aka social welfare
Maximise the sum of utilities $$\max_{o\in O}U_1(o)+U_2(o)$$
### Egalitarian Social Welfare
Maximise the minimum utility $$\max_{o\in O}\min_{i\in \{1,2\}}U_i(o)$$
### Nash Bargaining Solution
Maximise the product of the utility of the agents (minus the disagreement pay off) $$\max_{o\in O}(U_1(o)-U_1(disagreement))\cdot (U_2(o)-U_2(disagreement))$$
The Nash Bargaining Solution is uniquely characterised by the following axioms or properties
- **Individual rationality** - The solution always satisfies $U_1 \geq U_1(dis)$ and $U_2 \geq U_2(dis)$
- **Pareto efficiency**
- **Invariance to equivalent utility representations** - The solution is insensitive to affine transformations
- **Independence of irrelevant alternative (IIA)** - Remove all the non-optimal agreements, and the optimal agreement remains the same
- **Symmetry (SYM)** - If the agents have the same preferences, then the solution gives them the same utilities

### Envy-freeness
No agent prefers the resources allocated to other agents
An agent is envious of another agent if it would prefer the allocation received by that agent
A solution is envy free if no agent prefers the allocation of another agent (no agent is envious)

Agents do not care about the utility of the other agent, only the share/allocation received by other agents


# Negotiation Strategies
#### Game Theoretic
- Assumes rules of the game, preferences and beliefes of all players are common knowledge
- Assumes full rationality on the part of all players
- Preferences encoded in a (limited) set of player types
- Closed systems, predetermined interaction, small sized games
- Nash equilibrium
#### Heuristic Perspective
- No common knowledge or perfect rationality assumptions needed
- Agent behaviour is modeled directly
- Suitable for open, dynamic environments
- Space of possibilities is very large
## Heuristics
Heuristics used when there is unknowns about the opponent
### Concession Strategy
What should be the target utility I think I should achieve at a particular point in the negotiation?
Well-known strategies include:
#### Time-dependent tactics 
Only depend on time/current round of the negotiation and not on the opponent's action
Let $U_{max}$ and $U_{min}$ denote the agent's maximum and minimum acceptable utility
The target utility offered at time $t$ will be $$U_{target}(t)=U_{min}+(1-F(t))(U_{max}-U_{min})$$
Where $F(t)$ is a function between 0 and 1 and gives the fraction of the distance between best and worst offer, using a function such as $$F(t)=(\frac{\min(t,T_{max})}{T_{\max}})^\frac{1}{\beta}$$
Where $T_{\max}$ is the deadline and $\beta$ is a constant
$F(0)=0$ and $F(T_{\max})=1$

##### Hard-Headed ($\beta \rightarrow 0$)
- No concessions
- Sticks to the initial offer throughout
##### Linear time-dependent concession ($\beta = 1$)
- Concession is linear in the time remaining until the deadline
##### Boulware ($\beta < 1$)
- Concedes very slowly, initial offer is maintained until just before the deadline
##### Conceder ($\beta > 1$)
- Concedes to the reservation value very quickly

![|400](content/notes/Uni%20Content/Intelligent%20Agents/Images/Pasted%20image%2020221014153655.png)
#### Tit-for-tat
The agent detects the concession the opponent makes during the previous negotiation round, in terms of increase in its own utility function
The concession the agent makes in the next round is equal to (or less than) the concession made by the opponent in the previous round $$concession\leq U_{own}(o_{opponent}^t)-U_{own}(o_{opponent}^{t-1})$$
As long as the offer falls in the acceptable region
### Muti-Issue Offer producing Strategy
Once a target utility is establised, what offer to produce at or around that target utility (to ensure Pareto efficiency)
## Optimal Concession Strategy
If everything is known, then it is easy to compute a **best response**
- i.e. the optimal concession given the utility and strategy of the opponent
If there is a lot of uncertainty about the opponents utility function and strategy, then machine learning techniques can be used to learn the opponent model
- If the opponent does the same then game-theoretic approaches can be useful
## Offer-producing Strategy
In multi-issue negotiation, you need to generate a value for each issue
It is a good idea to ensure that the offer is always Pareto efficient
If the utility functions are known, it is possible to calculate the Pareto-efficient offer at a certain target utility level
![[content/notes/Uni Content/Intelligent Agents/Images/Pasted image 20221017132254.png]]
## Unknown Opponent Utility
Typically the opponent utility is not known
- This is **private information**
It is possible to guess the opponent utiity function based on the offers received so far and the conessions observed
- e.g. The opponent is likely to concede on their least preferred issues first, this can be used to guess the weight of that issue
## Preference Uncertainty and Elicitation
In many cases even the agents own utility function is not fully known by itself
The utility function is obtained through a process called **preference elicitation**
- Has associated 'cognitive costs'
- Trade-off between minimizing cognitive cost and maximising utility

# Tags
FILE TAGS intelligentAgents