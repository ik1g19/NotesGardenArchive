---
title: Dependent Types
---
# Dependent Types

## Typing Rules

$$\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Delta\vdash exp_2\:B}
{\Gamma\vdash (exp_1,exp_2)\:A\times B}$$

$$
\dfrac{\Gamma\vdash exp\:A}
{\Gamma\vdash (exp,1)\:A\sqcup B}
\hspace{10mm}
\dfrac{\Gamma\vdash exp\:B}
{\Gamma\vdash (exp,2)\: A\sqcup B}
$$

$$
\dfrac{\Gamma, x:A\vdash exp\:B}
{\Gamma\vdash (\lambda x. exp)\:A\to B}
\hspace{10mm}
\dfrac{\Gamma\vdash f\:A\to B
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash f(exp)\:B}
$$ 
## Dependent Product Type

$$prod(A,x.B)$$

Where $x.B$ is a **type function** with argument $x$. It takes an element of type $A$ and returns a type

## Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Gamma\vdash exp_2\:B}
{\Gamma\vdash (exp_1,exp_2)\:A\times B}
$$

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Gamma\vdash exp_2\:B[exp_1/x]}
{\Gamma\vdash (exp_1,exp_2)\:prod(A, x.B)}
$$

$$
\dfrac{\Gamma\vdash France\:Country\;\;\;\;\;\;\Gamma\vdash Paris\:Cities[France/x]}
{\Gamma\vdash (France,Paris)\:prod(Country,x.Cities)}
$$

## Second Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash p\:A\times B\;\;\;\;\Gamma, x:A \vdash exp\:C}
{\Gamma\vdash exp[pr_1(p)/x]\:C}
$$

$$
\dfrac{\Gamma\vdash p\:prod(A,y.B)\;\;\;\;\Gamma,x\:A\vdash exp:C}
{\Gamma\vdash exp[pr_1(p)/x]\:C}
$$

$$
\dfrac{\Gamma\vdash p\:prod(Country,x.Cities)\;\;\;\;\;\;\Gamma, x:Country\vdash population\:Integer}
{\Gamma\vdash population[pr_1(p)/x]\:Integer}
$$

## Third Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash p\:A\times B\;\;\;\;\Gamma, z:B \vdash exp\:C}
{\Gamma\vdash exp[pr_2(p)/z]\:C}
$$

$$
\dfrac{\Gamma\vdash p\:prod(A,y.B)\;\;\;\;\Gamma,x\:A, z:B[x/y]\vdash exp:C}
{\Gamma\vdash exp[pr_1(p)/x,pr_2(p)/z]\:C}
$$

$$
\hspace{-5mm}
\dfrac{\Gamma\vdash p\:prod(Country,x.Cities)\;\;\;\;\;\;\Gamma, u:Country,z:Cities[u/x]\vdash isCapital\:Bool}
{\Gamma\vdash isCapital[pr_1(p)/u,pr_2(p)/z]\:Integer}
$$

## Typing Rules

$$
\dfrac{\Gamma, x:A\vdash exp\:B}
{\Gamma\vdash (\lambda x. exp)\:A\to B}
\hspace{10mm}
\dfrac{\Gamma\vdash f\:A\to B
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash f(exp)\:B}
$$ 

$$
\dfrac{\Gamma, x:A\vdash exp\:B[x/y]}
{\Gamma\vdash (\lambda x. exp)\:fun(A;y.B)}
\hspace{10mm}
\dfrac{\Gamma\vdash f\:fun(A;y.B)
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash f(exp)\:B[exp/y]}
$$ 
# First Order Logic

## Formulae with Quantifiers

1. $\forall x.\;A$ means that statement $A$ is true for **each** value of $x$
2. $\exists x.\;A$ means that statement $A$ is true for **at least** one value of $x$

# First Order Sequents

## Sequent

A sequent is an expression of the form $\phi_1,\dots,\phi_n\vdash \psi$, where
$\phi_1,\dots,\phi_n,\psi$ are formulae. A sequent is **valid** if formula $\psi$ is true under any interpretation of formulae under which all of the formulae  $\phi_1,\dots,\phi_n$ are true. Examples of valid sequents:
1. $\forall x\forall y.\; A\vdash \forall y\forall x.\; A$
2. $\forall x.\; A, \forall x.\;B \vdash \forall x.\; (A\wedge B)$
3. $\forall x.\; A\vdash A[y/x]$

