# One-sided Matching

Bipartite structure
- Individuals in one group has preferences over the individuals in the other group.

Examples
- House allocation
- Each individual owns a house and is interested in improving its utility by swapping with others

# House Allocation Problem

- A model for allocation of indivisible goods.
- A set of $n$ agents, each owns a unique house and a strict preference ordering over all $n$ houses.
- The objective is to reallocate the houses among the agents to improve the agents' utility

## **T**op **T**rading **C**ycle Mechanism

In each round:
1. Each agent points to her most preferred house (possibly her own house); each house points back to its owner
2. This creates a directed graph; in this graph, identify cycles
- Finite: cycle must exist
- Strict preferences: each agent is in at most one cycle
3. Assign each agent in a cycle to the house she is pointing at and remove her from the mechanism with her assigned house.
4. If all houses are assigned or all agents are assigned or all preference lists are empty, stop.
5. Otherwise, Repeat (i.e. go to step 1)

### Example

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515172302.png|250]]


```start-multi-column  
number of columns: 2  
largest column: left
border: off
shadow: off
```

$$\begin{aligned}
& \mathbf{a}_1: \mathbf{h}_3>\mathrm{h}_2>\mathbf{h}_1 \\
& \mathrm{a}_2: \mathrm{h}_1>\mathrm{h}_4>\mathbf{h}_2 \\
& \mathrm{a}_3: \mathbf{h}_1>\mathrm{h}_4>\mathbf{h}_3 \\
& \mathrm{a}_4: \mathrm{h}_3>\mathbf{h}_4
\end{aligned}$$

--- end-column ---

$a_1$ is matched to $h_3$ 
$a_3$ is matched to $h_1$ 
$a_4$ is matched to $h_4$ 
$\mathbf{a}_2$ is matched to $\mathbf{h}_2$

=== end-multi-column

### Pareto Optimality

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515172518.png|450]]

>[!Theorem]
>TTC allocation is **always** Pareto optimal

# Student Rooms Allocation

- A set of existing students $\left\{a_1, a_2, \ldots, a_n\right\}$, each occupies a room
- A set of newcomers $\left\{a_{n+1}, a_{n+2,}, \cdots, a_{n+m}\right\}$
- A set of vacant rooms $\{1,2, \ldots, m\}$

## You Request my House, I Get your Turn (**YRMH-IGYT**)

- Fix a priority order of the agents
- Let the agent with the top priority receive her first-choice room, the second agent receive her top choice among the remaining goods and so on, until someone requests the room of an existing tenant.
- If the existing tenant whose room is requested has already received a room, then proceed the assignment to the next agent. Otherwise, insert the existing tenant at the top of the priority order and proceed with the procedure.
- If at any step a cycle forms, the cycle is formed by existing tenants $\left(a_1, . ., a_k\right)$ where $a_1$ points to the house of agent $a_2$, who points to the house of $a_3$, and so on. In such a case assign these houses by letting them exchange, and then proceed with the algorithm

