---
title: Optimal Auctions
---
# Optimal Auctions for Selling a Single Item

So far we have ignored the mechanism's revenue (i.e. some of the payments made by the agents), except in attempting to keep it as close to zero as possible (budget balanced).
But in some auctions, it is desirable to maximise the seller's revenue

A seller my be willing to risk failing to sell the item even when there is an interested buyer
A seller may be willing sometimes to sell to a buyer who didn't make the highest bid

Mechanisms which are designed to maximise seller's expected revenue are known as as **optimal auctions**

## Optimal Auctions Setting

As assumed previously:
- Independent private valuations (IPVs)  
- Risk-neutral bidders

Additionally, we assume that:
- Each bidder i's valuation is drawn from some strictly increasing cumulative density function $F_i(v)$ with a PDF $f_i(v)$ that is continious and bounded below
- We allow $F_i \neq F_j$ : asymmetric auctions
- The seller knows each $F_i$

**Optimal Auction** - Maximises seller’s expected revenue subject to  
some form of individual rationality

### Example
2 bidders, $v_i$ uniformly distributed on $[0,1]$
Set reserve price $R$ and then run a second price auction:
- no sale if both bids below $R$
- sale at price $R$ if one bid above reserve price and other below
- sale at second highest bid if both bids are above reserve

Still dominant strategy to bid true values, so
- no sale if both bids below $R$ - happens with probability $R^2$ and revenue $=0$.
- sale at price $R$ if one bid above reserve price and other below happens with probability $2(1-R) R$ and revenue $=R$.
- sale at second highest bid if both bids are above reserve - happens with probability $(1-R)^2$ and revenue
$E\left[\min v_i \mid \min v_i \geq R\right]=\frac{1+2 R}{3}$
Expected revenue $=2(1-R) R^2+(1-R)^2 \frac{1+2 R}{3}$
Expected revenue $=\frac{1+3 R^2-4 R^3}{3}$
Maximising: $0=2 R-4 R^2$, or $R=\frac{1}{2}$

Reserve price of $1 / 2$ gives us revenue $=5 / 12$
Reserve price of 0 gives us revenue $=1 / 3$
Tradeoffs:
- lose sales when both bids were below $1 / 2$ - but low revenue then in any case and probability $1 / 4$ of happening
- increase price when one bidder has low value other high: happens with probability $1 / 2$

Like adding another bidder: increasing competition in the auction

## Designing Optimal Auctions

>[!Definition]
>Bidder i's virtual valuation is $\psi_i\left(v_i\right)=v_i-\frac{1-F_i\left(v_i\right)}{f_i\left(v_i\right)}$.
>- Let us assume that this is increasing in $v_i$ (e.g. in the case of uniform distribution on $[0,1]$ this is going to be $\left.2 v_i-1\right)$

>[!Definition]
Bidder i's bidder-specific reserve price $r_i^*$ is the value for which $\psi_i\left(r_i^*\right)=0$

### Myerson's Theorem
>[!Theorem]
>**Myerson**
>The **optimal (single-item) auction** is a sealed-bid auction in which every agent is asked to declare his valuation. The good is sold to the agent $i=\operatorname{argmax}_i \psi_i\left(\hat{v}_i\right)$, as long as $\hat{v}_i \geq r_i^*$. If the good is sold, the winning agent $i$ is charged the smallest valuation that she could have declared while still remaining the winner; i.e.
$\hspace{11em}\inf \left\{v_i^*: \psi_i\left(v_i^*\right) \geq 0 \text { and } \forall j \neq i, \psi_i\left(v_i^*\right) \geq \psi_j\left(\hat{v}_j\right)\right\}$

#### Understanding Myerson's Theorem
Sealed-bid auction in which every agent is asked to declare his valuation

Declarations are used to compute a virtual (declared) valuation $\psi_i\left(\hat{v}_i\right)$ for each agent $i$

The item is sold to the agent $i$ whose virtual valuation is the highest, as long as this value is nonnegative; i.e. $\hat{v}_i$ is no less than her reserve price $r_i^*$

If every agent's virtual valuation is negative, the seller keeps the item and achieves a revenue of zero

If the item is sold, the winning agent $i$ pays an amount equal to the smallest valuation that she could have declared while still remaining the winner:
$$
\inf \left\{v_i^*: \psi_i\left(v_i^*\right) \geq 0 \text { and } \forall j \neq i, \psi_i\left(v_i^*\right) \geq \psi_j\left(\hat{v}_j\right)\right\}
$$
## Analysing Optimal Auctions

**Optimal auction**:
- winning agent $i=\operatorname{argmax}_i \psi_i\left(\hat{v}_i\right)$, as long as $\hat{v}_i \geq r_i^*$.
- $i$ is charged the smallest valuation that she could have declared while still remaining the winner:
$$\inf \left\{v_i^*: \psi_i\left(v_i^*\right) \geq 0\right.$ and $\left.\forall j \neq i, \psi_i\left(v_i^*\right) \geq \psi_j\left(\hat{v}_j\right)\right\}$$

### Questions
Is this VCG?
- No, it's not efficient.
How should bidders bid?
- This is a second-price (Vickrey) auction with a reserve price, held in virtual valuation space.
- Neither the reserve prices nor the virtual valuation transformation depends on the agent's declaration
- Thus the proof that a Vickrey auction is dominant-strategy truthful applies here as well
What happens in the special case where all agents' valuations are drawn from the same distribution?
- We will have a Vickrey auction with reserve price $r^*$ satisfying $r^*-\frac{1-F_i\left(r^*\right)}{f_i\left(r^*\right)}=0$
What happens in the general case?
- The virtual valuations also increase weak bidders' bids, making them more competitive.
- Low bidders can win, paying less.
- However, **bidders with higher expected valuations must bid more aggressively**

## Optimal Auctions in Practise

Optimal Auctions are not really used in practise
- They are not **detail free**! The seller needs to know bidders' distributions.
- In a symmetric IPV setting, it is better to attract one additional bidder than to set an optimal reserve price.
- Intuitively, adding an extra bidder is similar to a reserve price (as her addition increases the competition among the other bidders) but different also (because she can buy the item herself).
- Trying to **attract more bidders** may be **more important** that trying to figure out bidders' valuation distributions in order to run an optimal auction.