## Inference Rules for Quantifiers

$$
\dfrac{\Gamma\vdash A[exp/x]}
{\Gamma\vdash \exists x.\; A}
$$

$$
\dfrac{\Gamma\vdash \exists x.\;B\;\;\;\;\Gamma, B\vdash C\;\;\;\;\; \text{$x$ does not occur in $\Gamma$ and $C$}}
{\Gamma\vdash C}
$$

$$
\dfrac{\Gamma\vdash \forall x.\,A}
{\Gamma\vdash A[exp/x]}
$$

$$
\dfrac{\Gamma\vdash A\;\;\;\;\; \text{$x$ does not occur in $\Gamma$}}
{\Gamma\vdash \forall x.\,A}
$$

# Restricted Quantifiers

## Domain Specification

$\forall x: A. B$ means that $B$ is true for all $x\in A$

$\exists x: A. B$ means that $B$ is true for at least one $x\in A$

Some standard domains:
- $\mathbb{Z}$ all integer numbers
- $\mathbb{N}$ all natural numbers (include 0)
- $\mathbb{Q}$ all rational numbers
- $\mathbb{R}$ all real numbers

## Inference Rules

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Gamma\vdash B[exp_1/x]}
{\Gamma\vdash \exists x\:A.\; B}
$$

$$
\dfrac{\Gamma\vdash \exists y\:A.\;B\;\;\;\;\Gamma,x\:A\vdash C}
{\Gamma\vdash C}
$$

$$
\dfrac{\Gamma\vdash \exists y:A.\;B\;\;\;\;\Gamma,x\:A, B[x/y]\vdash C}
{\Gamma\vdash C}
$$

$$
\dfrac{\Gamma, x\:A\vdash B[x/y]}
{\Gamma\vdash \forall y\:A.\;B}
$$

$$
\dfrac{\Gamma\vdash \forall y\:A.\;B
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash B[exp/y]}
$$

# Back to Types

## Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Gamma\vdash exp_2\:B[exp_1/x]}
{\Gamma\vdash (exp_1,exp_2)\:prod(A, x.B)}
$$

$$
\dfrac{\Gamma\vdash exp_1\:A\;\;\;\;\Gamma\vdash B[exp_1/x]}
{\Gamma\vdash \exists x\:A.\; B}
$$

## Second Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash p\:A\times B\;\;\;\;\Gamma, x:A \vdash exp\:C}
{\Gamma\vdash exp[pr_1(p)/x]\:C}
$$

$$
\dfrac{\Gamma\vdash \exists y\:A.\;B\;\;\;\;\Gamma,x\:A\vdash C}
{\Gamma\vdash C}
$$

## Third Dependent Product Type Rule

$$
\dfrac{\Gamma\vdash p\:prod(A,y.B)\;\;\;\;\Gamma,x\:A, z:B[x/y]\vdash exp:C}
{\Gamma\vdash exp[pr_1(p)/x,pr_2(p)/z]\:C}
$$

$$
\dfrac{\Gamma\vdash \exists y:A.\;B\;\;\;\;\Gamma,x\:A, B[x/y]\vdash C}
{\Gamma\vdash C}
$$

## Dependent Function Type Rules

$$
\dfrac{\Gamma, x\:A\vdash exp\:B[x/y]}
{\Gamma\vdash (\lambda x. exp)\:fun(A;y.B)}
\hspace{10mm}
\dfrac{\Gamma\vdash f\:fun(A;y.B)
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash f(exp)\:B[exp/y]}
$$

$$
\dfrac{\Gamma, x\:A\vdash B[x/y]}
{\Gamma\vdash \forall y\:A.\;B}
\hspace{10mm}
\dfrac{\Gamma\vdash \forall y\:A.\;B
\;\;\;\;\;\;
\Gamma\vdash exp\:A
}
{\Gamma\vdash B[exp/y]}
$$

