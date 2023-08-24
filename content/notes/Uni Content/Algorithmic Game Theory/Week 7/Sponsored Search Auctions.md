# Advertiser/Bidder's Perspective

- Has a set of interested keywords
- Has a private value for each of the keywords
- Has a private daily/weekly/monthly budget
- Use their budget to buy clicks
- Obj: how to maximize utility, subject to budget?

## Advertiser's Perspective

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515181545.png|550]]

## Search Engine's Perspective

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515181626.png|700]]

# Search Engine

Products of Search Engines
- $k$ slots to sell
- Each slot can generate a certain number of clicks

- How to match advertisers with slots?
- How to charge advertisers?
- Obj: how to maximize revenue?

# Payment Models

Per-per-1000 impressions (per-per-mille or PPM/ PPI)
- An "impression" is when the ad is displayed
- Based on traditional advertising in printed media
- Used by search engines in early days (90s)

Pay-per-click
- Only pay when clicked
- Nowadays used by all search engines

Pay-per-conversion
- Only pay when actual purchase is made
- Need to track, and attribution problem

# Why Auctions?

In online advertising
- A large number of advertisers
- Rich user information and context
- Value of an impression/click varies largely across different advertisers

Pricing is based on the value to the clients/advertisers, not the cost to SE

Price differentiation is the key enabler of profit Essentially a price discovery mechanism

Auctions provide efficiency and revenue benefits over fixed prices, for markets where goods are hard for a seller to value

# How to Maximise Revenue

Objective: design online matching algorithm with good competitive ratio

For a moment let's consider a simplified version:
- All advertisers have the same budget
- There is only one ad slot
- Once a query comes in and the search engine matches it to a bidder, a payment is collected
- When a bidder is matched with a query, she pays what she bids
- When a bidders' budget is exhausted, she retreats from the market
- No 2nd price; no concern about DS truthfulness; integral matching; once matched, payment is collected

# Online Matching

**Greedy** - Always assign queries to the highest bidder

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515182139.png|600]]

# Competitive Ratio of Greedy Algorithm

**Offline Optimal** - Hindsight matching decision

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515182613.png|550]]

# Online Bipartite Matching

## Bipartite Matching

Two sets $\mathbf{L}$ and $\mathbf{R}$, each has $\mathbf{n}$ nodes

Each node in $\mathbf{L}$ is compatible with some nodes in $\mathbf{R}$

A matching is a subset of the edges s.t. every node is connected to at most one edge

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515182833.png|400]]

<span style="color:green">Maximal matching</span>:
- A matching that can not be made larger by adding another edge

<span style="color:red">Maximum matching</span>:
- A matching that contains the largest possible number of edges

<span style="color:red">Perfect matching</span>:
- A matching that matches all vertices
- Even number of vertices
- A.k.a., complete matching or 1-factor

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515182931.png|150]]

## Maximum Matching Algorithm

Problem: Find a maximum matching for a given bipartite graph
- A poly-time algorithm (Hopcroft and Karp 1973) using the concept of augmenting path

# Online Matching

What if we don't have the entire graph upfront?
- $\mathbf{L}$ is known. In each round, one node $v$ in $\mathbf{R}$ and its neighbours $\mathrm{N}(v)$ in $\mathrm{L}$ are revealed.

At that time, we have to decide to either:
- Pair $v$ with a node in $\mathbf{N}(v)$
- Don't pair $v$ with any node in $\mathrm{N}(v)$
- Again, decision cannot be canceled/revoked later

The goal is to construct as large a matching as possible
- Large: number of pairs matched
- Start thinking pairing keywords $\mathbf{R}$ with advertisers $\mathbf{L}$

# Comparison Benchmark

If it was offline, i.e., if we could make decisions until all nodes in $\mathbf{R}$ are revealed, we could make the best decision.
- Hopcroft and Karp's algorithm

