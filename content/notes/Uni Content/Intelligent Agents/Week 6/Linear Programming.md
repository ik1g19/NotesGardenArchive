---
title: "Linear Programming"
---

# Linear Programs
## Key Features
1. A linear objective function to be maximised/minimised
	e.g. $c_1x_1+c_2x_2+...+c_nx_n$
	We often use vector notation and dot product to write $\vec{c}\cdot\vec{x}$
2. A system of linear constraints
3. The decision variables are non-negative
	e.g. $\vec{x}\geq0$

$$
\begin{array}{ll@{}ll}
\text{minimise/maximise}  & \vec{c}\cdot\vec{x} & \color{red} \text{Objective Function} \\
\text{subject to}& A_1\vec{x}\leq\vec{b}_1 & \color{red} \text{Constraints}\\
                 & A_2\vec{x}\geq\vec{b}_2 \\
                 & A_3\vec{x}=\vec{b}_3 \\
                 & \vec{x}\geq0 & \color{red} \text{Non-negative Constraints} \\
\end{array}
$$

The value of the objective function given a setting of variables is called an **objective value**
Any setting of variables that satisfies all the constraints is called **feasible solution**

#### Example

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221118153844.png]]

![[notes/Uni Content/Intelligent Agents/Images/Pasted image 20221118153910.png]]

## Methods for solving LPs
- Simplex Method
- Ellipsoid Method
- Karmarkar's Algorithm

Tools
- MATLAB
- Mathematica
- CPLEX
- GUROBI