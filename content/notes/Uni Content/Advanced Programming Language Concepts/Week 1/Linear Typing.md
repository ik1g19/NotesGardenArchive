---
title: Linear Typing
---

# Propositional Logic
A **Tautology** is a formula which evaluates to true for any values of its propositional variables
e.g.
	$A\wedge B \to A$
	$A\to A\vee B$
	$A\to (B \to A)$
	$A\vee \neg A$
	$(A\to B)\wedge (\neg A\to B)\to B$
A **Sequent** is an expression of the form $\phi_1,\dots,\phi_n\vdash \psi$ 

For a sequent to be valid, it must evaluate to true for any potential assignment of variables that will make the formula on the left side of $\vdash$ evaluate to true

An **Inference Rule** is an expression of the form $\dfrac{\alpha_1\;\;\dots\;\;\alpha_n}{\beta}$, where $\alpha_1,\dots\alpha_n$ are sequents

The inference rule is valid if sequent $\beta$ is valid every time the sequents $\alpha_1,\dots\alpha_n$ are valid
#### Logical Inference Rules

![](Pasted%20image%2020230921210301.png)
#### Structural Inference Rules
$$
\dfrac{\Gamma\vdash B}
{\Gamma,A\vdash B} \hspace{10mm}(\text{Weakening})
$$ 
$$
\dfrac{\Gamma,A,A\vdash B}
{\Gamma,A\vdash B} \hspace{10mm}(\text{Contraction})
$$

$$
\dfrac{\Gamma,A,B\vdash C}
{\Gamma,B,A\vdash C} \hspace{10mm}(\text{Permutation})
$$ 
# Type Theory

## Basic Type Constructors

### Cartesian Product
$T_1 \times T_2 =\{(x,y)\;|\; x\in T_1, y\in T_2\}$
### Disjoint Union
$T_1 \sqcup T_2 =\{(x,1)\;|\; x\in T_1\}\cup \{(y,2)\;|\; y\in T_2\}$
### Function Type
$T_1 \to T_2$ is the set of all (computable) functions from type $T_1$ to type $T_2$

## Curry-Howard Isomorphism

>[!Tip]
>The Curry-Howard [Isomorphism](Isomorphism.md) is a way of looking at mathematical proofs and computer programs in a similar way. It says that a mathematical proof can be thought of as a way of solving a problem, just like a computer program. And just like a computer program, a proof has a clear structure and steps to follow. So, the ideas behind a proof can be translated into a computer program and vice versa.

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Delta\vdash exp_2\:B}
{\Gamma\vdash (exp_1,exp_2)\:A\times B}
\hspace{10mm}
\dfrac{\Gamma\vdash A\;\;\;\;\Delta\vdash B}
{\Gamma\vdash A\wedge B}
$$

$$
\dfrac{\Gamma\vdash exp\:A}
{\Gamma\vdash (exp,1)\:A\sqcup B}
\hspace{10mm}
\dfrac{\Gamma\vdash A}
{\Gamma\vdash A\vee B}
$$

$$
\dfrac{\Gamma\vdash exp\:B}
{\Gamma\vdash (exp,2)\:A\sqcup B}
\hspace{10mm}
\dfrac{\Gamma\vdash B}
{\Gamma\vdash A\vee B}
$$

$$
\dfrac{\Gamma, x:A\vdash exp\:B}
{\Gamma\vdash (\lambda x. exp)\:A\to B}
\hspace{10mm}
\dfrac{\Gamma, A\vdash B}
{\Gamma\vdash A\to B}
$$

$$\dfrac{\Gamma\vdash f\:A\to B\;\;\;\;\;\;\Gamma\vdash exp\:A}{\Gamma\vdash f(exp)\:B}\hspace{10mm}\dfrac{\Gamma\vdash A\to B\;\;\;\;\;\;\Gamma\vdash A}{\Gamma\vdash B}$$ ---
$$
\dfrac{\Gamma\vdash exp\:B}
{\Gamma,x\:A\vdash exp\:B}
\hspace{10mm}
\dfrac{\Gamma\vdash B}
{\Gamma,A\vdash B} 
$$ 
$$
\dfrac{\Gamma,x\:A\vdash exp\:B}
{\Gamma,x\:A,x\:A\vdash exp\:B}
\hspace{10mm}
\dfrac{\Gamma,A,A\vdash B}
{\Gamma,A\vdash B} 
$$

$$
\dfrac{\Gamma,x\:A,y\:B\vdash exp\:C}
{\Gamma,y\:B,x\:A\vdash exp\:C}
\hspace{10mm}
\dfrac{\Gamma,A,B\vdash C}
{\Gamma,B,A\vdash C} 
$$ 
## Type Interpretation of Propositional Logic

Using any function from $A$ to $B$ and any function from $B$ to $C$ one can construct a function from $A$ to $C$
$$
A\to B, B\to C \vdash A\to C
$$

Using any function from $A$ to $B$ and any function from $A$ to $C$ one can construct a function from $A$ to $B\times C$
$$
A\to B, A\to C \vdash A\to B\wedge C
$$
## Negation

$\neg\phi$ is logically equivalent to $\phi\to \bot$
$\bot$ is interpreted as empty type $Void$

# Resource Logics

## Resource Formulae and Sequents

$R_1\wedge R_2$ are two resources 

$R_1\vee R_2$ one of two resources

$R_1\to R_2$ is a disposable one-time device for converting a unit of resource $R_1$ into a single unit of resource $R_2$

$\bot$ is an impossible resource, an element of $\varnothing$

$R_1,\dots,R_n\vdash S$ means that using resources $R_1,\dots,R_n$ one can make resource $S$

## Affine vs. Linear Logic

In **affine logic**, some resources can be left unused (wasted)

In **linear logic**, all resources must be used (accounted for)

# Linear Types

**Linear type** systems have exchange only, so every variable must  
be used exactly once.
**Affine type** systems have exchange and weakening, so every  
variable can be used at most once.  
**Relevant type** systems have exchange and contraction, so every  
variable must be used at least once.  
**Ordered type** systems don’t use any of the three structural rules,  
so you have to use every variable exactly once in the order of  
creation