We care about the competitive ratio
- Informally speaking, to what extend an online algorithm could have achieved with full hindsight.
- Formally, an algorithm ALG is c-competitive if $A L G(I) \leq c * O P T(I), \forall$ inputs $I$
- Worst-case analysis

# Online Fractional Bipartite Matching

Fractional matching
- When a node $\mathbf{v} \in \mathbf{R}$ arrives, not necessarily need to fully match it to a node in $N(v)$; could partially match $\mathbf{v}$ with some nodes in $\mathbf{N}(\mathbf{v})$
- In other words, decisions are not binary anymore

# **W**ater **L**evel Algorithm

a.k.a., water-filling algorithm

Physical metaphor:
- each vertex $\mathbf{w} \in \mathbf{L}$ is a container with capacity 1
- each vertex $\mathbf{v} \in \mathbf{R}$ is a source of one unit of water

High level description:
- When a node $\mathbf{v} \in \mathbf{R}$ arrives, drain water from $\mathbf{v}$ to $\mathbf{N}(\mathbf{v})$, always preferring the neighbour with the lowest current water level, until either
- all $\mathbf{N}(\mathbf{v})$ is full, or
- $\mathbf{v}$ is empty

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515185119.png|150]]

The WL algorithm is deterministic and is $\left(1-\frac{1}{e}\right)$-competitive for the online fractional bipartite matching problem

The analysis (that we didn't discuss here) is tight
- There is an instance/example for which WL returns a fractional matching of size $1-\frac{1}{e}$ times the maximum possible

# Online Randomised Bipartite Matching

But what about our original problem of integral online bipartite matching? (Note that fractional $\neq$ randomised)

The same idea as in WL can be used to design a randomised online algorithm for the original integral online bipartite matching problem RANKING algorithm
- $\left(1-\frac{1}{e}\right)$ - competitive
- High-level idea: a special transformation from WL such that the probability that a given edge is included in the matching plays the same role as its fractional value in the WL algorithm

>[!Tip]
>The competitive ratio of $\left(1-\frac{1}{e}\right)$ is tight!
>No online algorithm, deterministic or randomised, has a competitive ratio better than $1-\frac{1}{e}$ for maximum bipartite matching

# Online B-Matching

b-matching: every node in $\mathbf{L}$ can be matched for at most $\mathbf{b}$ times
- think of $b$ as the capacity of each node in $\mathbf{L}$
A deterministic algorithm BALANCE achieves the optimal competitive ratio $1-\frac{1}{e}$ for this problem
- The competitive ratio is $1-\frac{1}{\left(1+\frac{1}{b}\right)^b}$ to be precise, which approaches $1-\frac{1}{e}$ for large $b$
- Idea: when a node $\mathbf{v}$ in $\mathbf{R}$ arrives, match it to a node $\mathbf{N}(\mathbf{v})$ in $\mathbf{L}$ with highest remaining match "allowance"
	- If there is more than one such node, pick one arbitrarily

# The BALANCE Algorithm for B-Matching

Special Case: All budgets are $£ 100$; bids are either $£ 0$ or $£ 1$ (all non-zero bids are the same)

BALANCE: awards the query to an interested bidder who has the highest unspent budget

![[notes/Uni Content/Algorithmic Game Theory/Images/Pasted image 20230515185810.png|550]]

# Factor Revealing LP Algorithm

When a query arrives, allocate it to the bidder i maximizing $b_{\mathrm{i}} \times \varphi(\mathbf{x})$
- $\mathrm{b}_{\mathrm{i}}$ is bidder i's bid
- $\varphi(x)=1-e^{x-1}$
- $x$ is the fraction of i's budget that has been spent so far.
- In particular, $x=\frac{m_i}{B}$, where $m_i$ is the amount of money spent by i when the query arrives, and $B$ is i's total budget

# Advertiser/Bidder

- Each has a set of interested keywords
- Each has a private value for each of the keyword
- Each has a private daily/weekly/monthly budget
- Use their budget to buy clicks
- Obj: how to maximise utility, subject to budget?

