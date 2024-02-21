---
title: "Linear Programming II"
---

# Computing the Nash Equilibrium of a two-player zero-sum Game

 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221122180841.png]]

**Zero-Sum** - Utilities add up to 0
Expected utility for player 1 will be:
- If player 2 picks 'Security' -> $3x-2(1-x)$
- If player 2 picks 'Tax Cuts' -> $-x+(1-x)$

## Computing Player 1's Strategy in NE
Player 2 will pick the pure strategy $s_2$ that maximises their utility
Since this is a zero-sum game - $s_2$ minimises the utility of player 1
So Player 1's expected utility will be $$\min(3x-2(1-x),-x+(1-x))$$
When choosing $x$, Player 1 should choose it so that it maximises $\min(3x-2(1-x),-x+(1-x))$
We can write this as a linear program: $$\begin{array}{ll@{}ll}
\text{maximise}  & z=\min(3x-2(1-x),-x+(1-x)) \\
\text{subject to}& 3x-2(1-x)-z\geq0 & \color{red} \text{Since z is the minimum of those two} \\
                 & -x+(1-x)-z\geq0 & \color{red} \text{it is either subtracting itself or less than it self} \\
                 & x\leq1 & \color{red} \text{x is a probability} \\
                 & x\geq0 \\
\end{array}$$
Solution $z=\frac{1}{7}$ and $x=\frac{3}{7}$
- Player 1 plays Economy with probability $\frac{3}{7}$ and plays Student Fees with probability $\frac{4}{7}$

## Computing Player 2's Strategy in NE

Expected utility for player 2 will be:
- If player 2 picks 'Economy' -> $-3y+(1-y)$
- If player 2 picks 'Student Fees' -> $2y-(1-y)$

Player 1 will pick the pure strategy $s_1$ that maximises their utility
Since this is a zero-sum game - $s_1$ minimises the utility of player 2
So Player 2's expected utility will be $$\min(-3y+(1-y),2y-(1-y))$$When choosing $y$, Player 2 should choose it so that it maximises $\min(-3y+(1-y),2y-(1-y))$

Written as a linear program:
$$\begin{array}{ll@{}ll}
\text{maximise}  & w=\min(-3y+(1-y),2y-(1-y)) \\
\text{subject to}& -3y+(1-y)-w\geq0 & \color{red} \text{Since z is the minimum of those two} \\
                 & 2y-(1-y)-w\geq0 & \color{red} \text{it is either subtracting itself or less than it self} \\
                 & y\leq1 & \color{red} \text{x is a probability} \\
                 & y\geq0 \\
\end{array}$$
Solution $w=-\frac{1}{7}$ and $y=\frac{2}{7}$
- Player 2 plays Security with probability $\frac{2}{7}$ and plays Tax Cuts with probability $\frac{5}{7}$

If Player 1 plays Economy with probability $x=\frac{3}{7}$ and Student Fees with probability $1-x=\frac{4}{7}$
- The expected utility of Player 1 is at least $z=\frac{1}{7}$
If Player 2 plays Security with probability $y=\frac{2}{7}$ and plays Tax Cuts with probability $1-y=\frac{5}{7}$
- The expected utility of Player 2 is at least $w=-\frac{1}{7}$
The sum of these two minimum expected utilities is $0$

# Structure of Linear Programs

The constraints in a Linear Program describe a **convex polytope** in n-dimensional space
The convex polytope corresponds to the **feasible region** that consists of all feasible solutions
The objective function will attain its minimum/maximum at a **vertex** of the polytope
If the set of constraints is infeasible, the linear program has no solutions
A linear program is unbounded if it has some feasible solutions but does not have a finite optimal objective value

## Unique Solutions
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221124142038.png]]

## Multiple Solutions
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221124142102.png]]

## Unbounded Solutions
 ![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221124142125.png]]

## Standard vs Slack Linear Programs
### Standard Form
Maximisation of a linear function subject to linear inequalities
$$\begin{array}{ll@{}ll}
\text{maximise}  & \vec{c}\cdot\vec{x} \\
\text{subject to}& A\vec{x}\leq \vec{b} \\
                 & \vec{x}\geq0 \\
\end{array}$$
### Slack (a.k.a. Normal Form)
Maximisation of a linear program subject to linear inequalities
$$\begin{array}{ll@{}ll}
\text{maximise}  & \vec{c}\cdot\vec{x} \\
\text{subject to}& A\vec{x} = \vec{b} \\
                 & \vec{x}\geq0 \\
\end{array}$$
## Transforming Linear Programs
We can transform an inequality constraint into an equality constraint by adding slack variables
$$\begin{array}{ll@{}ll}
\vec{a}_1\cdot\vec{x}\geq0\rightarrow \vec{a}_1\cdot\vec{x} - z_1=0,z_1\geq0 \\
\vec{a}_1\cdot\vec{x}\geq0\rightarrow \vec{a}_1\cdot\vec{x} + z_2=0,z_2\geq0 \\
\end{array}$$
$z_1$ (excess) and $z_2$ (deficit) are known as **slack variables**

We can transform an equality constraint into two inequality constraints e.g. $$\vec{a}_1\vec{x}=c\rightarrow \vec{a}_1\cdot\vec{x}\geq c,\vec{a}_1\cdot \vec{x}\leq c$$
A variable with no non-negativity constraints can be replaced by two non-negative variables
e.g. assume $x_2$ can take on any values
- We replace it with $x_2' - x_2''$ and add non-negativity constraints $x_2'\geq 0$ and $x_2''\geq 0$
- We replace each occurrence of $x_2$ with $x_2' - x_2''$
