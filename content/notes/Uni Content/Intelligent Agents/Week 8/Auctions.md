# Auction Design and Objectives
Auctions should maximise social welfare - allocate resources to those who value them the most
Auctions should be individually rational - agents should not be worse off from participating
Auctions should not be manipulatable - agents should be incentivised to behave truthfully
In some cases, the aim is to maximise revenue
# Single Item Auctions
## Families
### Open-outcry Auctions
- English auction
- Dutch auction
- Japanese auction
### Sealed-bid Auctions
- First-price auction
- Second-price (Vickrey) auction
- All-pay auction
## Setting
- $n$ strategic bidders
- Each bidder $i$ has a private valuation (willingness to pay) $\theta_i$ for the item
- Bidder utitlity model is quasilinear utility model
	- If $i$ loses and has to pay $p_i$, their utility is $-p_i$
		- In auctions where only winners pay, $i$'s utility is $0$
	- If $i$ wins at a price $p$, their utility is $u_i=\theta_i-p_i$
- Assuming
	- Independent private value model
		- i.e. a bidder's valuation does not depend on other bidder's valuations
	- Bidders cannot collude
## Objective and Allocation Rule
Let the goal of the auction designer be maximising the social welfare
Social welfare is $SW=\sum_limits_{i=1}^n\theta_ix_i$
$x_i$ is $1$ if $i$ wins, and $0$ if $i$ loses
$\sum\limits_{i=1}^nx_i\leq 1$ (feasibility constraint)
In a single-item auction, maximising social welfare means awarding the item to the bidder with the highest value
Let the allocation rule pick the bidder whose bid is the highest
## English Auction
1. Auctioneer starts the bidding at some low 'reservation price'
2. Bidders then shout out ascending prices
	1. Usually by some minimum increment set by the auctioneer
3. Auction ends once bidders stop shouting
	1. i.e. no bidder is willing to bid higher
4. Highest bidder wins the item and pays their bid
## Dutch Auction
1. Auctioneer starts the bidding at a high price
2. Auctioneer lowers the price until someone bids
3. Item is allocated to the first bidder at that current price
## Sealed-bid Auction
1. Each bidder submits their bid in a sealed envelope
2. Bidders do not see each others bids
3. Bids are collected by the auctioneer
4. Auctioneer determines the winner and the price to pay
	1. In the first-price sealed-bid auction, the highest bidder wins and pays their bid
## Vickrey (Second-price Sealed-bid) Auction
- The highest bidder wins but only pays the second highest bid (or the reserve price, whichever is higher)
# Analysing Auctions
## Every Auction is a Game
Consider first-price auction
- Let $b_i$ denote the bid placed by bidder $i$
- Let $b=(b_1,b_2,...,b_n)$ denote the bid profile of all bidders
- The set of actions available to each bidder is all possible bids that they can place
	- Effectively any non-negative real number, unless the auction has rules such as only integers
- The utility of each bidder $i$ depends on
	- Their private valuation or type $\theta_i$
	- The outcome (allocation + payment), which in turn depends on $b_i$ and the bids placed by the other bidders, hence on bid profile $b$
- The game induced by the first-price auction (or any auction) is not a strategic form game
- This is an example of a Bayesian game
## Model Decision Theoretic Framework
As assumed so far, a bidder does not know the private valuations of other players
However, in a decision theoretic framework, the bidder is assumed to have beliefs about the bid distribution
- Assume in the case of ties the bidder loses
- Let $F(b)$ denote the probability that all other bids are less than $b$ - so $F(b)$ is the probability of winning given bid $b$
Goal is to find the bidding strategy $s:\Theta\rightarrow A$, where $A$ is the set of actions or bids, which maximises the expected utility for any valuation $\theta_i\in\Theta$

