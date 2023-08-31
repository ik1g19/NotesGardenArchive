---
title: "Week 7"
---
# Languages, Problems and Complexity in Databases

## Boolean Queries
- Query evaluation reduces to BQE
- $\pi_\emptyset(E)=\{<>\}$ if **true**
- True or False queries
- $\pi_\emptyset(E)=\emptyset$ if **false**
- Queries are usually large
  - BQE focuses on the **hardness** of the query irrespective of the query size

## Computational Complexity Classes
- Groups decidable problems
- Each computational complexity class consists of **all problems that can be solved in a computational model under certain restrictions on the resources used to solve the problem**
- Examples of computational models
  - Turing Machine TM (deterministic Turing Machine)
  - Non-deterministic Turing Machine NTM
- Examples of resources
  - Amount of space (memory) needed to solve the problem
  - Amount of time needed to solve the problem
- Basic Computational Complexity Classes
  - Logspace (L)↔All decision problems solvable by a TM using extra memory bounded by a logarithmic amount in the input size
  - NLogspace (NL)↔All decision problems solvable by a NTM using extra memory bounded by a logarithmic amount in the input size
  - P (PTime)↔All decision problems solvable by a TM in time bounded by some polynomial in the input size
  - NP↔All decision problems solvable by a NTM in time bounded by some polynomial in the input size
  - PSpace↔All decision problems solvable by a TM using memory bounded by a polynomial in the input size
- Complexity
  - It is known that **LOGSPACE $\subset$ PSPACE**
  - **LOGSPACE $\subseteq$ NLOGSPACE $\subseteq$ P $\subseteq$ NP $\subseteq$ PSPACE**

## Problems in Databases
- Theorem QOT(RA) $\equiv _L$ **BQE(RA)**
  - $\equiv _L$ means logspace-equivalent
- BQE(L)
  - Input
    - A database  **D**
    - A boolean query  **Q** in  **L**
  - Question→$Q(D)\neq \emptyset$ (i.e. does  **D** satisfy  **Q**)
- QOT(L)
  - Input
    - A tuple of constants  **t**
    - A database  **D**
    - A query  **Q** in  **L**
  - Question→$t\in Q(D)$

## Complexity in Databases
- Combined Complexity↔Both  **D** and  **Q** are part of the input
  - Theorem, for L$\in$ {RA,...}
    -  **BQE(L)** is **PSPACE-complete**
- Query Complexity↔Fixed  **D**, input  **Q**
  - Theorem, for L$\in$ {RA,...}
    -  **BQEDL** is **PSPACE-complete**, for a fixed database  **D**
- Data Complexity↔Input  **D**, fixed  **Q**
  - Theorem, for L$\in$ {RA,...}
    -  **BQEQL** is in **LOGSPACE**, for a fixed query Q$\in$ L

## Problems in Databases
- Important problems for optimisation purposes
  -  **SAT(L)**
    - Input→A query Q$\in$ L
    - Question→Is there a (finite) database  **D** such that $Q(D)\neq \emptyset$?
      - If the answer is no, then **the input query Q makes no sense**
      - Query evaluation becomes **trivial - the answer is always no**
  -  **EQUIV(L)**
    - Input→Two queries $Q_1\in$ L and $Q_2\in$ L
    - Question→$Q_1(D)=Q_2(D)$ for every (finite) database  **D**? ($Q_1 \equiv Q_2$)
      - But we have to be sure that $Q_1(D)=Q_2(D)$ for every database  **D**
      - **Replace** a query Q_1 with a query Q_2 that is easier to evaluate
  -  **CONT(L)**
    - Input→Two queries $Q_1\in$ L and $Q_2\in$ L
    - Question→$Q_1(D)\subseteq Q_2(D)$ for every (finite) database  **D**? ($Q_1\subseteq Q_2$)
      - **Approximate** a query Q_2 with a query Q_1 that is easier to evaluate
      - But we have to be sure that $Q_1(D)\subseteq Q_2(D)$ for every database  **D**

## Solutions to Database Problems
- In RA
  - Satisfiability, equivalence and containment are **undecidable**
    - Perfect query optimisation is impossible
  - Evaluation is **decidable (and highly tractable)** in data complexity
- Conjunctive Queries↔Sublanguage of RA for which satisfiability, equivalence and containment are decidable
  - Simple **SELECT-FROM-WHERE** SQL queries
    - Only AND and equality in the WHERE clause

# Conjunctive Queries

# Containment and Minimisation
