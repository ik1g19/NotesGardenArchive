---
title: "Formulae"
---

$F(b_i)$ - The probability of winning given bid $b_i$
$\theta_i$ - The value of the item to agent $i$

### First Price Auction
#### Expected Utility
$E[u_i(\theta_i)|b_i]=(\theta_i-b_i)F(b_i)$

### Second-Price Sealed-Bid (Vickrey)
$f(b)=F(b+1)-F(b)$
#### Expected Utility
$E[u_i(\theta_i)|b_i]=\theta_iF(b_i)-\sum\limits_{b=0}^{b_i-1}b\cdot f(b)$
