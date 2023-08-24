# Offline vs Online

So far we have considered settings where all participants are present, the game is single-shot, and a centralised mechanism is in place

So we have considered
- offline setting (vs online setting)
- single-shot game (vs repeated games)

What if the participants arrive at different times (i.e. we are in an online setting)?

# Another \Marriage Problem

When someone proposes to me, should I accept or reject the current proposer if
- I know there are in total $n$ men
- I do not know the future proposers and their qualities
- My current decision is irrevocable

What is the best strategy to maximise the probability of finding the best partner?

## Strategy

- Reject the first $k$ candidates no matter how good they are.
- Learn how good they are
- Because there may be better ones later.
- After this, accept the first one who is better than all the first $k$ candidates.
- If all the rest $n-k$ are worse than the best one among the first $k$, then accept the last one
- I want to determine, for each $k$, the probability that I appoint the best candidate.
- And then maximise this probability over all $k$.
- Suppose I accept candidate $i(i>k)$.
- $S$ : the event that I accept the best one (amongst all $n$ candidates).
- $S_i$ : the event that I accept the best one (amongst all $n$ candidates), which is $i$.
- $\operatorname{Pr}[S]=\sum_{i=k+1}^n \operatorname{Pr}\left[S_i\right]$
- $\quad S_i$ : the event that I accept the best one, which is $i$.
- Let's compute $\operatorname{Pr}\left[S_i\right]$
- $S_i$ : event $S_i$ is true implies that candidate $i$ is the best among the $n$ people
- probability: $1 / n$. (assuming uniform distribution in the classical problem)
- Recall that my strategy is to reject the first $k$ candidates, event $S_i$ is true also implies that candidates $k+1, \ldots, i-1$ are all worse than the best one among $1, \ldots, k$.
- so that candidates $k+1, \ldots, i-1$ are all rejected.
- probability: $k /(i-1)$. (The best one among the first $i-1$ appears in the first $k$.)
- So, $\operatorname{Pr}\left[S_i\right]=\frac{1}{n} \cdot \frac{k}{i-1}$

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515180725.png|500]]

# The Secretary Problem

## Hire the Best Secretary

$\begin{array}{llllllllll}\boldsymbol{n} & \mathbf{1} & \mathbf{2} & \mathbf{3} & \mathbf{4} & \mathbf{5} & \mathbf{6} & \mathbf{7} & \mathbf{8} & \mathbf{9} \\ k+1 & 1 & 1 & 2 & 2 & 3 & 3 & 3 & 4 & 4 \\ \operatorname{Pr} & 1.0 & 0.5 & 0.5 & 0.433 & 0.433 & 0.428 & 0.414 & 0.410 & 0.406\end{array}$

For small $n$ we can find the optimal $\boldsymbol{k}$ using dynamic programming

## Selling a house

Given a series of offers, how many should you consider before accepting an offer?

## Job hunting

How many interviews should I take?

## Ski rental

Continuing to pay a repeating cost or paying a one-time cost which eliminates or reduces the repeating cost?