# First-Price Auction
The utiity is given by $$u_i(\theta_i)=\biggr\{
\begin{array} a\theta_i-b_i & \text{if } b_i>\max_{j\neq i}b_j \\
0 & otherwise \\
\end{array}$$
The expected utility given by bid $b_i$ is then $$E[u_i(\theta_i)|b_i]=(\theta_i-b_i)F(b_i)$$
## Exercise: Discrete Bids
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221207180005.png|450]]
## Solution
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221207180031.png|450]]
## Optimal Bid for Continuous Bid Distributions
Using the equations from [[#First-Price Auction]]

Let $f(b)=\frac{dF(b)}{db}$ denote the first derivative of $F$
$f$ is the probability density and $F$ is the corresponding cumulative distribution
Find the optimal bid by setting the first derivative to 0: $$\frac{dE[u_i(\theta_i)]}{db_i}=0\leftrightarrow F(b_i)=(\theta_i-b_i)f(b_i)$$
For uniform distribution $F\sim U(0,1)$ this gives: (for $b_i<1$) $$b_i=\theta_i-b_i\leftrightarrow b_i=\frac{1}{2}\theta_i\leftrightarrow s(\theta_i)=\frac{1}{2}\theta_i$$
# Vickrey Auction
## Discrete Bids
The utility is given by: $$u_i(\theta_i)=\biggr\{
\begin{array} a\theta_i-\max_{j\neq i}b_j & \text{if } b_i>\max_{j\neq i}b_j \\
0 & otherwise \\
\end{array}$$
Let $f(b)=F(b+1)-F(b)$ denote the probability that the highest opponent bid is exactly $b$
The expected utility given bid $b_i$ is then: $$E[u_i(\theta_i)|b_i]=\theta_iF(b_i)-\sum\limits_{b=0}^{b_i-1}b\cdot f(b)$$
According to our tie breaking rule $i$ loses if tied with the highest opponent bid, to compute the expected payment we have to consider only cases where the highest opponent bid is at most $b_i-1$
## Exercise: Discrete Bids
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221208133946.png|450]]
## Solution
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221208134018.png|450]]
## Continuous Bids
Using the equations from [[#Vickrey Auction]]
For continuous distributions, $f$ is the probability density, and we replace the sum by the integral.
The expected utility given by bid $b_i$ then becomes: $$E[u_i(\theta_i)|b_i]=\theta_iF(b_i)-\int\limits_{b=0}^{b_i}b\cdot f(b)db$$
>[!Note]
>The integral is from $0$ to $b_i$ (and not $b_i-1$)
>The upper bound of the integral should be the largest opponent bid at which $i$ still wins, which would be $b_i-\epsilon$ for infinitely small $\epsilon$
>Therefor, under some conditions that we can assume for $F$ - we can put $b_i$ as the upper bound

The optimal bid is given by: $$\frac{dE[u_i(\theta_i)]}{db_i}=0\leftrightarrow \theta_if(b_i)=b_if(b_i)$$
> [!Note]
> Note that $s(\theta_i)=\theta_i$ is always an optimal outcome (second derivative is negative)

## Strategy Proofness
> [!Definition]
> A strategy is weakly dominant if, regardless of what any other players do, the strategy earns a player a utility at least as high as any other strategy

In the Vickrey auction, bidding $s_i(\theta_i)=\theta_i$ is a weakly dominant strategy
Such an auction is called
- Truthful
- Strategy-proof
- Incentive-compatible in dominant strategies

### Proof
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221208143548.png|450]]
![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221208143614.png|450]]

# Dutch Auction
Here strategy $s(\theta_i)$ is the point at which you bid when the clock reaches the vlaue $s(\theta_i)$
## First-Price Sealed-Bid Auction vs. Dutch Auction
In both auctions, if $i$ is the winner they pay $s(\theta_i)$
The amount of available information in both cases is the same [[notes/Uni Content/Intelligent Agents/Week 8/Notes/Pins/📌₈.₁]]
Therefor the optimal strategies in Dutch and first-price sealed-bid auctions are identical
These auctions are said to be **strategically equivalent**
# English Auction
More complicated strategy space
A bidder may place several bids throughout the auction, conditioning their new bid on the information revealed (an extensive form game)
To simplify the representation of a bidder's strategy in an English auction
- Let us interpret the strategy $s_i$ of bidder $i$ as the point at which $i$ should stop bidding
- $s_i$ is not necessarily the same as the last bid placed by bidder $i$, $b_i$, but that $b_i\leq s_i$ (no bidder outbids themselves)
## Vickrey Auction vs. English Auction
In English auction it is a dominant strategy for bidders to bid up to (and not beyond) their valuation
- i.e. setting $s_i=\theta_i$ is a dominant strategy for each bidder $i$
In Vickrey auction it is a dominant strategy to bid truthfully
- i.e. to set $b_i=\theta_i$
Bidding your trure valuation (setting $b_i=\theta_i$) is not exactly the same as bidding up to, and not beyond, your true valuation (setting $s_i=\theta_i$) but it is closesly similar
We say that these two auctions are weakly strategically equivalent

# Model (Bayes-Nash Framework)
$\theta_i$ is the type of agent $i$
Let $\theta_{-i}$ denote the types of other agents

In the independent private value model, a player's utility depends on their type $\theta_i$ and on the *actions* (i.e. bids) of all the players (not on their types)

Each player knows their own type $\theta_i$ but does not know the type of other players $\theta_{-i}$

Agents have a *prior distribution* $Pr(\theta_{-i})$ over other player's type profiles, which is *common knowledge*

Hence this is called a *Bayesian game*, and the solution concept is called a *Bayes-Nash equilibrium*

# Revenue Equivalence
Assume all bidders are risk-neutral and utility maximisers, and each has an indpendent private valuation for the single item, drawn from a common cumulative distribution $F(\theta)$ that is strictly increasing and atomless on $[L,H]$
Then any auction mechanism which
- In equilibrium, the item will be allocated to the agent with the highest valuation and
- Any agent with valuation $L$ has an expected utility of zero
yields the same expected revenue, and hence results in any bidder with valuation $\theta$ making the same expected payment

The four single-item auctions discussed before all satisfy the above. Therefore they are *revenue equivalent*

# Advertising Auctions
## Sponsored Search
Allocation of ad space alongside search results
- Multiple slots on single page sold simultaneously
- Uses an auction called Generalised Second Price (GSP) Auction
- Bidding and auction fully automated
## Banner Advertising
Advertising on regular webpages usually auctioned off
- Auctions are run by ad exchanges
- Each item is a slot on a webpage
- Auctioned off individually using the Vickrey auction